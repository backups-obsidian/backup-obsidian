---
created: 2022-05-15 21:47
updated: 2022-05-29 13:15
---
---
**Links**: [[103 Golang Index]]

---
## Functions
- Go recommends writing function names in simple word or **camelCase**.

> [!caution]- Within the same package function names must be unique!
- One of Go's features is that functions and methods **can return multiple values**.
- Go *doesn't support function overloading*.
- Everything in Go is **passed by value**.

### Defining functions
```go
func f1(a int, b int){
	// statements
}
f1(3,5)
```
- Shorthand parameter notation
```go
func f1(a,b int, c,d float64) {
	// statements
}
f1(1,2,3.4,4.5)
```

> [!caution] There are **no default arguments** in Go.

### Returning values
- If the function is returning something its return type must be specified
- Simple return
```go
func f1(a int) int {
	return a
}
```

#### Multiple return
- If `error` is returned then as a convention it should be the last parameter
- For multiple return values type must be inside parenthesis
```go
func f1(a int) (string, int) {
	// statements
	return "hello", 54
}
a, b := f1(3)
_, d := f1(5) // if you are interested in only one value 
```

#### Named Return
- We can return the named parameters without any value. 
- This is known as *naked return* and should *only be used in short functions* as it harms the readability in long functions.	
```go
// behind the scenes it does var s string inside the function
func f1(a int) (s string) {
	fmt.Println(s, a) // "" 45 -> we get default value since it has been declared
	s = "hello"
	return // naked return, same as return s
}
val := f1(45)
fmt.Println(val) // hello
```
- We can also return multiple values with named return
```go
func f1(a int) (s string, b int) {
	s = "hello"
	b = 100
	return
}
val, b := f1(45)
fmt.Println(val, b) // hello 100
```

### Variadic Functions
