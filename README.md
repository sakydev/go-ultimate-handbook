# Golang: Ultimate Handbook
A super detailed handbook for Golang

## Basics of GoLang
- [Basic commands](#basic-commands)
- [Variables](#variables)
- [Loops](#loops)
- [Functions](#functions)
- [If statements](#if-statements)
- [Switch](#switch)
- [Anonymous functions](#anonymous-functions)
- [Variadic functions](#variadic-functions)
- [Error handling](#error-handling)
- [Defer](#defer)
- [Receivers](#receivers)

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
- [Mutex](#mutex)
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

## Basics of GoLang
### Basic commands
### Variables
### Loops
### Functions
### If statements
### Switch
### Anonymous functions
### Variadic functions
### Error handling

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

### Receivers
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

## Data Structures and Types
### Structs
### Slices
### Maps
### Runes
### Interfaces
### Generics
There might be situations where you can't fully predict types of data. These can be function parameters or return types. In such cases, you can use generics to specify one or multiple types to anticipate. These were introduced in `go 1.18`

**Generic methods**  
A simple example where we do multiplication. Both numbers can either be `int` or `float64`
```go
func multiply[T int | float64](number T, multiplier T) T {
  return number + multiplier // output: 7.1
}
```

If we want to specify more types without things getting too ugly, we can also make use of interfaces.
```go
type customType interface {
  int | int64 | float64 | float32
}

func multiply[T customType](number T, multiplier T) T {
  return number + multiplier
}
```

**Generic structs**  
We can specify `struct` fields as generics too. Again, we can specify inline types or use interface
```go
type Balance interface {
	int | int64 | float64
}

type Person[T Balance] struct {
	Name    string
	Balance T
}
```


## Concurrency and Parallelism
### Goroutines
### Channels
### Wait groups
### Mutex
### Context

## Advanced Topics
### Reflection
### Type assertion & conversion
### Dependency Injection

## File Operations
### File handling
### JSON Encoding & decoding

## Web Development
### HTTP functions
### URL functions
### Path functions
### Templates
### Database operations

## Utility Functions
### Math functions
### String functions
### Print functions
### Test functions
### Time functions
### Slice functions
### Sort functions
### Operating system functions
### Random numbers
### UUID functions
### Null functions

