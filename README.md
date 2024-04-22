# Golang: Ultimate Handbook
A super detailed handbook for Golang

### Defer
Execution of a function can be delayed with `defer` keyword. This is useful for closing database/files and performing cleanups etc. Methods are executed on first in / last out bases. The method defered earliest will be executed last inside a method context.

```go
func executesLast() {
  fmt.Println("I ran first but executed last")
}

func main() {
  defer executesLast()

  fmt.Println("I'll execute first")
}
```

### Reciever methods
You can create callable methods on structs. There you may access struct values or simply perform other actions.

```go
type person struct {
  Name string
  Age  int
}

func (p person) canVote() {
  if p.Age >= 18 {
    fmt.Printf("Hi %s, Welcome!", p.Name)
  }

  fmt.Printf("Sorry %s!", p.Name)
}

voter := person{
  Name: "Saqib",
  Age: 29
}

voter.canVote() // prints "Hi Saqib, Welcome!"
```

## Basics of GoLang
- [Basic commands](#basic-commands)
- [Variables](#variables)
- [Loops](#loops)
- [Functions](#functions)
- [If statements](#if-statements)
- [Switch](#switch)
- [Anonymous functions](#anonymous-functions)
- [Variadic functions](#variadic-functions)
- [Error handling](#errors)

## Data Structures and Types
- [Structs](#structs)
- [Slices](#slices)
- [Maps](#maps)
- [Runes](#runes)
- [Interfaces](#interfaces)
- [Generics](#generics)

## Concurrency and Parallelism
- [Goroutines](#go-routines)
- [Channels](#channels)
- [Wait groups](#wait-groups)
- [Context](#context)

## Advanced Topics
- [Reflection](#reflections)
- [Type assertion & conversion](#type-assertion--conversion)
- [Dependency Injection](#dependency-injection)

## File Operations
- [File handling](#file-handling)
- [JSON Encoding & decoding](#json-encoding--decoding)

## Web Development
- [HTTP functions](#http-functions)
- [URL functions](#url-functions)
- [Path functions](#path-functions)
- [Templates](#templates)
- [Database operations](#database-operations)

## Utility Functions
- [Math functions](#math-functions)
- [String functions](#string-functions)
- [Print functions](#print-functions)
- [Test functions](#test-functions)
- [Time functions](#time-functions)
- [Slice functions](#slice-functions)
- [Sort functions](#sort-functions)
- [Operating system functions](#operating-system-functions)
- [Random numbers](#random-numbers)
- [UUID functions](#uuid-functions)
- [Null functions](#null-functions)

