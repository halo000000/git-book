---
icon: html5
---

# html/template package

## HTML Templates in Go

The `html/template` package provides a simple and powerful way to generate HTML output. It is part of the standard library in Go.

### **1. `template.New`**

Creates a new, named template.

```go
package main

import (
	"html/template"
	"os"
)

func main() {
	t := template.New("example")
	t, _ = t.Parse("Hello, {{.}}!")
	t.Execute(os.Stdout, "World")
}
```

**Output:**

```
Hello, World!
```

***

### **2. `template.Parse`**

Parses a string containing a template.

```go
package main

import (
	"html/template"
	"os"
)

func main() {
	t, _ := template.New("example").Parse("Hello, {{.}}!")
	t.Execute(os.Stdout, "World")
}
```

**Output:**

```
Hello, World!
```

***

### **3. `template.ParseFiles`**

Parses template definitions from one or more files.

```go
package main

import (
	"html/template"
	"os"
)

func main() {
	t, _ := template.ParseFiles("example.html")
	t.Execute(os.Stdout, "World")
}
```

**example.html:**

```html
Hello, {{.}}!
```

**Output:**

```
Hello, World!
```

***

### **4. `template.ParseGlob`**

Parses template definitions from files matching a glob pattern.

```go
package main

import (
	"html/template"
	"os"
)

func main() {
	t, _ := template.ParseGlob("templates/*.html")
	t.ExecuteTemplate(os.Stdout, "example.html", "World")
}
```

**templates/example.html:**

```html
Hello, {{.}}!
```

**Output:**

```
Hello, World!
```

***

### **5. `template.Execute`**

Executes a template and writes the output to an `io.Writer`.

```go
package main

import (
	"html/template"
	"os"
)

func main() {
	t, _ := template.New("example").Parse("Hello, {{.}}!")
	t.Execute(os.Stdout, "World")
}
```

**Output:**

```
Hello, World!
```

***

### **6. `template.ExecuteTemplate`**

Executes a specific template from a template set.

```go
package main

import (
	"html/template"
	"os"
)

func main() {
	t, _ := template.New("example").Parse("Hello, {{.}}!")
	t.ExecuteTemplate(os.Stdout, "example", "World")
}
```

**Output:**

```
Hello, World!
```

***

### **7. `template.Funcs`**

Adds custom functions to a template.

```go
package main

import (
	"html/template"
	"os"
	"strings"
)

func main() {
	funcMap := template.FuncMap{
		"toUpper": strings.ToUpper,
	}
	t := template.New("example").Funcs(funcMap)
	t, _ = t.Parse("Hello, {{. | toUpper}}!")
	t.Execute(os.Stdout, "world")
}
```

**Output:**

```
Hello, WORLD!
```

***

### **8. `template.Clone`**

Creates a copy of an existing template.

```go
package main

import (
	"html/template"
	"os"
)

func main() {
	t := template.New("example")
	t, _ = t.Parse("Hello, {{.}}!")
	clone, _ := t.Clone()
	clone.Execute(os.Stdout, "World")
}
```

**Output:**

```
Hello, World!
```

***

### **9. `template.Must`**

Wraps a function that returns a `*Template` and an error, panicking if there's an error.

```go
package main

import (
	"html/template"
	"os"
)

func main() {
	t := template.Must(template.New("example").Parse("Hello, {{.}}!"))
	t.Execute(os.Stdout, "World")
}
```

**Output:**

```
Hello, World!
```

***

These examples cover the key functions in the `html/template` package. Let me know if you'd like additional details or more advanced examples!

***

***

## Complete Example with Error Handling\*\*

Ensures template parsing errors are handled at initialization.

```go
package main

import (
	"html/template"
	"net/http"
)

func main() {
	t := template.Must(template.New("example").ParseFiles("example.html"))

	http.HandleFunc("/", func(w http.ResponseWriter, r *http.Request) {
		t.Execute(w, "World")
	})
	http.ListenAndServe(":8080", nil)
}
```

In Go's `html/template` package, there are several types of placeholders and actions you can use inside your HTML template to manipulate data, control flow, and format content. Below is an example template that demonstrates many of these actions, along with an explanation of what they do.

### Summary of Template Actions:

* **`{{.FieldName}}`**: Insert data from the context.
* **`{{if condition}}...{{else}}...{{end}}`**: Conditional rendering based on a value.
* **`{{range .Slice}}...{{end}}`**: Loop through a slice or array.
* **`{{with .Field}}...{{end}}`**: Set a new context and work with a specific field.
* **`{{define "name"}}...{{end}}`**: Define a reusable sub-template.
* **`{{template "name" .}}`**: Render a defined sub-template.

***

### Template Example with Various Placeholders

**`index.html`**:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>{{.Title}}</title>
</head>
<body>
    <h1>{{.Header}}</h1>
    <p>{{.Message}}</p>
    
    <p><strong>Uppercase Title:</strong> {{.Title | upper}}</p> <!-- Custom function applied -->

    <h2>Conditional Example</h2>
    {{if .IsAdmin}}
        <p>You have admin privileges!</p>
    {{else}}
        <p>You are a regular user.</p>
    {{end}}

    <h2>Loop Example</h2>
    <ul>
    {{range .Items}}
        <li>{{.}}</li>
    {{end}}
    </ul>

    <h2>With Example</h2>
    {{with .Contact}}
        <p>Email: {{.Email}}</p>
        <p>Phone: {{.Phone}}</p>
    {{end}}

    <h2>Template Action Example</h2>
    {{define "footer"}}
        <footer>
            <p>Footer content goes here</p>
        </footer>
    {{end}}

    {{template "footer" .}} <!-- Includes the footer template -->
</body>
</html>
```

### Explanation of the Template Placeholders

1. **`{{.Title}}`**:
   * Placeholder that inserts the value of the `Title` field from the data passed to the template. The dot (`.`) represents the current context or data passed in.
2. **`{{if .IsAdmin}}...{{else}}...{{end}}`**:
   * Conditional statement to check if `IsAdmin` is `true`. If it is, the first block (`<p>You have admin privileges!</p>`) is rendered. If not, the block under `else` is rendered.
3. **`{{range .Items}}...{{end}}`**:
   * Loops over the `Items` field, which is expected to be a slice or array. For each item, the block is executed, and the current item is inserted where `{{.}}` is placed. It creates a list (`<li>`) for each item.
4. **`{{with .Contact}}...{{end}}`**:
   * The `with` action sets the context to `Contact` temporarily. Inside the block, you can refer to fields of `Contact` directly (e.g., `{{.Email}}`). This is useful when you want to extract and use sub-fields in a structured object.
5. **`{{define "footer"}}...{{end}}`** and **`{{template "footer" .}}`**:
   * `define` creates a named template (`footer` in this case) that can be reused later with `template`. The content inside `{{define "footer"}}` is the footer content, and `{{template "footer" .}}` will insert that defined template into the page.
6.  **`{{.Title | upper}}`**:

    * This applies a custom function (like `upper` to convert text to uppercase). You would need to define the `upper` function when parsing the template in Go using `Funcs` method.

    Example in Go:

    ```go
    tmpl, err := template.New("index.html").Funcs(template.FuncMap{
        "upper": strings.ToUpper,
    }).ParseFiles("index.html")
    ```

### Example Data Structure in Go

Here's the Go data structure that would work with this template:

```go
package main

import (
    "html/template"
    "log"
    "net/http"
    "strings"
)

type Contact struct {
    Email string
    Phone string
}

type PageData struct {
    Title    string
    Header   string
    Message  string
    IsAdmin  bool
    Items    []string
    Contact  Contact
}

func handler(w http.ResponseWriter, r *http.Request) {
    data := PageData{
        Title:   "Go Templates Demo",
        Header:  "Welcome to Go Templates!",
        Message: "This page demonstrates various template features.",
        IsAdmin: true,
        Items:   []string{"Item 1", "Item 2", "Item 3"},
        Contact: Contact{
            Email: "contact@example.com",
            Phone: "123-456-7890",
        },
    }

    tmpl, err := template.New("index.html").Funcs(template.FuncMap{
        "upper": strings.ToUpper,
    }).ParseFiles("index.html")
    if err != nil {
        log.Fatal(err)
    }

    err = tmpl.Execute(w, data)
    if err != nil {
        log.Fatal(err)
    }
}

func main() {
    http.HandleFunc("/", handler)
    log.Fatal(http.ListenAndServe(":8080", nil))
}
```
