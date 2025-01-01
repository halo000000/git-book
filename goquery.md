---
icon: square-js
---

# GoQuery

## Introduction to GoQuery: A Beginner’s Guide

GoQuery is a powerful Go library inspired by jQuery, designed for web scraping and manipulation of HTML documents. It provides an easy-to-use API for traversing and manipulating HTML elements, making it an excellent choice for building web scrapers or data parsers in Go.

In this tutorial, we’ll cover the basics of GoQuery with practical examples.

***

### Installation

To use GoQuery, you need to install it first. Run the following command:

```sh
go get -u github.com/PuerkitoBio/goquery
```

Make sure your Go environment is set up correctly.

***

### Basic Usage

#### Importing GoQuery

Start by importing GoQuery and other essential packages:

```go
package main

import (
	"fmt"
	"log"
	"github.com/PuerkitoBio/goquery"
)
```

***

#### Example 1: Loading an HTML Document

Let’s load an HTML document from a URL and print its title:

```go
func main() {
	// Load the HTML document
	doc, err := goquery.NewDocument("https://example.com")
	if err != nil {
		log.Fatal(err)
	}

	// Find and print the title
	title := doc.Find("title").Text()
	fmt.Println("Page Title:", title)
}
```

**Explanation:**

* `goquery.NewDocument`: Fetches and parses the HTML from the provided URL.
* `Find`: Searches for elements matching the CSS selector.
* `Text`: Extracts the text content of the selected element.

***

#### Example 2: Extracting Links

Suppose you want to extract all the hyperlinks ( tags) from a webpage:

```go
func main() {
	doc, err := goquery.NewDocument("https://example.com")
	if err != nil {
		log.Fatal(err)
	}

	doc.Find("a").Each(func(index int, item *goquery.Selection) {
		href, exists := item.Attr("href")
		if exists {
			fmt.Printf("Link #%d: %s\n", index+1, href)
		}
	})
}
```

**Explanation:**

* `Each`: Iterates over each matched element.
* `Attr`: Retrieves the value of an attribute (e.g., `href`).

***

#### Example 3: Scraping Tables

You can scrape data from tables by targeting rows and cells:

```go
func main() {
	doc, err := goquery.NewDocument("https://example.com")
	if err != nil {
		log.Fatal(err)
	}

	doc.Find("table tr").Each(func(index int, row *goquery.Selection) {
		row.Find("td").Each(func(indexTD int, cell *goquery.Selection) {
			fmt.Printf("Row %d, Cell %d: %s\n", index+1, indexTD+1, cell.Text())
		})
	})
}
```

**Explanation:**

* `Find("table tr")`: Finds all table rows.
* Nested `Find("td")`: Iterates through each cell in the row.

***

#### Example 4: Manipulating HTML

GoQuery also allows you to manipulate HTML elements. Here’s how you can modify an element’s content:

```go
func main() {
	html := `<div class="content">Hello, World!</div>`
	doc, err := goquery.NewDocumentFromReader(strings.NewReader(html))
	if err != nil {
		log.Fatal(err)
	}

	doc.Find(".content").Text("Hello, GoQuery!")
	updatedHTML, _ := doc.Html()
	fmt.Println(updatedHTML)
}
```

**Explanation:**

* `NewDocumentFromReader`: Loads HTML from a string.
* `Text`: Updates the content of the selected element.
* `Html`: Returns the updated HTML document as a string.

***

### Advanced Features

#### Selecting Elements with Complex CSS Selectors

GoQuery supports complex CSS selectors:

```go
doc.Find("div.content > p.highlight").Each(func(index int, item *goquery.Selection) {
	fmt.Println(item.Text())
})
```

#### Chaining Methods

You can chain methods for more concise code:

```go
links := doc.Find("a").Map(func(index int, item *goquery.Selection) string {
	link, _ := item.Attr("href")
	return link
})
fmt.Println("Links:", links)
```

#### Handling HTTP Requests with Custom Headers

To handle HTTP requests with custom headers, use `http.Client`:

```go
import (
	"net/http"
)

func main() {
	client := &http.Client{}
	req, err := http.NewRequest("GET", "https://example.com", nil)
	if err != nil {
		log.Fatal(err)
	}
	req.Header.Set("User-Agent", "GoQuery-Tutorial")

	resp, err := client.Do(req)
	if err != nil {
		log.Fatal(err)
	}
	defer resp.Body.Close()

	doc, err := goquery.NewDocumentFromReader(resp.Body)
	if err != nil {
		log.Fatal(err)
	}

	fmt.Println(doc.Find("title").Text())
}
```

***

### Tips for Effective Scraping

1. **Respect Robots.txt:** Check the website’s `robots.txt` file to ensure scraping is allowed.
2. **Throttle Requests:** Use delays between requests to avoid overloading the server.
3. **Handle Errors Gracefully:** Anticipate broken links, missing elements, or rate limits.
4. **Use Proxies:** For large-scale scraping, consider using proxies to distribute requests.

***

### Table of GoQuery Functions

| Function                | Description                                       | Parameters                              |
| ----------------------- | ------------------------------------------------- | --------------------------------------- |
| `NewDocument`           | Loads an HTML document from a URL.                | `url string`                            |
| `NewDocumentFromReader` | Loads an HTML document from an `io.Reader`.       | `reader io.Reader`                      |
| `Find`                  | Searches for elements matching a CSS selector.    | `selector string`                       |
| `Each`                  | Iterates over each matched element.               | `func(index int, selection *Selection)` |
| `Attr`                  | Retrieves the value of an attribute.              | `attrName string`                       |
| `Text`                  | Extracts or sets the text content of elements.    | `text string` (optional)                |
| `Html`                  | Retrieves or sets the HTML content of elements.   | `html string` (optional)                |
| `Map`                   | Maps each element to a value and returns a slice. | `func(index int, selection *Selection)` |
| `Children`              | Selects all direct child elements.                | `selector string` (optional)            |
| `Parent`                | Selects the parent of each element.               | None                                    |
| `Remove`                | Removes the selected elements from the document.  | None                                    |

***

### Conclusion

GoQuery is a powerful and easy-to-use library for web scraping and HTML manipulation in Go. With its jQuery-like syntax, it simplifies working with complex HTML documents. By practicing with the examples above, you can master GoQuery and build efficient web scraping applications.
