# The godotenv package

The `godotenv` package in Go is commonly used for loading environment variables from a `.env` file into the application's environment. Here are the most used functions of the `godotenv` package:

1.  **`godotenv.Load()`**

    * This function loads environment variables from a `.env` file into the process environment. It returns an error if it fails to load the file.

    ```go
    err := godotenv.Load()
    if err != nil {
        log.Fatal("Error loading .env file")
    }
    ```
2.  **`godotenv.Load(filenames ...string)`**

    * This function allows you to specify custom file names instead of just `.env`. You can pass multiple filenames, and it will load them in the given order.

    ```go
    err := godotenv.Load(".env.local", ".env")
    if err != nil {
        log.Fatal("Error loading .env files")
    }
    ```
3.  **`godotenv.Overload()`**

    * Similar to `Load()`, but it will overwrite any existing environment variables with those from the `.env` file.

    ```go
    err := godotenv.Overload()
    if err != nil {
        log.Fatal("Error loading .env file and overwriting existing environment variables")
    }
    ```
4.  **`godotenv.Overload(filenames ...string)`**

    * This is the overloaded version that accepts custom filenames to load environment variables from specific files while overwriting existing variables.

    ```go
    err := godotenv.Overload(".env.local", ".env")
    if err != nil {
        log.Fatal("Error loading .env files with overwrite")
    }
    ```
5.  **`godotenv.Parse()`**

    * This function is used to manually parse environment variables from a `.env` file into a map. It's useful when you want to load the contents of a file without actually modifying the environment.

    ```go
    envs, err := godotenv.Parse(".env")
    if err != nil {
        log.Fatal("Error parsing .env file")
    }
    fmt.Println(envs) // Map of environment variables
    ```
6.  **`godotenv.MustLoad()`**

    * This function loads environment variables from a `.env` file, but it panics if the file can't be loaded, making it less suitable for situations where you need error handling.

    ```go
    godotenv.MustLoad() // Panics if the .env file is not found
    ```

These functions allow you to configure and manage environment variables in a Go application seamlessly, ensuring they are loaded and accessible throughout the program.
