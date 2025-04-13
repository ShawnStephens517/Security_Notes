Attempted to use for a challenge coin
```go
package main

import (
	"bytes"
	"flag"
	"fmt"
	"html"
	"os"
	"strconv"
)

// decodeEscapes scans the input string looking for occurrences of "/x" followed
// immediately by exactly 2 hex digits. It converts those into a byte and writes it
// to the output. Any characters that do not follow that pattern are simply copied.
func decodeEscapes(input string) []byte {
	var out bytes.Buffer
	for i := 0; i < len(input); {
		// Check for the pattern "/x" plus at least two characters
		if i+3 <= len(input) && input[i] == '/' && input[i+1] == 'x' {
			hexDigits := input[i+2 : i+4]
			if b, err := strconv.ParseUint(hexDigits, 16, 8); err == nil {
				// Successfully parsed two hex digits; write the corresponding byte.
				out.WriteByte(byte(b))
				i += 4 // Move past "/x" and the two hex digits.
				continue
			}
		}
		// Otherwise, just write the current byte as-is.
		out.WriteByte(input[i])
		i++
	}
	return out.Bytes()
}

// xorBytes applies a repeating-key XOR over data using the provided key.
func xorBytes(data []byte, key []byte) []byte {
	res := make([]byte, len(data))
	for i, b := range data {
		res[i] = b ^ key[i%len(key)]
	}
	return res
}

func main() {
	// Allow an optional XOR key via a command-line flag
	keyStr := flag.String("key", "", "XOR key. If provided, the decoded bytes will be XOR-ed with this key.")
	flag.Parse()

	// The obfuscated URL string (obtained from the challenge coin).
	// Note: The domain prefix "http://b/" is removed from processing.
	inputString := ``

	// Remove the "http://b/" prefix if present.
	prefix := "http://b/"
	if len(inputString) >= len(prefix) && inputString[:len(prefix)] == prefix {
		inputString = inputString[len(prefix):]
	}

	// First, unescape HTML entities.
	unescaped := html.UnescapeString(inputString)
	fmt.Println("After HTML unescape:")
	fmt.Println(unescaped)

	// Then decode the custom hex escapes. It will convert sequences like "/xcb" to the byte 0xCB.
	decodedBytes := decodeEscapes(unescaped)
	fmt.Println("\nDecoded bytes (hex):")
	fmt.Printf("%x\n", decodedBytes)

	// Also print the decoded bytes as a string (this may still be unreadable if it's further obfuscated)
	fmt.Println("\nDecoded string:")
	fmt.Println(string(decodedBytes))

	// If a XOR key is provided, apply XOR to the decoded bytes.
	if *keyStr != "" {
		fmt.Printf("\nApplying XOR with key \"%s\":\n", *keyStr)
		xored := xorBytes(decodedBytes, []byte(*keyStr))
		fmt.Println("Resulting string:")
		fmt.Println(string(xored))
		fmt.Println("\nResulting bytes (hex):")
		fmt.Printf("%x\n", xored)
	}

	// Exit cleanly.
	os.Exit(0)
}

// removePKCS7Padding checks and removes PKCS#7 padding from a byte slice.
func removePKCS7Padding(data []byte) ([]byte, error) {
	if len(data) == 0 {
		return nil, fmt.Errorf("empty data")
	}
	paddingLen := int(data[len(data)-1])
	if paddingLen == 0 || paddingLen > len(data) {
		return nil, fmt.Errorf("invalid padding length")
	}
	// Check that the last paddingLen bytes are all the same value.
	for i := len(data) - paddingLen; i < len(data); i++ {
		if int(data[i]) != paddingLen {
			return nil, fmt.Errorf("invalid padding")
		}
	}
	return data[:len(data)-paddingLen], nil
}

```
