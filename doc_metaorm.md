# MetaORM: A Modern ORM for Go

MetaORM provides these features to make [GORM](https://gorm.io/) more powerful and easier to use.

- Connection Helper: Simplify database connection configuration.
- Encryption: Protect sensitive data with AES encryption.
- Clause Builder: Build complex queries easily.
- Query Operation Helpers: Perform common query operations more easily.
- Write Operation Helpers: Perform common write operations more easily.

## Installation

```bash
go get -u github.com/metadiv-go-tech/metaorm
```

## Usage

### Connection Helper

#### Environment Variables

The following environment variables are required for connecting to the MySQL and PostgreSQL databases:

```bash
METAORM_HOST="localhost"
METAORM_PORT="3306"
METAORM_USERNAME="root"
METAORM_PASSWORD="password"
METAORM_DATABASE="database"
```

#### MySQL

```go
package main

import (
	"log"

	"github.com/metadiv-go-tech/metaorm"
)

func main() {
	// Connect to MySQL using the Connector instance
	db, err := metaorm.Connector.MySQL(false) // Pass 'true' for silent mode if needed
	if err != nil {
		log.Fatalf("Failed to connect to MySQL: %v", err)
	}
	defer db.Close() // Ensure the database connection is closed when done

	// Use the db instance for database operations
	log.Println("Successfully connected to MySQL!")
}
```

#### PostgreSQL

```go
package main

import (
	"log"

	"github.com/metadiv-go-tech/metaorm"
)

func main() {
	// Connect to PostgreSQL using the Connector instance
	db, err := metaorm.Connector.Postgres(false) // Pass 'true' for silent mode if needed
	if err != nil {
		log.Fatalf("Failed to connect to PostgreSQL: %v", err)
	}
	defer db.Close() // Ensure the database connection is closed when done

	// Use the db instance for database operations
	log.Println("Successfully connected to PostgreSQL!")
}
```

#### SQLite

File Path:
```go
package main

import (
	"log"

	"github.com/metadiv-go-tech/metaorm"
)

func main() {
	// Connect to SQLite using the Connector instance
	db, err := metaorm.Connector.SQLite("path/to/your/database.db", false) // Pass 'true' for silent mode if needed
	if err != nil {
		log.Fatalf("Failed to connect to SQLite: %v", err)
	}
	defer db.Close() // Ensure the database connection is closed when done

	// Use the db instance for database operations
	log.Println("Successfully connected to SQLite!")
}
```

In-Memory:
```go
package main

import (
	"log"

	"github.com/metadiv-go-tech/metaorm"
)

func main() {
	// Connect to an in-memory SQLite database using the Connector instance
	db, err := metaorm.Connector.SQLiteInMemory(false) // Pass 'true' for silent mode if needed
	if err != nil {
		log.Fatalf("Failed to connect to in-memory SQLite: %v", err)
	}
	defer db.Close() // Ensure the database connection is closed when done

	// Use the db instance for database operations
	log.Println("Successfully connected to in-memory SQLite!")
}
```

### Encryption

#### Environment Variables

For encryption, you need to set the `METAORM_ENCRYPT_KEY` environment variable.

```bash
METAORM_ENCRYPT_KEY="your-encryption-key"
```

#### Define the encrypted field

For field you need encrypted, set the type of the field to `[]byte`.

```go
type User struct {
	gorm.Model
	Name     []byte
}
```

#### Encrypt

```go
name := "John Doe"

user := &User{
    Name: metaorm.Encryption.Encrypt(name),
}
```

#### Decrypt

```go
name := metaorm.Encryption.Decrypt(user.Name)
```

### Clause Builder

#### Equal

```go
metaorm.Eq("field", value)
```

#### Decrypt Equal

This function will use the `METAORM_ENCRYPT_KEY` environment variable to decrypt the value before comparing it with the field.

```go
metaorm.DecryptEq("field", value)
```

#### Not Equal

```go
metaorm.Neq("field", value)
```

#### Decrypt Not Equal

This function will use the `METAORM_ENCRYPT_KEY` environment variable to decrypt the value before comparing it with the field.

```go
metaorm.DecryptNeq("field", value)
```

#### Greater Than

```go
metaorm.Gt("field", value)
```

#### Greater Than or Equal

```go
metaorm.Gte("field", value)
```

#### Less Than

```go
metaorm.Lt("field", value)
```

#### Less Than or Equal

```go
metaorm.Lte("field", value)
```

#### Like

```go
metaorm.Like("field", value)
```

#### Decrypt Like

This function will use the `METAORM_ENCRYPT_KEY` environment variable to decrypt the value before comparing it with the field.

```go
metaorm.DecryptLike("field", value)
```

#### Not Like

```go
metaorm.NotLike("field", value)
```

#### Decrypt Not Like

This function will use the `METAORM_ENCRYPT_KEY` environment variable to decrypt the value before comparing it with the field.

```go
metaorm.DecryptNotLike("field", value)
```

#### Similar

```go
metaorm.Similar("field", value)
```

#### Decrypt Similar

This function will use the `METAORM_ENCRYPT_KEY` environment variable to decrypt the value before comparing it with the field.

```go
metaorm.DecryptSimilar("field", value)
```

#### Not Similar

```go
metaorm.NotSimilar("field", value)
```

#### Decrypt Not Similar

This function will use the `METAORM_ENCRYPT_KEY` environment variable to decrypt the value before comparing it with the field.

```go
metaorm.DecryptNotSimilar("field", value)
```

#### In

The values must be a slice of any type.

```go
metaorm.In("field", value)
```

#### Decrypt In

This function will use the `METAORM_ENCRYPT_KEY` environment variable to decrypt the value before comparing it with the field.

```go
metaorm.DecryptIn("field", value)
```

#### Not In

```go
metaorm.NotIn("field", value)
```

#### Decrypt Not In

This function will use the `METAORM_ENCRYPT_KEY` environment variable to decrypt the value before comparing it with the field.

```go
metaorm.DecryptNotIn("field", value)
```

#### Is Null

```go
metaorm.IsNull("field")
```

#### Is Not Null

```go
metaorm.IsNotNull("field")
```

#### And

Pass the `metaorm.IClause` to the function.

```go
metaorm.And(
    metaorm.Eq("field", value), 
    metaorm.Neq("field", value),
)
```

#### Or

Pass the `metaorm.IClause` to the function.

```go
metaorm.Or(
    metaorm.Eq("field", value), 
    metaorm.Neq("field", value),
)
```

#### Between

```go
metaorm.Between("field", from, to)
```

#### Not Between

```go
metaorm.NotBetween("field", from, to)
```

### Query Operation Helpers

#### FindOne

FindOne is a function that finds one record from the database.

```go
v, err := metaorm.FindOne(db, metaorm.Eq("field", value))
```

#### FindAll

FindAll is a function that finds all records from the database.

```go
vs, err := metaorm.FindAll(db, metaorm.Eq("field", value))
```

#### FindAllComplex

FindAllComplex is a function that finds all records from the database with pagination and sorting.

```go
vs, p, err := metaorm.FindAllComplex(db, metaorm.Eq("field", value), metaorm.Page(1, 10), metaorm.Sort("field", "asc"))
```

#### Count

Count is a function that counts the number of records from the database.

```go
total, err := metaorm.Count(db, metaorm.Eq("field", value))
```

### Write Operation Helpers

#### Save

Save is a function that saves a record to the database.

```go
v, err := metaorm.Save(db, &record)
```

#### SaveAll

SaveAll is a function that saves all records to the database.

```go
vs, err := metaorm.SaveAll(db, vs)
```

#### Delete

Delete is a function that deletes a record from the database.

```go
err := metaorm.Delete(db, &record)
```

#### DeleteAll

DeleteAll is a function that deletes all records from the database.

```go
err := metaorm.DeleteAll(db, vs)
```

#### DeleteBy

DeleteBy is a function that deletes records from the database by a clause.

```go
err := metaorm.DeleteBy(db, metaorm.Eq("field", value))
```
