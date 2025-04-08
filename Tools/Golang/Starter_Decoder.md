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
	inputString := `http://b/xcb/xfa/x1b&lt;W/xb2/x8d/xb0/xe0/xb3/xcb1/xa95/x9d/x88/x8f/xa3]/x01,T/xf4/x7f/xabe/xf5/x0c/xa1/x89su+{/x12/x99]/x95/x03/x12/x8e/xfd/xca/x7f/xdaN/x0b/xd2/xf6/xda/xecX/xecM&amp;/x02{/x00/xf9l/xb7/x80:/x87/x0c/xb4&#039;/xb1L/x02/x00/xc9/xa1/xc9V/xbe/x10/xd5/x88R]/xde/xfc/x91kl/xbb/x8a/xf3/xef/xbfN/xfa/xe0/xb6_?!v/x9e/x82/x80i/xe6{/x95zU/xd7/xcd/x08v/x12/x8b/xe7/x86-/x19/x04:/x1a{~l/xa2/xac/xa2`

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

```
