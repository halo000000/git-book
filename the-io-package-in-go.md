# The io package in Go

1.  **`io.Read()`**\
    Reads data from a source (like a file or network connection) into a byte slice.

    ```go
    n, err := io.Read(p []byte)
    ```
2.  **`io.ReadAtLeast()`**\
    Reads at least the specified number of bytes from a source.

    ```go
    n, err := io.ReadAtLeast(r io.Reader, p []byte, min int)
    ```
3.  **`io.ReadFull()`**\
    Reads exactly the number of bytes specified by the length of the provided byte slice.

    ```go
    n, err := io.ReadFull(r io.Reader, p []byte)
    ```
4.  **`io.Write()`**\
    Writes data from a byte slice to a destination.

    ```go
    n, err := io.Write(p []byte)
    ```
5.  **`io.Copy()`**\
    Copies data from a source (reader) to a destination (writer) until EOF.

    ```go
    n, err := io.Copy(dst io.Writer, src io.Reader)
    ```
6.  **`io.CopyN()`**\
    Copies exactly `n` bytes from the reader to the writer.

    ```go
    n, err := io.CopyN(dst io.Writer, src io.Reader, n int64)
    ```
7.  **`io.TeeReader()`**\
    Creates a reader that reads from the underlying reader and writes to the writer.

    ```go
    tee := io.TeeReader(r io.Reader, w io.Writer)
    ```
8.  **`io.MultiReader()`**\
    Combines multiple readers into a single reader that reads from each of them sequentially.

    ```go
    r := io.MultiReader(r1, r2)
    ```
9.  **`io.MultiWriter()`**\
    Combines multiple writers into a single writer that writes to all of them.

    ```go
    w := io.MultiWriter(w1, w2)
    ```
10. **`io.Discard`**\
    A `Writer` that discards all data written to it. Useful for ignoring output.

```go
io.Discard.Write(p []byte)
```

These functions are widely used for handling input/output operations efficiently in Go, especially when working with streams, files, or network connections.
