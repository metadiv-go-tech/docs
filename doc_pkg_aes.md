# Aes Encryption and Decryption Package

This package provides functions to encrypt and decrypt data using AES encryption. It supports both byte slices and strings as input and output formats.

## Installation

```bash
go get -u github.com/metadiv-go-tech/pkg_aes
```

## Usage

### Encryption

```go
package main

import (
	"fmt"
	"github.com/metadiv-go-tech/pkg_aes"
)

func main() {
	// Define your encryption key
	key := "your-secret-key-here"

    // Byte slice to byte slice encryption
	data := []byte("Sensitive data")
	encryptedBytes := pkg_aes.Encrypt.BytesToBytes(data, key)
	fmt.Printf("Encrypted bytes: %v\n", encryptedBytes)

    // Byte slice to string encryption
    encryptedString := pkg_aes.Encrypt.BytesToString(data, key)
	fmt.Printf("Encrypted string: %s\n", encryptedString)

    // Byte slice to base64 encryption
    encryptedBase64 := pkg_aes.Encrypt.BytesToBase64(data, key)
	fmt.Printf("Encrypted base64: %s\n", encryptedBase64)

    // String to byte slice encryption
	plaintext := "Hello, World!"
	encryptedBytes := pkg_aes.Encrypt.StringToBytes(plaintext, key)
	fmt.Printf("Encrypted bytes: %v\n", encryptedBytes)

    // String to string encryption
    encryptedString := pkg_aes.Encrypt.StringToString(plaintext, key)
	fmt.Printf("Encrypted string: %s\n", encryptedString)

    // String to base64 encryption
	encryptedString := pkg_aes.Encrypt.StringToBase64(plaintext, key)
	fmt.Printf("Encrypted string: %s\n", encryptedString)
}
```

### Decryption

```go
package main

import (
	"fmt"
	"github.com/metadiv-go-tech/pkg_aes"
)

func main() {
	// Define your encryption key
	key := "your-secret-key-here"

    // Byte slice to byte slice decryption
    decryptedBytes := pkg_aes.Decrypt.BytesToBytes(encryptedBytes, key)
	fmt.Printf("Decrypted bytes: %v\n", decryptedBytes)

    // Byte slice to string decryption
    decryptedString := pkg_aes.Decrypt.BytesToString(encryptedBytes, key)
	fmt.Printf("Decrypted string: %s\n", decryptedString)

    // String to byte slice decryption
    decryptedBytes := pkg_aes.Decrypt.StringToBytes(encryptedString, key)
	fmt.Printf("Decrypted bytes: %v\n", decryptedBytes)

    // String to string decryption
    decryptedString := pkg_aes.Decrypt.StringToString(encryptedString, key)
	fmt.Printf("Decrypted string: %s\n", decryptedString)

    // Base64 to byte slice decryption
    decryptedBytes := pkg_aes.Decrypt.Base64ToBytes(encryptedBase64, key)
	fmt.Printf("Decrypted bytes: %v\n", decryptedBytes)

    // Base64 to string decryption
    decryptedString := pkg_aes.Decrypt.Base64ToString(encryptedBase64, key)
	fmt.Printf("Decrypted string: %s\n", decryptedString)
}
```