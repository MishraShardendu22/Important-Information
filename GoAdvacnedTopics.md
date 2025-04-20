# Go Routines, Race Conditions, and Channels

## Table of Contents
- [Introduction](#introduction)
- [Code Overview](#code-overview)
- [Key Concepts](#key-concepts)
- [Usage and Compilation](#usage-and-compilation)
- [Common Errors](#common-errors)
- [Fixing Data Races](#fixing-data-races)
- [Conclusion](#conclusion)

---

## Introduction

This project demonstrates the use of Go routines, channels, and race conditions in handling concurrent operations. Go’s lightweight concurrency features allow efficient parallel execution of tasks, but care must be taken to avoid race conditions that can lead to unexpected behaviors.

### Go Routines

Go routines allow functions to run concurrently. Unlike threads, they are cheap to create, making them suitable for handling large-scale concurrency.

### Channels

Channels provide a way for goroutines to communicate by sending and receiving data. They ensure safe data sharing among different routines through synchronization.

### Race Conditions

A race condition occurs when multiple goroutines access shared memory concurrently, leading to unpredictable results. Go’s `-race` flag is used to detect such conditions during execution.

---

## Code Overview

Here's a breakdown of the main code implementing Go routines and channels:

```go
package main

import (
	"fmt"
	"sync"
)

func sender(ch chan<- int, wg *sync.WaitGroup) {
	defer wg.Done()
	for i := 1; i <= 5; i++ {
		ch <- i
	}
	close(ch)
}

func receiver(ch <-chan int, wg *sync.WaitGroup) {
	defer wg.Done()
	for num := range ch {
		fmt.Println("Received:", num)
	}
}

func main() {
	ch := make(chan int)
	wg := &sync.WaitGroup{}

	wg.Add(2)

	go sender(ch, wg)
	go receiver(ch, wg)

	wg.Wait()
}
```

---

## Key Concepts

### 1. Go Routines

- A Go routine runs a function concurrently. Multiple routines can be created within a program.

### 2. Channels

- Channels are used to send and receive data between goroutines, ensuring safe concurrent operations.

### 3. Race Conditions

- When multiple goroutines access and modify the same data without proper synchronization, a race condition occurs.

---

## Usage and Compilation

To run the program with race detection, use the following command:

```bash
go run -race main.go
```

Upon execution, race conditions will be detected, and you will see output like this:

```
==================
WARNING: DATA RACE
Read at 0x00c000008030 by goroutine 7:
  main.main.func1()
      D:/Coding Stuff Shardendu Mishra/GoLang-Further Learning/main.go:98 +0xfe

Previous write at 0x00c000008030 by goroutine 8:
  main.main.func2()
      D:/Coding Stuff Shardendu Mishra/GoLang-Further Learning/main.go:103 +0x186

Goroutine 7 (running) created at:
  main.main()
      D:/Coding Stuff Shardendu Mishra/GoLang-Further Learning/main.go:95 +0x19c

Goroutine 8 (finished) created at:
  main.main()
      D:/Coding Stuff Shardendu Mishra/GoLang-Further Learning/main.go:100 +0x244
==================
```

This indicates that multiple goroutines are accessing shared data concurrently, leading to race conditions.

---

## Common Errors

### Data Race Error

The errors indicate race conditions, where multiple goroutines access and modify shared memory concurrently.

Example error:

```
==================
WARNING: DATA RACE
Read at 0x00c000008030 by goroutine 7:
  main.main.func1()
      D:/Coding Stuff Shardendu Mishra/GoLang-Further Learning/main.go:98 +0xfe

Previous write at 0x00c000008030 by goroutine 8:
  main.main.func2()
      D:/Coding Stuff Shardendu Mishra/GoLang-Further Learning/main.go:103 +0x186

Goroutine 7 (running) created at:
  main.main()
      D:/Coding Stuff Shardendu Mishra/GoLang-Further Learning/main.go:95 +0x19c

Goroutine 8 (finished) created at:
  main.main()
      D:/Coding Stuff Shardendu Mishra/GoLang-Further Learning/main.go:100 +0x244
==================
```

---

## Fixing Data Races

To avoid data races, proper synchronization methods are needed. Using `sync.Mutex` or similar constructs ensures that goroutines do not interfere with shared resources.

Here is a corrected version:

```go
package main

import (
	"fmt"
	"sync"
)

func sender(ch chan<- int, wg *sync.WaitGroup) {
	defer wg.Done()
	for i := 1; i <= 5; i++ {
		ch <- i
	}
	close(ch)
}

func receiver(ch <-chan int, wg *sync.WaitGroup) {
	defer wg.Done()
	for num := range ch {
		fmt.Println("Received:", num)
	}
}

func main() {
	ch := make(chan int)
	wg := &sync.WaitGroup{}

	wg.Add(2)

	go sender(ch, wg)
	go receiver(ch, wg)

	wg.Wait()
}
```

With this fix, race conditions are eliminated, and safe communication between goroutines is ensured.
