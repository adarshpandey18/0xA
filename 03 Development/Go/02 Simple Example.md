# Simple Example

### Basic CLI Program Using `os.Args`

```go
package main

import (
	"fmt"
	"os"
)

func main() {
	// os.Args[0] is the program name; os.Args[1] is the first argument.
	fmt.Printf("Hello, %s\n", os.Args[1])
}
```

---

### Creating a Custom Package

Suppose your folder structure is:

```
practice/
├── hello/
│   └── hello.go
└── cmd/
    └── main.go
```

#### `hello/hello.go`

```go
package hello

import "fmt"

// Variable name comes before the type name.
func Say(name string) string {
	return fmt.Sprintf("Hello, %s!", name)
}
```

#### `cmd/main.go`

```go
package main

import (
	"fmt"
	"practice/hello" // Import your custom package
)

func main() {
	fmt.Println(hello.Say("Adarsh"))
}
```

### Common Error

If you run this without setting up a module, you'll see an error like:

```bash
main.go:6:2: package hello is not in std (/usr/lib/go-1.24/src/hello)
```

This happens because Go can't find the `hello` package—it assumes it's part of the standard library.

---

### Solution: Initialize a Go Module

From the root `practice/` directory:

```bash
go mod init practice
```

This creates a `go.mod` file and allows you to use the correct import path (`practice/hello`).

---

## Adding a Test File

Go has a built-in testing package. The conventions are:

- **Test files** should end with `_test.go`
    
- **Test functions** must start with `Test` and take `*testing.T` as a parameter
    

### Example: `hello/hello_test.go`

```go
package hello

import "testing"

func TestSay(t *testing.T) {
	result := Say("Adarsh")
	expected := "Hello, Adarsh!"

	if result != expected {
		t.Errorf("expected %q but got %q", expected, result)
	}
}
```

Run tests with:

```bash
go test ./...
```

---
