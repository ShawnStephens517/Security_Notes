
```go
package main

import (
	"fmt"
	"os"
)

func generateFourDigitNumbers() []string {
	numbers := make([]string, 10000)
	for i := 0; i < 10000; i++ {
		numbers[i] = fmt.Sprintf("%04d", i)
	}
	return numbers
}

func writeNumbersToFile(numbers []string, filename string) error {
	file, err := os.Create(filename)
	if err != nil {
		return err
	}
	defer file.Close()

	for _, number := range numbers {
		_, err := file.WriteString(number + "\n")
		if err != nil {
			return err
		}
	}
	return nil
}

func main() {
	numbers := generateFourDigitNumbers()
	err := writeNumbersToFile(numbers, "four_digit_numbers.txt")
	if err != nil {
		fmt.Println("Error writing to file:", err)
	} else {
		fmt.Printf("Successfully wrote %d numbers to 'four_digit_numbers.txt'.\n", len(numbers))
	}
}

```