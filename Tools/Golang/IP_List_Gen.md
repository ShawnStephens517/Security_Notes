Same concept as Python version [[Tools/Python/IP_List_Gen|IP_List_Gen]]
```go
package main

import (
	"fmt"
	"math/rand"
	"os"
	"time"
)

func generateRandomIP() string {
	return fmt.Sprintf("%d.%d.%d.%d",
		rand.Intn(255-1)+1,
		rand.Intn(256),
		rand.Intn(256),
		rand.Intn(255-1)+1)
}

func main() {
	rand.Seed(time.Now().UnixNano()) // Seed the random number generator

	file, err := os.Create("ips.txt")
	if err != nil {
		fmt.Println("Error creating file:", err)
		return
	}
	defer file.Close()

	for i := 0; i < 25000; i++ {
		ip := generateRandomIP()
		_, err := file.WriteString(ip + "\n")
		if err != nil {
			fmt.Println("Error writing to file:", err)
			return
		}
	}

	fmt.Println("Successfully wrote 25,000 IPs to 'ips.txt'.")
}

```

`go run generate_ips.go`
