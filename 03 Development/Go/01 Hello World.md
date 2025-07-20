# Hello World

## Go Playground — [Link](https://go.dev/play/)

A browser-based environment provided by the Go team to write, run, and share simple Go programs.

### Playground Limitations

The Go Playground has the following constraints:

- Only allows output to `stdout` and `stderr`
    
- No support for file I/O
    
- No access to the network (sockets, APIs, etc.)
    
- Cannot run a persistent web server
    

These restrictions exist for **security and resource control**.

---

### Basic Hello World Program

```go
// Go is a modular language — code can be split across multiple files.
// The main function must reside in the 'main' package.
package main

// Import any required packages.
// 'fmt' is used here for formatted I/O.
import "fmt"

// main function is the entry point of the program.
func main() {
	fmt.Println("hello, world")
}
```

---

### Running a Go Program

To run a program from the terminal:

```bash
go run .
```

- The dot (`.`) tells Go to compile and run the current directory's files (typically files ending with `.go`).
    

---
