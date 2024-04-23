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
```go
// for loop
for i := 0; i < 10; i++ {
  ...
}

// while loop
for {
  if something {
    break
  }
}

// for each loop
items := []int{1, 2, 3, 4}
for index, item := range items {
  ...
}
```

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
  Name  string
  Balance T
}
```


## Concurrency and Parallelism
### Goroutines
A goroutine is a lightweight thread managed by the Go runtime. They are useful when you want to run background processes and collect results, or simply move on without while process runs in background.

```go
// using anonymous function
go func() {
  fmt.Println("Hello")
}()

// or call an actual function
go sayHello()
```

Main go program won't wait for these to finish. If you need to analyse results of these routines, you'll need either channels or waitgroups.

### Channels
### Wait groups

```go
import "sync"

var waitGroup sync.WaitGroup

for i := 0; i < 5; i++ {
  waitGroup.Add(1) // tell waitGroup to include one more in waitlist

  go func(n int) {
    fmt.Printf("Hello %d", n)

    waitGroup.Done()
  }(i)
}

waitGroup.Wait() // waits for all routines to call .Done
```
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
Some of frequently used string methods are listed below. [Full list](https://pkg.go.dev/strings)
```go
// Clone returns a copy of the given string.
strings.Clone("Hello, World!") // Output: Hello, World!

// Compare returns an integer comparing two strings lexicographically.
// It returns 0 if a == b, -1 if a < b, and 1 if a > b.
strings.Compare("apple", "banana") // Output: -1

// Contains reports whether substr is within s.
strings.Contains("gopher", "ph") // Output: true

// ContainsAny reports whether any Unicode code points in chars are within s.
strings.ContainsAny("hello", "aeiou") // Output: true

// ContainsRune reports whether the Unicode code point r is within s.
strings.ContainsRune("hello", 'o') // Output: true

// Count counts the number of non-overlapping instances of substr in s.
strings.Count("cheese", "e") // Output: 3

// Cut slices s into all substrings separated by sep and returns a slice of the substrings between those separators.
strings.Cut("a-b-c-d-e", "-") // Output: ["a" "b" "c" "d" "e"]

// CutPrefix returns s without the provided leading prefix string.
strings.CutPrefix("Goodbye, world!", "Goodbye, ") // Output: world!

// CutSuffix returns s without the provided trailing suffix string.
strings.CutSuffix("Goodbye, world!", ", world!") // Output: Goodbye

// HasPrefix tests whether the string s begins with prefix.
strings.HasPrefix("Gopher", "Go") // Output: true

// HasSuffix tests whether the string s ends with suffix.
strings.HasSuffix("Amigo", "go") // Output: true

// Index returns the index of the first instance of substr in s, or -1 if substr is not present in s.
strings.Index("chicken", "ken") // Output: 4

// IndexAny returns the index of the first instance of any Unicode code point from chars in s, or -1 if no Unicode code point from chars is present in s.
strings.IndexAny("chicken", "aeiou") // Output: 2

// Join concatenates the elements of a to create a single string. The separator string sep is placed between elements in the resulting string.
strings.Join([]string{"hello", "world"}, ", ") // Output: hello, world

// LastIndex returns the index of the last instance of substr in s, or -1 if substr is not present in s.
strings.LastIndex("go gopher", "go") // Output: 3

// LastIndexAny returns the index of the last instance of any Unicode code point from chars in s, or -1 if no Unicode code point from chars is present in s.
strings.LastIndexAny("go gopher", "ao") // Output: 4

// Map returns a copy of the string s with all its characters modified according to the mapping function.
strings.Map(func(r rune) rune { return r + 1 }, "hello") // Output: "ifmmp"

// Repeat returns a new string consisting of count copies of the string s.
strings.Repeat("na", 3) // Output: "nanana"

// Replace returns a copy of the string s with the first n non-overlapping instances of old replaced by new.
strings.Replace("oink oink oink", "k", "ky", 2) // Output: "oinky oinky oink"

// ReplaceAll returns a copy of the string s with all non-overlapping instances of old replaced by new.
strings.ReplaceAll("oink oink oink", "k", "ky") // Output: "oinky oinky oinky"

// Split slices s into all substrings separated by sep and returns a slice of the substrings between those separators.
strings.Split("a,b,c", ",") // Output: ["a" "b" "c"]

// SplitAfter slices s into all substrings after each instance of sep and returns a slice of those substrings.
strings.SplitAfter("a,b,c", ",") // Output: ["a," "b," "c"]

// SplitAfterN slices s into substrings after each instance of sep and returns a slice of those substrings.
strings.SplitAfterN("a,b,c", ",", 2) // Output: ["a," "b,c"]

// SplitN slices s into substrings separated by sep and returns a slice of the substrings between those separators.
strings.SplitN("a,b,c", ",", 2) // Output: ["a" "b,c"]

// Title returns a copy of the string s with all Unicode letters that begin words mapped to their title case.
strings.Title("her royal highness") // Output: "Her Royal Highness"

// ToLower returns a copy of the string s with all Unicode letters mapped to their lower case.
strings.ToLower("Gopher") // Output: "gopher"

// ToUpper returns a copy of the string s with all Unicode letters mapped to their upper case.
strings.ToUpper("Gopher") // Output: "GOPHER"

// Trim returns a slice of the string s with all leading and trailing Unicode code points contained in cutset removed.
strings.Trim("¡¡¡Hello, Gophers!!!", "!¡") // Output: "Hello, Gophers"

// TrimLeft returns a slice of the string s with all leading Unicode code points contained in cutset removed.
strings.TrimLeft("¡¡¡Hello, Gophers!!!", "!¡") // Output: "Hello, Gophers!!!"

// TrimRight returns a slice of the string s with all trailing Unicode code points contained in cutset removed.
strings.TrimRight("¡¡¡Hello, Gophers!!!", "!¡") // Output: "¡¡¡Hello, Gophers"

// TrimSpace returns a slice of the string s with all leading and trailing white space removed, as defined by Unicode.
strings.TrimSpace(" \t\n Hello, Gophers \n\t\r\n") // Output: "Hello, Gophers"

```
### Print functions
### Test functions
### Time functions
### Slice functions
### Sort functions
### Operating system functions
### Random numbers
### UUID functions
### Null functions

