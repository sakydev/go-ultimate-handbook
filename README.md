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

