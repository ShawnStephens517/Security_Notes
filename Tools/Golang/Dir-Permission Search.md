Looks for writable directories across `C:\`
#### Build
`go get golang.org/x/sys/windows`
`GOOS=windows GOARCH=arm64 go build -o go-dir-arm.exe`
`GOOS=windows GOARCH=amd64 go build -o go-dir.exe`

 ```go
// +build windows

package main

import (
	"bytes"
	"fmt"
	"os"
	"os/exec"
	"path/filepath"
	"strings"
	"sync"
	"time"
)

const maxThreads = 5
const cpuFriendlyDelay = 25 * time.Millisecond

func checkACLWithPowerShell(path string) bool {
	script := fmt.Sprintf(`$acl = Get-Acl -LiteralPath '%s'; $acl.Access | Where-Object { ($_.IdentityReference -match 'Everyone|Users') -and ($_.FileSystemRights -match 'Write|FullControl') }`, path)

	cmd := exec.Command("powershell", "-NoProfile", "-NonInteractive", "-Command", script)
	var out bytes.Buffer
	cmd.Stdout = &out

	_ = cmd.Run()

	output := strings.TrimSpace(out.String())
	time.Sleep(cpuFriendlyDelay) // Yield CPU per check

	return output != ""
}

func main() {
	root := `C:\`
	var wg sync.WaitGroup
	sem := make(chan struct{}, maxThreads)

	_ = filepath.WalkDir(root, func(path string, d os.DirEntry, err error) error {
		if err != nil || !d.IsDir() {
			return nil
		}

		sem <- struct{}{}
		wg.Add(1)

		go func(p string) {
			defer wg.Done()
			defer func() { <-sem }()

			if checkACLWithPowerShell(p) {
				fmt.Printf("[!] Writable by 'Users' or 'Everyone': %s\n", p)
			}
		}(path)

		return nil
	})

	wg.Wait()
	fmt.Println("Scan complete.")
}
```