---
icon: golang
---

# Get started

## basics of Go beginner level

in this page you will learn the basics  of go-lang&#x20;

### Variables are containers for storing data values

In Go, there are two ways to declare a variable

1. Use the var keyword, followed by variable name and type

```go
package main
import ("fmt")

var name = "John Doe" // Variable One

func main() {
    var fruit = "Apple" // Variable Two
    fmt.Println(name)
    fmt.Println(fruit)
}
```

2. Use the := sign, followed by the variable value

```go
package main
import ("fmt")

func main() {
    varOne := 100
    varTwo := 2
    fmt.Println(varOne)
    fmt.Println(varTwo)
}
```

Assigning Types + Type Inferred

```go
package main
import ("fmt")

func main() {
    var fruit string = "Mango" // type is string
    var user = "HuXn" // type is inferred
    number := 2 // type is inferred

    fmt.Println(fruit)
    fmt.Println(user)
    fmt.Println(number)
}
```

Go Multiple Variable Declaration

```go
package main
import ("fmt")

func main() {
    var one, two, three, four, five int = 1, 2, 3, 4, 5

    fmt.Println(one)
    fmt.Println(two)
    fmt.Println(three)
    fmt.Println(four)
}
```

Go Variable Declaration in a Block

```go
package main
import ("fmt")

func main() {
     var (
         num int
         number int = 1
         greetings string = "hello"
     )

    fmt.Println(num)
    fmt.Println(number)
    fmt.Println(greetings)
}
```

### Go Variable Naming Rules

1. A variable name must start with a letter or an underscore character (\_)
2. A variable name cannot start with a digit
3. A variable name can only contain alpha-numeric characters and underscores (a-z, A-Z, 0-9, and \_ )
4. Variable names are case-sensitive (age, Age and AGE are three different variables)
5. There is no limit on the length of the variable name
6. A variable name cannot contain spaces
7. The variable name cannot be any Go keywords

***

The const keyword declares the variable as "constant", which means that it is unchangeable and read-only.

```go

package main
import ("fmt")

const user = "admin" // cannot be changed

func main() {
    fmt.Println("admin")
}

```

Constant Rules

1. Constant names follow the same naming rules as variables
2. Constant names are usually written in uppercase letters
3. Constants can be declared both inside and outside of a function

***

### A boolean data-type can either be "TRUE" or "FALSE"

```go

package main

import "fmt"

func main() {
    isGolangPL := true
    isHtmlPL := false
    fmt.Println(isGolangPL)
    fmt.Println(isHtmlPL)
}
```

***

### Operators are used to perform operations on variables and values

#### Arithmetic Operators

1. Addition: The + operator adds two operands. For example, x+y.
2. Subtraction: The - operator subtracts two operands. For example, x-y.
3. Multiplication: The \* operator multiplies two operands. For example, x\*y.
4. Division: The / operator divides the first operand by the second. For example, x/y.
5. Modulus: Returns the division remainder
6. Increment: The ++ Increases the value of a variable by 1
7. Decrement: The -- Decreases the value of a variable by 1

```go

package main
import "fmt"

func main() {
	fmt.Println(2 + 2) // 4
	fmt.Println(2 - 2) // 0
	fmt.Println(2 * 2) // 4
	fmt.Println(2 / 2) // 1
	fmt.Println(2 % 2) // 0
}
```

#### Increment

```go

package main
import ("fmt")

func main() {
  x:= 10
  x++ // Add one new value (increment)
  fmt.Println(x)
}
```

#### Decrement

```go

package main
import ("fmt")

func main() {
  x:= 10
  x-- // Remove one new value (decrement)
  fmt.Println(x)
}
```

#### Assignment Operators

Assignment operators are used to assign values to variables.

| Operator | Example | Same As    |
| -------- | ------- | ---------- |
| =        | x = 5   | x = 5      |
| +=       | x += 3  | x = x + 3  |
| -=       | x -= 3  | x = x - 3  |
| \*=      | x \*= 3 | x = x \* 3 |
| /=       | x /= 3  | x = x / 3  |
| %=       | x %= 3  | x = x % 3  |

***

### String Data Type

The string data type is used to store a sequence of characters (text).

String values must be surrounded by double quotes

```go

    package main
    import "fmt"

    func main() {
        fmt.Println("I'm a String data type")
        fruit := "Orange"
        info := "Hello everyone my name is HuXn and i'm a Golang lover 😊"
        yt := "https://www.youtube.com/@huxnwebdev"
        fmt.Println(fruit)
        fmt.Println(info)
        fmt.Println(yt)
    }
```

***

### Comparison Operators

Comparison operators are used to compare two values

| Operator | Name                     | Example |
| -------- | ------------------------ | ------- |
| ==       | Equal to                 | x == y  |
| !=       | Not equal                | x != y  |
| >        | Greater than             | x > y   |
| <        | Less than                | x < y   |
| >=       | Greater than or equal to | x >= y  |
| <=       | Less than or equal to    | x <= y  |

```go

package main

import "fmt"

func main() {
	fmt.Println(2 > 2) // false
	fmt.Println(2 < 2) // false
	fmt.Println(2 >= 2) // true
	fmt.Println(2 <= 2) // true
	fmt.Println(2 == 2) // true
	fmt.Println(2 != 2) // false
}
```

***

### Logical Operators

Logical operators are used to determine the logic between variables or values.

1. Logical and (&&) Returns true if both statements are true
2. Logical or (||) Returns true if one statements is true
3. Logical not (!) Reverse the result, returns false if the result is true

```go

package main

import "fmt"

func main() {
	fmt.Println(true && true) // true
	fmt.Println(true && false) // false

	fmt.Println(true || true) // true
	fmt.Println(false || false) // false

	fmt.Println(!true) // false
	fmt.Println(!false) // true
}
```

***

### Go Conditions

Conditional statements allow us to control the structure of our program.

There are different ways by which we can control the flow of our program, (If, else if, else) are one of them.

(If, else if, else) statments allow us to make "decisions" while our program is running, They're also called (conditional statments) in programming.

```go
    // Sudo Syntax
     if condition { <code> }
     else if condition { <code> }
     else { <code> }
```

```go
// Actual Code
package main
import "fmt"

func main() {
	password := "12345678"
	if len(password) > 7 {
		fmt.Println("Valid Password")
	} else {
		fmt.Println("Invalid Password")
	}
}
```

***

### For Loop

A "For" Loop is used to repeat a specific block of code a known number of times.

For example, if we want to check the grade of every student in the class, we loop from 1 to that number. When the number of times is not known before hand, we use a "While" loop.

```go
// Sudo Syntax
for initialExpression; condition; increment { <code> }
```

```go
package main
import ("fmt")

func main() {
  for i:=0; i < 5; i++ {
    fmt.Println(i)
  }
}
```

### The continue Statement

The continue statement is used to skip one or more iterations in the loop. It then continues with the next iteration in the loop.

```go
package main
import ("fmt")

func main() {
  for i:=0; i < 5; i++ {
    if i == 3 {
      continue
    }
   fmt.Println(i)
  }
}
```

#### The break Statement

The break statement is used to break/terminate the loop execution.

```go
package main
import ("fmt")

func main() {
  for i:=0; i < 5; i++ {
    if i == 3 {
      break
    }
   fmt.Println(i)
  }
}
```

#### Nested Loops

Loop inside other loop is known as Nested Loop.

```go
package main

import (
	"fmt"
)

func main() {
	for i := 0; i < 20; i++ {
		fmt.Println("-----OUTER------", i)
		for j := 0; j < 10; j++ {
			fmt.Println("-----INNER------", j)
		}
	}
}

```

***

### While Loop

Unlike other programming languages, Go doesn't have a dedicated keyword for a while loop. However, we can use the for loop to perform the functionality of a while loop.

```go
// Program to print numbers between 0 and 10
package main
import ("fmt")

func main() {
  number := 0

  for number <= 10 {
    fmt.Println(number)
    number++
  }
}
```

***

### The switch Statement

The switch statement allows us to execute one code block among many alternatives.

```go
package main
import ("fmt")

func main() {
  day := 8

  switch day {
  case 1:
    fmt.Println("Monday")
  case 2:
    fmt.Println("Tuesday")
  case 3:
    fmt.Println("Wednesday")
  case 4:
    fmt.Println("Thursday")
  case 5:
    fmt.Println("Friday")
  case 6:
    fmt.Println("Saturday")
  case 7:
    fmt.Println("Sunday")
  default:
    fmt.Println("Not a weekday")
  }
}
```

***

### Arrays

Arrays is a data structure which is use to store multiple values of the same type in a single variable, instead of declaring separate variables for each value.

Arrays are 0 index based.

```go
package main
import ("fmt")

func main() {
  var arr1 = [3]int{1,2,3}
  arr2 := [5]int{4,5,6,7,8}

  fmt.Println(arr1)
  fmt.Println(arr2)
}
```

***

### Slices

Slices are also used to store multiple values of the same type in a single variable, however unlike arrays, the length of a slice can grow and shrink as you see fit.

There are several ways to create a slice 👇

1. Using the \[]datatype{values} format
2. Create a slice from an array
3. Using the make() function

```go
// name := []datatype{values}
// name := []int{}

package main
import ("fmt")

func main() {
  myslice1 := []int{}
  fmt.Println(len(myslice1))
  fmt.Println(cap(myslice1))
  fmt.Println(myslice1)

  myslice2 := []string{"Go", "Slices", "Are", "Powerful"}
  fmt.Println(len(myslice2))
  fmt.Println(cap(myslice2))
  fmt.Println(myslice2)
}
```

### Make() Method

The make function will create a zeroed array and return a slice referencing an array. This is a great way to create a dynamically sized array. To create a slice using the make function, we need to specify three arguments: type, length and the capacity.

```go
package main
import "fmt"
func main() {
    slice := make([]string, 3, 5)
    fmt.Println("Length", len(slice))
    fmt.Println("Capacity", cap(slice))
    fmt.Println(slice)
}
```

***

### Maps

Maps are a data structure which allow us to store data values in key:value pairs.

A map is an unordered and changeable collection that does not allow duplicates.

The default value of a map is nil.

```go
userInfo := map[string]int{
		"huxn": 17,
		"alex": 18,
		"john": 27,
	}

	fmt.Println(userInfo)
	userInfo["jordan"] = 15
	fmt.Println(userInfo["huxn"])
	fmt.Println(userInfo["alex"])
	fmt.Println(userInfo["john"])
```

***

### Structs (Structures)

A struct is used to create a collection of members of different data types, into a single variable.

```go
package main
import ("fmt")

type Person struct {
  name string
  age int
  job string
  salary int
}

func main() {
  var userOne Person

    userOne.name = "HuXn"
    userOne.age = 18
    userOne.job = "Programmer"
    userOne.salary = 40000
    fmt.Println(userOne)
    fmt.Println("My name is", userOne.name, "I'm", userOne.age, "Years old", "My Profession is", userOne.job, "My salary is", userOne.salary)
}
```
