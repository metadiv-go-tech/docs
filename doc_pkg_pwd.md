# Password Hashing Package

This Go package provides simple and secure password hashing functionality using the bcrypt algorithm.

## Features

- Password hashing using bcrypt
- Password verification against hashed passwords
- Uses default cost for bcrypt hashing

## Installation

To use this package in your Go project, run:

```bash
go get -u github.com/metadiv-go-tech/pkg_pwd
```

## Usage

### Hashing a Password

```go
package main

import (
    "fmt"
    "github.com/metadiv-go-tech/pkg_pwd"
)

func main() {
    password := "mySecurePassword123"
    hashedPassword := pkg_pwd.Hash(password)
    fmt.Printf("Hashed password: %s\n", hashedPassword)
}
```

### Verifying a Password

```go
package main

import (
    "fmt"
    "github.com/metadiv-go-tech/pkg_pwd"
)

func main() {
    password := "mySecurePassword123"
    hashedPassword := pkg_pwd.Hash(password)

    // Verify correct password
    isCorrect := pkg_pwd.Verify(password, hashedPassword)
    fmt.Printf("Password is correct: %v\n", isCorrect)

    // Verify incorrect password
    wrongPassword := "wrongPassword456"
    isIncorrect := pkg_pwd.Verify(wrongPassword, hashedPassword)
    fmt.Printf("Wrong password is correct: %v\n", isIncorrect)
}
```