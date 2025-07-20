# Basic Types

## Keywords & Symbols

Go has only **25 keywords** (you cannot use them as identifiers):

```
break       case        chan        const       continue  
default     defer       else        fallthrough for  
func        go          goto        if          import  
interface   map         package     range       return  
select      struct      switch      type        var
```

Go also uses various **operators and symbols**:

### Arithmetic & Bitwise

```
+   -   *   /   %  
&   |   ^   &^  
<<  >>  
```

### Comparison

```
==  !=  <  <=  >  >=
```

### Assignment & Compound Assignment

```
=   :=  
+=  -=  *=  /=  %=  
&=  |=  ^=  <<=  >>=  &^=
```

### Other Symbols

```
( )   [ ]   { }  
,     .     ...  
;     :
```

---

## Predeclared Identifiers

In Go, when you write:

```go
a := 2
```

The variable `a` is **directly stored in memory**, without the abstraction of an interpreter like in Python.  
This low-level control contributes to **Go’s high performance**.

---

## Numeric Types

### Integers

Go uses **machine-native word size** for `int` and `uint`:

- **64-bit** on most desktops/laptops
    
- **32-bit** on 32-bit systems (e.g., Raspberry Pi)
    

|Signed|Unsigned|
|---|---|
|int|uint|
|int64|uint64|
|int32|uint32|
|int16|uint16|
|int8|uint8|

> `byte` is an alias for `uint8`  
> `rune` is an alias for `int32` (used for Unicode characters)

---

### Floating Point & Complex

- `float32`, `float64`: for real numbers
    
- `complex64`, `complex128`: for imaginary numbers
    

> ⚠️ **Do not use floating point types for currency calculations**. Use specialized packages like `github.com/Rhymond/go-money`.

---

## Declaration & Type Inference

```go
var a int          // explicitly typed
var (
	b = 2        // inferred as int
	f = 2.01     // inferred as float64
)
```

Short variable declarations (only inside functions):

```go
c := 2
```

---

### Example: Type Inference

```go
package main

import "fmt"

func main() {
	a := 2
	b := 2.1

	fmt.Printf("a: %T %v\n", a, a)
	fmt.Printf("b: %T %v\n", b, b)
}
```

**Output:**

```
a: int 2
b: float64 2.1
```

---

### Type Conversion

```go
a = b // ❌ Compilation error: cannot assign float64 to int

a = int(b) // ✅ Explicit conversion
```

---

## Special Simple Types

- `bool`: holds `true` or `false`
    
    - **Not** implicitly convertible to/from integers
        
- `error`: built-in interface with a single method `Error() string`
    
    - Used to represent errors; can be `nil` or non-`nil`
        
- `pointers`: hold memory addresses
    
    - May be `nil`
        
    - No pointer arithmetic (except through `unsafe` package)
        

---

## Initialization Defaults

All variables are automatically initialized to **zero values**:

|Type Category|Default Value|
|---|---|
|Integers|`0`|
|Floats|`0.0`|
|Complex|`0 + 0i`|
|Boolean|`false`|
|Strings|`""`|
|Pointers|`nil`|
|Slices|`nil`|
|Maps|`nil`|
|Channels|`nil`|
|Functions|`nil`|
|Interfaces|`nil`|

For composite types (structs, arrays), each field is initialized to its zero value.

---

## Constants

Only numbers, strings, and booleans can be constant.  
Constants must be assigned **at compile time**.

```go
const (
	a = 1             // int
	b = 2 * 1024      // 2048
	c = b << 3        // 16384

	g uint8 = 0x07    // 7
	h uint8 = g & 0x03 // 3

	s = "a string"
	t = len(s)        // 8 — valid at compile time
	// u = s[2:]      // ❌ invalid in constant context
)
```

---

## The `for` Loop

Go has only one looping construct — `for`.

```go
package main

import (
	"fmt"
	"os"
)

func main() {
	var sum float64
	var count int

	for {
		var val float64

		_, err := fmt.Fscanln(os.Stdin, &val)

		if err != nil {
			break
		}

		sum += val
		count++
	}

	fmt.Println("Sum:", sum)
	fmt.Println("Count:", count)
}
```

> `++count` is **not valid** in Go — use `count++`.

---

## Comments

- Single-line: `// like this`
    
- Multi-line:
    
    ```go
    /* this is 
       a multi-line comment */
    ```
    

---
