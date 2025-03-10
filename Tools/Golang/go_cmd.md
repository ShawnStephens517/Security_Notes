```go
package main

import (
    "fmt"
    "log"
    "os"
    "os/exec"
)

func main() {
    // Create a command to run cmd.exe
    cmd := exec.Command("cmd.exe")

    // Hook up cmd.exe's standard input/output/error to this process.
    // That way, you can interact with cmd.exe from your own console window.
    cmd.Stdin = os.Stdin
    cmd.Stdout = os.Stdout
    cmd.Stderr = os.Stderr

    // Start the cmd.exe process
    if err := cmd.Start(); err != nil {
        log.Fatalf("Failed to start cmd.exe: %v", err)
    }

    // Wait for the cmd.exe process to exit
    if err := cmd.Wait(); err != nil {
        log.Fatalf("cmd.exe exited with error: %v", err)
    }

    fmt.Println("cmd.exe has exited.")
}
```

Basic Logging Struct for script like execution
```go

entries := []logging.LogEntry{
		{Timestamp: time.Now(), CheckName: "Hostname", Message: "Captured", Data: "Host-01"},
		{Timestamp: time.Now(), CheckName: "Process List", Message: "Found", Data: "proc1, proc2"},
	}

	// Run OS-specific checks.
	switch runtime.GOOS {
	case "windows":
		fmt.Println("Running Windows Enumeration")
		oscheck.WinCheck()
	case "linux":
		fmt.Println("Running Linux Enumeration")
		oscheck.LinCheck()
	default:
		fmt.Printf("Unsupported OS: %s\n", runtime.GOOS)
	}

	// Write the results concurrently to multiple file formats.
	logging.WriteAllFormats(entries, "enumeration_results")
```
