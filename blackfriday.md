---
icon: markdown
---

# Blackfriday

## Blackfriday&#x20;

Blackfriday is a [Markdown](https://daringfireball.net/projects/markdown/) processor implemented in [Go](https://golang.org/). It is paranoid about its input (so you can safely feed it user-supplied data), it is fast, it supports common extensions (tables, smart punctuation substitutions, etc.), and it is safe for all utf-8 (unicode) input.

HTML output is currently supported, along with Smartypants extensions.

It started as a translation from C of [Sundown](https://github.com/vmg/sundown).

***

### Installation

Blackfriday is compatible with modern Go releases in module mode. With Go installed:

```
go get github.com/russross/blackfriday
```

will resolve and add the package to the current development module, then build and install it. Alternatively, you can achieve the same if you import it in a package:

```
import "github.com/russross/blackfriday"
```

and `go get` without parameters.

Old versions of Go and legacy GOPATH mode might work, but no effort is made to keep them working.

### Usage

v1

For basic usage, it is as simple as getting your input into a byte slice and calling:

```
output := blackfriday.MarkdownBasic(input)
```

This renders it with no extensions enabled. To get a more useful feature set, use this instead:

```
output := blackfriday.MarkdownCommon(input)
```

v2

For the most sensible markdown processing, it is as simple as getting your input into a byte slice and calling:

```
output := blackfriday.Run(input)
```

Your input will be parsed and the output rendered with a set of most popular extensions enabled. If you want the most basic feature set, corresponding with the bare Markdown specification, use:

```
output := blackfriday.Run(input, blackfriday.WithNoExtensions())
```

#### Sanitize untrusted content

Blackfriday itself does nothing to protect against malicious content. If you are dealing with user-supplied markdown, we recommend running Blackfriday's output through HTML sanitizer such as [Bluemonday](https://github.com/microcosm-cc/bluemonday).

Here's an example of simple usage of Blackfriday together with Bluemonday:

```
import (
    "github.com/microcosm-cc/bluemonday"
    "github.com/russross/blackfriday"
)

// ...
unsafe := blackfriday.Run(input)
html := bluemonday.UGCPolicy().SanitizeBytes(unsafe)
```

#### Custom options, v1

If you want to customize the set of options, first get a renderer (currently only the HTML output engine), then use it to call the more general `Markdown` function. For examples, see the implementations of `MarkdownBasic` and `MarkdownCommon` in `markdown.go`.

Custom options, v2

If you want to customize the set of options, use `blackfriday.WithExtensions`, `blackfriday.WithRenderer` and `blackfriday.WithRefOverride`.`blackfriday-tool`

You can also check out `blackfriday-tool` for a more complete example of how to use it. Download and install it using:

```
go get github.com/russross/blackfriday-tool
```

This is a simple command-line tool that allows you to process a markdown file using a standalone program. You can also browse the source directly on github if you are just looking for some example code:

***





