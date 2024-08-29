# Metadiv `quick_setup.go`

Here is the example of the `quick_setup.go` file:

```go
package mod_meta_static

import "github.com/metadiv-go-tech/metagin"

// @title mod_meta_static
// @version v0.0.0

// @license.name All rights reserved by Metadiv Technology Limited
// @license.url https://metadiv.io

func QuickSetup() {
	metagin.SetupSwagger(ModName)

	metagin.Migrate()
}
```