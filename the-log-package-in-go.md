# The log package in Go

The `log` package in Go provides basic logging functionality. Below are some of the most commonly used functions in the `log` package:

1. **`log.Print(v ...interface{})`**
   * Logs a message with the default log format (typically followed by a newline).
   *   Example:

       ```go
       log.Print("This is a log message")
       ```
2. **`log.Println(v ...interface{})`**
   * Logs a message with the default log format, followed by a newline.
   * It's similar to `Print` but automatically adds a newline.
   *   Example:

       ```go
       log.Println("This is a log message")
       ```
3. **`log.Printf(format string, v ...interface{})`**
   * Logs a formatted message, similar to `fmt.Printf`, with a default log format.
   *   Example:

       ```go
       log.Printf("User %s has logged in", username)
       ```
4. **`log.Fatal(v ...interface{})`**
   * Logs a message and then calls `os.Exit(1)` to terminate the program. It's used for fatal errors.
   *   Example:

       ```go
       if err != nil {
           log.Fatal("Error:", err)
       }
       ```
5. **`log.Fatalln(v ...interface{})`**
   * Similar to `log.Fatal`, but adds a newline at the end of the log message before calling `os.Exit(1)`.
   *   Example:

       ```go
       if err != nil {
           log.Fatalln("Fatal error:", err)
       }
       ```
6. **`log.Fatalf(format string, v ...interface{})`**
   * Logs a formatted message and then calls `os.Exit(1)`. It’s useful when you need to format the error message before exiting.
   *   Example:

       ```go
       log.Fatalf("Error: %v\n", err)
       ```
7. **`log.Panic(v ...interface{})`**
   * Logs a message and then calls `panic()`. It’s used for non-recoverable errors that need to be logged before panicking.
   *   Example:

       ```go
       if err != nil {
           log.Panic("Error:", err)
       }
       ```
8. **`log.Panicln(v ...interface{})`**
   * Similar to `log.Panic`, but adds a newline after the log message before calling `panic()`.
   *   Example:

       ```go
       log.Panicln("This is a panic message")
       ```
9. **`log.Panicf(format string, v ...interface{})`**
   * Similar to `log.Panic`, but with formatted output.
   *   Example:

       ```go
       log.Panicf("Something went wrong: %v", err)
       ```
10. **`log.SetFlags(flag int)`**
    * Sets the flags for the default logger. Common flags include `log.Ldate`, `log.Ltime`, `log.Lshortfile`, etc., which control the output format of log messages.
    *   Example:

        ```go
        log.SetFlags(log.Ldate | log.Ltime | log.Lshortfile)
        ```
11. **`log.SetPrefix(prefix string)`**
    * Sets a prefix to be included at the start of every log message.
    *   Example:

        ```go
        log.SetPrefix("[INFO] ")
        ```

These functions provide a simple interface for logging messages in Go applications.
