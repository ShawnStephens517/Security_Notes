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
