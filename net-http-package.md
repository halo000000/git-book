---
icon: globe-pointer
---

# net/http Package



## Basic Use of Go's net/http Package

The `net/http` package in Go is a powerful and versatile library for building HTTP clients and servers. This document provides a basic introduction to its usage, with short explanations and simple code examples.

## 1. Setting Up an HTTP Server

To start an HTTP server, you can use the `http.HandleFunc` function to define routes and their corresponding handler functions.

### Example: Basic HTTP Server

```go
package main

import (
    "fmt"
    "net/http"
)

func helloHandler(w http.ResponseWriter, r *http.Request) {
    fmt.Fprintf(w, "Hello, World!")
}

func main() {
    http.HandleFunc("/hello", helloHandler) // Route definition

    fmt.Println("Starting server on :8080...")
    if err := http.ListenAndServe(":8080", nil); err != nil {
        fmt.Println("Error starting server:", err)
    }
}
```

### Explanation

1. `http.HandleFunc`: Maps the `"/hello"` route to the `helloHandler` function.
2. `http.ListenAndServe`: Starts the server on port 8080.
3. `helloHandler`: Writes "Hello, World!" as the response.

Run the program and access `http://localhost:8080/hello` to see the message.

***

## patterns for matching routes

A pattern has three optional parts: `[METHOD ][HOST]/[PATH]`

Key rules:

* METHOD must be followed by space/tab if present
* No method = matches all methods
* GET matches both GET and HEAD
* No host = matches all hosts
* Paths can contain wildcards in two forms:
  * `{NAME}`: Matches one path segment
  * `{NAME...}`: Matches all remaining segments

Examples:

```
"/index.html"              // Matches exact path, any host/method
"GET /static/"            // Matches GET requests starting with /static/
"example.com/"           // Matches any request to example.com
"example.com/{$}"        // Matches exactly "/" on example.com
```

Path segments are unescaped before matching, so "/a%2Fb" is treated as "/a/b".

***

## 2. Making HTTP Requests

The `http` package includes tools for creating HTTP clients to send requests to other servers.

### Example: Making a GET Request

```go
package main

import (
    "fmt"
    "net/http"
    "io/ioutil"
)

func main() {
    response, err := http.Get("https://jsonplaceholder.typicode.com/posts/1")
    if err != nil {
        fmt.Println("Error making GET request:", err)
        return
    }
    defer response.Body.Close()

    body, err := ioutil.ReadAll(response.Body)
    if err != nil {
        fmt.Println("Error reading response body:", err)
        return
    }

    fmt.Println("Response:", string(body))
}
```

### Explanation

1. `http.Get`: Sends a GET request to the specified URL.
2. `response.Body`: Contains the response body, which is read using `ioutil.ReadAll`.
3. `defer response.Body.Close()`: Ensures the response body is closed after use.

***

## 3. Handling Query Parameters

Query parameters can be extracted using the `r.URL.Query` method.

### Example: Extract Query Parameters

```go
package main

import (
    "fmt"
    "net/http"
)

func queryHandler(w http.ResponseWriter, r *http.Request) {
    params := r.URL.Query()
    name := params.Get("name")
    if name == "" {
        name = "Guest"
    }
    fmt.Fprintf(w, "Hello, %s!", name)
}

func main() {
    http.HandleFunc("/greet", queryHandler)

    fmt.Println("Starting server on :8080...")
    http.ListenAndServe(":8080", nil)
}
```

### Explanation

1. `r.URL.Query()`: Parses query parameters into a map-like structure.
2. `params.Get("name")`: Retrieves the value of the `name` parameter.

Access `http://localhost:8080/greet?name=Areen` to see the greeting with your name.

***

## 4. Handling path Parameters

path parameters in Go using the `net/http` package&#x20;

you can get path parames with `r.PathValue("param-name")`

url example `http://localhost:8080/{user}/{post}/{id}`

```go
package main

import (
	"fmt"
	"net/http"
)

func main() {
	http.HandleFunc("/users/{id}", handler)
	http.ListenAndServe(":8080", nil)
}

func handler(w http.ResponseWriter, r *http.Request) {
	// you can get path parames with r.PathValue("param-name")
	id := r.PathValue("id")
	fmt.Printf("User ID: %s\n", id)
	fmt.Fprintf(w, "User ID: %s\n", id)
}

```

***

## 5. Using Custom Handlers

For more control, implement the `http.Handler` interface with a custom struct.

### Example: Custom Handler

```go
package main

import (
    "fmt"
    "net/http"
)

type myHandler struct{}

func (h *myHandler) ServeHTTP(w http.ResponseWriter, r *http.Request) {
    fmt.Fprintf(w, "Custom handler response!")
}

func main() {
    handler := &myHandler{}
    fmt.Println("Starting server on :8080...")
    http.ListenAndServe(":8080", handler)
}
```

### Explanation

1. `ServeHTTP`: Method required to implement the `http.Handler` interface.
2. Custom handler provides more flexibility in handling requests.

***

## 6. Middleware Example

Middleware allows pre- or post-processing of HTTP requests and responses.

### Example: Logging Middleware

```go
package main

import (
    "fmt"
    "net/http"
)

func loggingMiddleware(next http.Handler) http.Handler {
    return http.HandlerFunc(func(w http.ResponseWriter, r *http.Request) {
        fmt.Printf("%s %s\n", r.Method, r.URL.Path)
        next.ServeHTTP(w, r)
    })
}

func mainHandler(w http.ResponseWriter, r *http.Request) {
    fmt.Fprintf(w, "Welcome!")
}

func main() {
    mainHandler := http.HandlerFunc(mainHandler)
    http.Handle("/", loggingMiddleware(mainHandler))

    fmt.Println("Starting server on :8080...")
    http.ListenAndServe(":8080", nil)
}
```

### Explanation

1. Middleware wraps handlers to add functionality (e.g., logging).
2. `loggingMiddleware` prints the request method and path before passing it to the next handler.

***

This document covers basic functionality to help you get started with Go's `net/http` package. Explore further by combining these examples and creating more advanced HTTP applications!

Here’s a list of the most commonly used functions in Go’s `net/http` package, categorized by functionality:

***

### **Server-Side Functions**

1.  **`http.HandleFunc`**\
    Maps a route to a handler function.

    ```go
    http.HandleFunc("/path", handlerFunction)
    ```
2.  **`http.ListenAndServe`**\
    Starts an HTTP server on a specified address and port.

    ```go
    http.ListenAndServe(":8080", nil)
    ```
3.  **`http.Serve`**\
    Serves HTTP requests on a custom `net.Listener`.

    ```go
    http.Serve(listener, handler)
    ```
4.  **`http.ServeMux`**\
    A request multiplexer for handling routes.

    ```go
    mux := http.NewServeMux()
    mux.Handle("/path", handler)
    ```
5.  **`http.FileServer`**\
    Serves static files from a directory.

    ```go
    http.Handle("/static/", http.StripPrefix("/static/", http.FileServer(http.Dir("./static"))))
    ```

***

### **Client-Side Functions**

1.  **`http.Get`**\
    Sends an HTTP GET request and returns the response.

    ```go
    resp, err := http.Get("http://example.com")
    ```
2.  **`http.Post`**\
    Sends an HTTP POST request with a body.

    ```go
    resp, err := http.Post("http://example.com", "application/json", body)
    ```
3.  **`http.PostForm`**\
    Sends an HTTP POST request with form-encoded data.

    ```go
    resp, err := http.PostForm("http://example.com", url.Values{"key": {"value"}})
    ```
4.  **`http.NewRequest`**\
    Creates a new HTTP request with custom headers or methods.

    ```go
    req, err := http.NewRequest("GET", "http://example.com", nil)
    ```
5.  **`http.DefaultClient.Do`**\
    Executes a custom `http.Request`.

    ```go
    resp, err := http.DefaultClient.Do(req)
    ```

***

### **Request and Response Handling**

1.  **`http.Redirect`**\
    Redirects the client to a new URL.

    ```go
    http.Redirect(w, r, "http://new-url.com", http.StatusFound)
    ```
2.  **`http.Error`**\
    Sends an HTTP error response with a status code.

    ```go
    http.Error(w, "Something went wrong", http.StatusInternalServerError)
    ```
3.  **`http.NotFound`**\
    Sends a 404 Not Found response.

    ```go
    http.NotFound(w, r)
    ```
4.  **`http.ServeContent`**\
    Serves content with caching headers.

    ```go
    http.ServeContent(w, r, "filename", modTime, content)
    ```
5.  **`http.ServeFile`**\
    Serves a file directly to the client.

    ```go
    http.ServeFile(w, r, "./path/to/file")
    ```

***

### **Utilities**

1.  **`http.NewServeMux`**\
    Creates a new multiplexer for routing.

    ```go
    mux := http.NewServeMux()
    ```
2.  **`http.StripPrefix`**\
    Strips a prefix from a URL path before routing.

    ```go
    http.StripPrefix("/static/", handler)
    ```
3.  **`http.TimeoutHandler`**\
    Wraps a handler with a timeout.

    ```go
    http.TimeoutHandler(handler, 2*time.Second, "Request timed out")
    ```
4.  **`http.ParseForm`**\
    Parses form data from a request.

    ```go
    err := r.ParseForm()
    ```
5.  **`http.Header`**\
    Allows access to HTTP headers.

    ```go
    r.Header.Get("Content-Type")
    ```

***

These functions cover the most common use cases for creating HTTP servers, handling client requests, and making HTTP requests in Go.
