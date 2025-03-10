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

Example Setup Cobra Flags:
```go
var rootCmd = &cobra.Command{
	Use:   "goenumer",
	Short: "A cross-platform enumeration tool for Purple-Teaming",
	Long: `goenumer is a lightweight tool that mimics some functionallity found in WinPeas/LinPeas.

Flags:
-eg, --exfilGit: Exfil results of the enumeration to a Git Repo.
-egP, --gitPort: Specify a port to push to if not HTTP/S based.
--eh, --exfilHTTP: Exfil to a Web Server.
--ehP, --httpPort: Specify port for the receiving Web Server.
--ChariZarD: Runs all nefarious functions on the machine. This is a designed to be extremely noisy.
-OA, --outputall: Outputs results to CSV, HTML, JSON files.
-OH, --outputHTML: Outputs results to HTML.
-OJ, --outputJSON: Outputs results to JSON.
-OC, --outputCSV: Outputs results to CSV.
-fn, --filename: Base name for the results file/s.
`,	
	Run: func(cmd *cobra.Command, args []string) {
		// Call your enumeration functions here based on OS
	},
}
func init (){
	rootCmd.Flags().BoolP("help", "h", false, "Displays help info")
	rootCmd.Flags().StringP("exfilGit","eg","", "Exfil results to Git Repo")
	rootCmd.Flags().StringP("exfilHTTP","eh","","Exfil results to Web Server")
	rootCmd.Flags().StringP("outputall","OA","","Export to CSV, HTML, JSON")
	rootCmd.Flags().StringP("outputHTML","OH","","Export to HTML Only")
	rootCmd.Flags().StringP("outputJSON","OJ","","Export to JSON Only")
	rootCmd.Flags().StringP("outputCSV","OC","","Export to CSV Only")
	rootCmd.Flags().StringP("filename","fn","enumerresults"+ time.now(),"Base name for the Output files")
	rootCmd.Flags().IntP("gitPort","egP",443,"Non Standard port for Git operations. EX:5000")
	rootCmd.Flags().IntP("httpPort","ehP",80, "Specify Web Server receiving the results. EX: 443 or 8080")
}
```


Example Float Sleep Timer. Used for odd random sleep timer for hiding better:
```go
package main

import (
	"fmt"
	"time"
)
//Use fun math equations and the float to sleep. Example: Sqrt of a random prime number.
func main() {
	floatSeconds := 1.5
    
    // Convert float seconds to nanoseconds (int64)
	duration := time.Duration(floatSeconds * float64(time.Second))

    fmt.Printf("Sleeping for: %v\n", duration)
	time.Sleep(duration)
    fmt.Println("Wake up")
}
```
