---
icon: rabbit-running
---

# FastHTTP

## Beginner's Tutorial on FastHTTP in Go

FastHTTP is a high-performance HTTP library for Go, designed to be faster and more efficient than the standard `net/http` package. It is widely used in scenarios where speed and low resource usage are critical. However, it has a slightly different API compared to `net/http`, which requires some learning.

This tutorial will guide you through the basics of using FastHTTP, complete with examples to help you get started.

***

## **Why FastHTTP?**

* **Speed:** Optimized for high performance and low resource consumption.
* **Low Memory Usage:** Focuses on reducing memory allocations.
* **Concurrency:** Built for handling high levels of concurrent HTTP requests.

However, keep in mind that it is not compatible with `net/http`, so existing `net/http` middleware and libraries cannot be reused directly.

***

## **Installing FastHTTP**

To install FastHTTP, use:

```bash
go get -u github.com/valyala/fasthttp
```

***

## **Basic HTTP Server**

Let’s start by creating a basic HTTP server using FastHTTP.

### **Example 1: Simple HTTP Server**

```go
package main

import (
    "github.com/valyala/fasthttp"
)

func main() {
    // Define the request handler
    requestHandler := func(ctx *fasthttp.RequestCtx) {
        switch string(ctx.Path()) {
        case "/":
            ctx.WriteString("Welcome to FastHTTP!") // Sends a response
        case "/hello":
            ctx.WriteString("Hello, World!")
        default:
            ctx.Error("Unsupported path", fasthttp.StatusNotFound)
        }
    }

    // Start the server
    if err := fasthttp.ListenAndServe(":8080", requestHandler); err != nil {
        panic(err)
    }
}
```

### **How it Works:**

* The `ListenAndServe` function starts the server on port `8080`.
* The `ctx` object (of type `*fasthttp.RequestCtx`) is used to read the request and write the response.

***

## **Handling Query Parameters**

FastHTTP provides efficient methods to parse query parameters.

### **Example 2: Parsing Query Parameters**

```go
package main

import (
    "github.com/valyala/fasthttp"
)

func main() {
    requestHandler := func(ctx *fasthttp.RequestCtx) {
        name := string(ctx.QueryArgs().Peek("name")) // Extract the 'name' query parameter
        if name == "" {
            name = "Guest"
        }
        ctx.WriteString("Hello, " + name + "!")
    }

    if err := fasthttp.ListenAndServe(":8080", requestHandler); err != nil {
        panic(err)
    }
}
```

### **How it Works:**

* `ctx.QueryArgs().Peek("key")` retrieves the value of a query parameter.

For example, visiting `http://localhost:8080/?name=Areen` will respond with `Hello, Areen!`.

***

## **Serving Static Files**

FastHTTP can also serve static files efficiently.

### **Example 3: Static File Server**

```go
package main

import (
    "github.com/valyala/fasthttp"
)

func main() {
    fs := &fasthttp.FS{
        Root:               "./static", // Directory containing static files
        IndexNames:         []string{"index.html"},
        GenerateIndexPages: true,       // Automatically generate index pages for directories
    }

    if err := fasthttp.ListenAndServe(":8080", fs.NewRequestHandler()); err != nil {
        panic(err)
    }
}
```

### **How it Works:**

* Place your static files in the `./static` directory.
* FastHTTP will automatically serve them when accessed through the browser.

***

## **HTTP Client with FastHTTP**

FastHTTP also includes a high-performance HTTP client.

### **Example 4: Sending HTTP Requests**

```go
package main

import (
    "fmt"
    "github.com/valyala/fasthttp"
)

func main() {
    statusCode, body, err := fasthttp.Get(nil, "https://httpbin.org/get")
    if err != nil {
        panic(err)
    }

    fmt.Printf("Status Code: %d\n", statusCode)
    fmt.Printf("Body: %s\n", string(body))
}
```

### **How it Works:**

* `fasthttp.Get` sends a GET request to the specified URL.
* It returns the status code, response body, and an error if any.

***

## **Using Middleware**

FastHTTP does not natively support middleware like `net/http`, but you can implement your own.

### **Example 5: Middleware Implementation**

```go
package main

import (
    "github.com/valyala/fasthttp"
)

func loggingMiddleware(next fasthttp.RequestHandler) fasthttp.RequestHandler {
    return func(ctx *fasthttp.RequestCtx) {
        println("Request received for:", string(ctx.Path()))
        next(ctx)
    }
}

func mainHandler(ctx *fasthttp.RequestCtx) {
    ctx.WriteString("Hello from the main handler!")
}

func main() {
    if err := fasthttp.ListenAndServe(":8080", loggingMiddleware(mainHandler)); err != nil {
        panic(err)
    }
}
```

### **How it Works:**

* The `loggingMiddleware` function wraps the main handler, allowing you to add custom logic (e.g., logging) before and after the main handler executes.

***

## **Functions in FastHTTP**

Below is a table summarizing key functions in the FastHTTP package:

| **Function**             | **Parameters**                                 | **Description**                                           |
| ------------------------ | ---------------------------------------------- | --------------------------------------------------------- |
| `ListenAndServe`         | `addr string, handler fasthttp.RequestHandler` | Starts an HTTP server on the given address.               |
| `Get`                    | `dst *[]byte, url string`                      | Sends an HTTP GET request to the specified URL.           |
| `Post`                   | `dst *[]byte, url string, body string`         | Sends an HTTP POST request with the provided body.        |
| `RequestCtx.Write`       | `data []byte`                                  | Writes raw bytes to the response body.                    |
| `RequestCtx.WriteString` | `s string`                                     | Writes a string to the response body.                     |
| `RequestCtx.Error`       | `msg string, statusCode int`                   | Sends an error response with a custom message and status. |
| `QueryArgs.Peek`         | `key string`                                   | Retrieves the value of a query parameter.                 |
| `FS.NewRequestHandler`   | `none`                                         | Creates a request handler for serving static files.       |
| `AcquireRequest`         | `none`                                         | Creates a reusable HTTP request object.                   |
| `AcquireResponse`        | `none`                                         | Creates a reusable HTTP response object.                  |

***

## **Best Practices with FastHTTP**

1. **Reuse Buffers:** Use `fasthttp.AcquireRequest` and `fasthttp.AcquireResponse` for efficient request and response handling.
2. **Connection Reuse:** Use `fasthttp.Client` for multiple requests to the same server.
3. **Concurrency:** Leverage goroutines to handle multiple requests concurrently.

***

## **Conclusion**

FastHTTP is a powerful library for building high-performance web applications in Go. While it has a steeper learning curve compared to `net/http`, its efficiency makes it an excellent choice for performance-critical applications.

