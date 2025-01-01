---
icon: golang
---

# Intermediate Go

### Functions

A function is a block of statements that can be used repeatedly in a program.

Functions are not executed immediately. They are "saved for later use", and will be executed when they are called.

```go
package main
import "fmt"

// My Own Function
func printName(username string) {
    fmt.Println(username)
}

func main() {
    printName("HuXn")
}
```

***

### Function Expression

When we store a function inside a "variable" that function is known as Function Expression.

```go
package main

import "fmt"

func main() {
	add := func(num1 int, num2 int) int {
		return num1 + num2
	}

	res := add(10, 20)
	fmt.Println(res)
}

```

***

### Methods

A method is a function associated with a particular type. It is a way to define behavior for a specific type. In Go, methods are declared with a receiver, which is a special type of parameter that appears in the method signature. The receiver indicates on which type the method operates.

```go
package main

import "fmt"

// Define a type named "Person"
type Person struct {
    FirstName string
    LastName  string
}

// Define a method named "FullName" for the type "Person"
func (p Person) FullName() string {
    return p.FirstName + " " + p.LastName
}

func main() {
    // Create a Person instance
    person := Person{FirstName: "John", LastName: "Doe"}

    // Call the method on the Person instance
    fullName := person.FullName()

    // Print the result
    fmt.Println("Full Name:", fullName)
}


```

***

### Callback Functions

If a function is passed as an argument to another function, then such types of functions are known as a Higher-Order function. This passing function as an argument is also known as a callback function or first-class function in the Go language.

```go
package main
import "fmt"

func addName(name string, callback func(string)) {
	callback(name)
}

func main() {
	addName("HuXn", func(nm string) {
		fmt.Printf("hi may name is %v \n", nm)
	})
}
```

***

### Defer Keyword

The defer keyword is used to delay the execution of a function or a statement until the nearby function returns. In simple words, defer will move the execution of the statement to the very end inside a function.

```go
package main
import "fmt"

func greet() {
    defer fmt.Println("World")
    fmt.Println("Hello")
}

func main() {
 greet()
}
```

***

### Scope

Think of scope as the visibility or accessibility of things (like variables or functions) in your code. It's like where things are known or can be used.

1. Block Scope

Imagine your code as a series of blocks, like paragraphs in a story.

Variables and functions created inside a block are known only within that block.

```go
func main() {
    // Inside main's block
    var x int = 10
    fmt.Println(x)  // Can use x here

    if true {
        // Inside if's block
        var y int = 20
        fmt.Println(y)  // Can use y here
    }

    // Can't use y here, it's outside its block
}
```

2. Function Scope

Functions have their own scope. Variables defined inside a function are known only within that function.

```go
func myFunction() {
    // Inside myFunction's block
    var z int = 30
    fmt.Println(z)  // Can use z here
}

// Can't use z here, it's outside myFunction's block
```

3. Package Scope

Variables and functions defined at the top level of a package have a wider scope.

They can be used across multiple files within the same package.

```go
package main

// Outside any function, package scope
var globalVariable int = 50

func main() {
    // Can use globalVariable here
}
```

***

### Pointers

A pointer in Go is a variable that stores the memory address of another variable. By using pointers, you can indirectly access and modify the value of the variable whose address is stored in the pointer.

You can create a pointer using the \* (asterisk) symbol.

The & (ampersand) symbol is used to obtain the memory address of a variable

```go
package main

import "fmt"

func main() {
    // Declare a variable
    x := 42

    // Create a pointer that stores the memory address of x
    var pointerToX *int = &x

    // Print the value and memory address of x
    fmt.Println("Value of x:", x)
    fmt.Println("Memory address of x:", &x)

    // Print the value and memory address stored in the pointer
    fmt.Println("Value pointed to by pointerToX:", *pointerToX)
    fmt.Println("Memory address stored in pointerToX:", pointerToX)
}

```

***

### panic()

Similar to exceptions raised at runtime when an error is encountered. panic() is either raised by the program itself when an unexpected error occurs or the programmer throws the exception on purpose for handling particular errors.

```go
package main

func employee(name *string, age int){
  if age > 65{
    panic("Age cannot be greater than retirement age")
  }

}

func main() {
  empName := "Samia"
  age := 75
  employee(&empName, age)
}
```
