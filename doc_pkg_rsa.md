# RSA Key Pair Generator

This Go package provides functionality to generate RSA key pairs. It includes a `KeyPair` struct to store the private and public keys, and a `GenerateKeyPair` function to create new key pairs.

## Installation

To install this package, run the following command:

```bash
go get -u github.com/metadiv-go-tech/pkg_rsa
```

## Usage

To generate a new RSA key pair, use the `GenerateKeyPair` function:

```go
package main

import (
	"fmt"
	"github.com/metadiv-go-tech/pkg_rsa"
)

func main() {
	keyPair, err := pkg_rsa.GenerateKeyPair()
	if err != nil {
		fmt.Println("Error generating key pair:", err)
		return
	}

	fmt.Println("Private Key:", keyPair.Private)
	fmt.Println("Public Key:", keyPair.Public)
}
```
