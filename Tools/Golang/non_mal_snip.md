Quick test code. Compile and run

```go
package main

import(
	"fmt"
	"os/exec"
	"time"
	"os"
)


func main() {
	
	// Detect the operating system.
	osName := runtime.GOOS
	fmt.Printf("Running on: %s\n", osName)

	// Get the current working directory.
	dir, err := os.Getwd()
	if err != nil {
		fmt.Println(err)
		return
	}

	// Print the current working directory and operating system.
	fmt.Printf("Current working directory: %s\n", dir)

	hostname, err := os.Hostname()
	if err != nil {
		fmt.Printf("Error getting hostname: %v\n", err)
	} else {
		fmt.Printf("Hostname: %s\n", hostname)
	}

	cmd, err := exec.Command("whoami")
	output, err := cmd.Output()
	if err != nil{
		fmt.Printf("Error getting current user: %v\n", err)
		return
	}
	fmt.Printf("Current user: %s", output)
}
```
