# 7 Levels of Go

The Go level 99% of developers never reach.

## Level 1: Syntax

Go still forces a type on every variable, but skips semicolons and classes entirely.

```go
package main

import "fmt"

func main() {
  var name string = "Go"
  age := 16

  fmt.Println(name, "is", age)
}
```

## Level 2: Structs

Go skips class hierarchies, since a `struct` needs the right methods.

```go
package shape

type Shape interface {
  Area() float64
}

type Circle struct {
  Radius float64
}

func (c Circle) Area() float64 {
  return 3.14 * Radius * Radius
}

```

> `Circle` satisfies `Shape`, no import needed

## Level 3: Errors

Go treats an `error` as an ordinary return value.
So you check it right where it happens, wrapping it with `%w` that keeps the original
cause attached all the way up the call stack.

```go
resp, err := http.Get(url)
if err != nil {
  return fmt.Errorf("fetch: %w", err)
}
defer resp.body.Close()
```

Usage:

- retrying a failed API call
- logging why a request failed
- validating user input

## Level 4: Channels

A `goroutine` is a lightweight thread the Go runtime schedules for you.
A `channel` is the pipe two goroutines use to pass values back and forth, and
sending on it blocks until another goroutine is ready to receive.

```plaintext
+-------------+
| goroutine A |
+-------------+
+-------------+   +----------+   +------+
| goroutine A | → | chan int | → | main |
+-------------+   +----------+   +------+
+-------------+
| goroutine A |
+-------------+
```

### Implementation

Goroutine:
`go f(x, y, z)` starts a new goroutine running f(x, y, z)

```go
package main

import (
  "fmt"
  "time"
)

func say(s string) {
  for i := 0; i < 5; i++ {
    time.Sleep(100 * time.Millisecond)
    fmt.Println(s)
  }
}

func main() {
  go say("world")
  say("hello")
}
```

Channel:

```go
ch := make(chan int) // Like maps and slices, it must be created before use
ch <- v              // Send v to channel ch.
v := <-ch            // Receive from ch, and assign value to v.
```

```go
package main

import "fmt"

func sum(s []int, c chan int) {
  sum := 0
  for _, v := range s {
    sum += v
  }
  c <- sum // send sum to c
}

func main() {
  s := []int{7, 2, 8, -9, 4, 0}

  c := make(chan int)
  go sum(s[:len(s)/2], c)
  go sum(s[len(s)/2:], c)
  x, y := <-c, <-c // receive from c

  fmt.Println(x, y, x+y)
}
```

## Level 5: Standard Library

The standard library already ships a working HTTP client and server(`net/http`).
`encoding/json` turns a Go struct into a **JSON** response with one function call,
so most APIs never pull in a third-party framework at all.

Some of the most essential Go standard library packages are:

- `fmt`: For formatted I/O operations and debugging.
- `net/http`: The foundation for building web servers and clients.
- `context`: For managing request-scoped values, cancellation, and deadlines.
- `encoding/json`: For marshaling and unmarshaling JSON data.
- `io` and `bufio`: For efficient byte-based I/O operations.
- `sync`: For synchronization primitives like mutexes and wait groups.
- `os`: For operating system functionality like file handling and environment variables.
- `time`: For date and time manipulation.
- `strings` & `strconv`: For string manipulation & conversion between strings and basic data types.
- `testing`: For writing and running unit tests

Usage:

- building a CLI (binary) application
- building a REST API
- parsing a JSON payload

## Level 6: Testing

The command `go test` runs every function starting with `Test` and reports a `pass`
or `fail` for each one. Table-driven tests check a dozen inputs against one function
without writing a dozen near-identical tests.

```sh
$ go test -v ./...
=== RUN TestAdd
--- PASS: TestAdd (0.00s)
=== RUN TestParseJSON
--- PASS: TestParseJSON (0.00s)
PASS
ok shop/cart 0.412s
```

## Level 7: Scale

Understanding DevOps/Cloud Tools built in Go upgrades the developer productivity.

- `Docker`
- `Kubernetes`
- `Terraform`
- `Prometheus` and
- `Grafana`
are all written in Go.

Understanding these will help in creating better tools and solutions for scalability.
