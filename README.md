# bufio _fork: writer buffer injection_

[![godoc - documentation](https://godoc.org/github.com/ahmedabdou14/bufio?status.svg)](https://pkg.go.dev/github.com/ahmedabdou14/bufio)
[![go report card](https://goreportcard.com/badge/github.com/ahmedabdou14/bufio)](https://goreportcard.com/report/github.com/ahmedabdou14/bufio)
[![github action - test](https://github.com/ahmedabdou14/bufio/workflows/test/badge.svg)](https://github.com/ahmedabdou14/bufio/actions)
[![codecov - code coverage](https://img.shields.io/codecov/c/github/ahmedabdou14/bufio.svg?style=flat-square)](https://codecov.io/gh/ahmedabdou14/bufio)

A fork of Go's standard bufio package, adding support for buffer injected writers.

## Installation

```shell
go get -u github.com/ahmedabdou14/bufio
```

## Usage

```go
package main

import (
    "os"

    "github.com/ahmedabdou14/bufio"
)

func main() {
    file, err := os.Create("test.txt")
    if err != nil {
        panic(err)
    }
    defer file.Close()

    buf := make([]byte, 10) 
    
    w := bufio.NewWriterBuffer(file, buf)
    w.WriteString("Hello, World!")
    w.Flush() 
}
```

## Why?

Only use this package if you need the fine-grained control over the buffers used by the writer. One use case is when you want to reuse buffers for multiple writers **and** somewhere else in your code. For more details, checkout this [issue](https://github.com/golang/go/issues/69970)

Maybe you do not need this package, in most usecases, you would only need to reuse the writers themselves, not the buffers.  For more details, checkout this [issue](https://github.com/golang/go/issues/13650)

## Warning ⚠️

Be carful of using the buffer after passing it to the writer. Doings so will result in unexpected behavior.
