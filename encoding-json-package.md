# encoding/json Package

The `encoding/json` package provides functions for encoding and decoding JSON data. It is part of the standard library in Go.

***

### **1. `json.Marshal`**

Converts a Go object into a JSON byte slice.

```go
package main

import (
	"encoding/json"
	"fmt"
)

func main() {
	data := map[string]interface{}{
		"name": "Areen",
		"age":  16,
	}
	jsonData, err := json.Marshal(data)
	if err != nil {
		fmt.Println("Error:", err)
		return
	}
	fmt.Println(string(jsonData))
}
```

**Output:**

```json
{"name":"Areen","age":16}
```

***

### **2. `json.MarshalIndent`**

Converts a Go object into a JSON byte slice with indentation.

```go
package main

import (
	"encoding/json"
	"fmt"
)

func main() {
	data := map[string]interface{}{
		"name": "Areen",
		"age":  16,
	}
	jsonData, err := json.MarshalIndent(data, "", "  ")
	if err != nil {
		fmt.Println("Error:", err)
		return
	}
	fmt.Println(string(jsonData))
}
```

**Output:**

```json
{
  "name": "Areen",
  "age": 16
}
```

***

### **3. `json.Unmarshal`**

Parses JSON data into a Go object.

```go
package main

import (
	"encoding/json"
	"fmt"
)

func main() {
	jsonData := `{"name":"Areen","age":16}`
	var data map[string]interface{}
	err := json.Unmarshal([]byte(jsonData), &data)
	if err != nil {
		fmt.Println("Error:", err)
		return
	}
	fmt.Println(data)
}
```

**Output:**

```
map[age:16 name:Areen]
```

***

### **4. `json.NewDecoder` and `Decoder.Decode`**

Reads JSON data from an `io.Reader`.

```go
package main

import (
	"encoding/json"
	"fmt"
	"strings"
)

func main() {
	jsonData := `{"name":"Areen","age":16}`
	reader := strings.NewReader(jsonData)
	decoder := json.NewDecoder(reader)
	var data map[string]interface{}
	err := decoder.Decode(&data)
	if err != nil {
		fmt.Println("Error:", err)
		return
	}
	fmt.Println(data)
}
```

**Output:**

```
map[age:16 name:Areen]
```

***

### **5. `json.NewEncoder` and `Encoder.Encode`**

Writes a Go object as JSON to an `io.Writer`.

```go
package main

import (
	"encoding/json"
	"os"
)

func main() {
	data := map[string]interface{}{
		"name": "Areen",
		"age":  16,
	}
	encoder := json.NewEncoder(os.Stdout)
	err := encoder.Encode(data)
	if err != nil {
		fmt.Println("Error:", err)
	}
}
```

**Output:**

```json
{"name":"Areen","age":16}
```

***

### **6. `json.Valid`**

Checks if a byte slice contains valid JSON.

```go
package main

import (
	"encoding/json"
	"fmt"
)

func main() {
	jsonData := `{"name":"Areen","age":16}`
	if json.Valid([]byte(jsonData)) {
		fmt.Println("Valid JSON")
	} else {
		fmt.Println("Invalid JSON")
	}
}
```

**Output:**

```
Valid JSON
```

***

### **7. `json.RawMessage`**

Allows delaying or customizing JSON decoding.

```go
package main

import (
	"encoding/json"
	"fmt"
)

func main() {
	jsonData := `{"name":"Areen","details":{"age":16}}`
	var data map[string]json.RawMessage
	err := json.Unmarshal([]byte(jsonData), &data)
	if err != nil {
		fmt.Println("Error:", err)
		return
	}
	fmt.Println(string(data["details"]))
}
```

**Output:**

```
{"age":16}
```

***

These examples demonstrate how to use the `encoding/json` package effectively. Let me know if you'd like further explanations or additional use cases!
