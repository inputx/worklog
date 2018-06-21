---
layout: post
title: go test case
date: 2018-06-16 12:29 +0000
---

# Test Types
* `*testing.T`: Type T - Testing
* `*testing.B`: Type B - Benchmarks
* `*testing.M`: Type M - Main





## Example
**main.go**

```go
package main

func Sum(x int, y int) int {
	return x + y
}

func main() {
	Sum(5, 5)
}

```


**main_test.go**

```go
package main

import "testing"

func TestSum(t *testing.T) {
	total := Sum(5, 5)
	if total != 10 {
		t.Errorf("Sum was incorrect, got: %d, want: %d.", total, 10)
	}
}

```

```go
package main

import (
	"flag"
	"fmt"
	"os"
	"testing"
)

func setup() {
	println("setup")
}

func teardown() {
	println("teardown")
}

func TestMain(m *testing.M) {
	// call flag.Parse() here if TestMain uses flags
	switch os.Getenv("GO_TEST_MODE") {
	case "":
		setup()
		flag.Parse()
		exitCode := m.Run()
		fmt.Printf("exitCode is %d\n", exitCode)
		if exitCode == 0 {
			teardown()
		}

		// Exit
		os.Exit(exitCode)
	}

}

```
- Ref
 - https://splice.com/blog/lesser-known-features-go-test/
 - https://golang.org/pkg/testing/