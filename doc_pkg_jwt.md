# Jwt Encode and Decode

Jwt Encode and Decode is a package that provides functions to encode and decode JWT tokens.

## Installation

```bash
go get -u github.com/metadiv-go-tech/pkg_jwt
```

## Usage

### Create a new JWT

```go
// Create a new JWT
jwt := NewJwt()

// Set values
jwt.Set("user_id", 123)
jwt.Set("username", "john_doe")
jwt.Set("is_admin", false)

// Get values
userId := jwt.Get("user_id")
username := jwt.Get("username")
isAdmin := jwt.Get("is_admin")

// Print the values
fmt.Printf("User ID: %v\n", userId)
fmt.Printf("Username: %v\n", username)
fmt.Printf("Is Admin: %v\n", isAdmin)

// Get a non-existent key
email := jwt.Get("email")
fmt.Printf("Email: %v\n", email) // Will print "Email: <nil>"
```

### Encode a JWT

#### Encode with secret

```go
// Create a new Jwt object
jwt := &Jwt{
    data: map[string]interface{}{
        "user_id": 123,
        "role":    "admin",
    },
}

// Define the secret key and duration
secret := "my-secret-key"
duration := 24 * time.Hour // 24 hours

// Encode the JWT
token, err := EncodeWithSecret(jwt, secret, duration)
if err != nil {
    fmt.Printf("Error encoding JWT: %v\n", err)
    return
}

fmt.Printf("Encoded JWT: %s\n", token)
```

#### Encode with RSA

```go
// Create a new Jwt object
jwt := &Jwt{
    data: map[string]interface{}{
        "user_id": 123,
        "role":    "admin",
    },
}

// Load the RSA private key
privateKeyPEM, err := ioutil.ReadFile("path/to/private_key.pem")
if err != nil {
    fmt.Printf("Error reading private key: %v\n", err)
    return
}

privateKey, err := jwt.ParseRSAPrivateKeyFromPEM(privateKeyPEM)
if err != nil {
    fmt.Printf("Error parsing private key: %v\n", err)
    return
}

// Define the duration
duration := 24 * time.Hour // 24 hours

// Encode the JWT
token, err := EncodeWithRSA(jwt, privateKey, duration)
if err != nil {
    fmt.Printf("Error encoding JWT: %v\n", err)
    return
}

fmt.Printf("Encoded JWT: %s\n", token)
```

### Decode a JWT

#### Decode unverified

```go
// Example JWT token (this is a dummy token, don't use in production)
token := "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiaWF0IjoxNTE2MjM5MDIyfQ.SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV_adQssw5c"

// Decode the token without verification
jwt := pkg_jwt.DecodeUnverified(token)

if jwt != nil {
    fmt.Println("Token decoded successfully:")
    fmt.Printf("Subject: %s\n", jwt.Subject)
    fmt.Printf("Name: %s\n", jwt.Name)
    fmt.Printf("Issued At: %v\n", jwt.IssuedAt)
} else {
    fmt.Println("Failed to decode token")
}
```

#### Decode with secret

```go
// Example JWT token (this is a dummy token, don't use in production)
token := "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiaWF0IjoxNTE2MjM5MDIyfQ.SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV_adQssw5c"

// The secret key used to sign the token
secret := "your-secret-key"

// Decode and verify the token
jwt, err := pkg_jwt.DecodeWithSecret(token, secret)

if err != nil {
    fmt.Printf("Failed to decode token: %v\n", err)
    return
}

fmt.Println("Token decoded and verified successfully:")
fmt.Printf("Subject: %s\n", jwt.Get("sub"))
fmt.Printf("Name: %s\n", jwt.Get("name"))
fmt.Printf("Issued At: %v\n", jwt.Get("iat"))
```

#### Decode with RSA

```go
// Example JWT token (this is a dummy token, don't use in production)
token := "eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiaWF0IjoxNTE2MjM5MDIyfQ.NHVaYe26MbtOYhSKkoKYdFVomg4i8ZJd8_-RU8VNbftc4TSMb4bXP3l3YlNWACwyXPGffz5aXHc6lty1Y2t4SWRqGteragsVdZufDn5BlnJl9pdR_kdVFUsra2rWKEofkZeIC4yWytE58sMIihvo9H1ScmmVwBcQP6XETqYd0aSHp1gOa9RdUPDvoXQ5oqygTqVtxaDr6wUFKrKItgBMzWIdNZ6y7O9E0DhEPTbE9rfBo6KTFsHAZnMg4k68CDp2woYIaXbmYTWcvbzIuHO7_37GT79XdIwkm95QJ7hYC9RiwrV7mesbY4PAahERJawntho0my942XheVLmGwLMBkQ"

// Load the RSA public key
publicKeyPEM, err := ioutil.ReadFile("path/to/public_key.pem")
if err != nil {
    fmt.Printf("Error reading public key: %v\n", err)
    return
}

publicKey, err := jwt.ParseRSAPublicKeyFromPEM(publicKeyPEM)
if err != nil {
    fmt.Printf("Error parsing public key: %v\n", err)
    return
}

// Decode and verify the token
jwt, err := pkg_jwt.DecodeWithRSA(token, publicKey)

if err != nil {
    fmt.Printf("Failed to decode token: %v\n", err)
    return
}

fmt.Println("Token decoded and verified successfully:")
fmt.Printf("Subject: %s\n", jwt.Get("sub"))
fmt.Printf("Name: %s\n", jwt.Get("name"))
fmt.Printf("Issued At: %v\n", jwt.Get("iat"))
```