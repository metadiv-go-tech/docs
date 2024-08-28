# NanoID Generator Package

This package provides a simple and efficient way to generate unique identifiers using the NanoID algorithm. NanoID is a compact, URL-friendly, and collision-resistant identifier generator.

## Installation

To install the package, run the following command:

```bash
go get -u github.com/metadiv-go-tech/pkg_nanoid
```

## Usage

To generate a new NanoID, use the `New` function:

```go
id := pkg_nanoid.New()
```