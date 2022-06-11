---
created: 2022-06-05 11:28
updated: 2022-06-11 15:24
---
---
**Links**: [[103 Golang Index]]

---
## Channels
- A channel in go provides a **connection between 2 go routines** allowing them to communicate.
- Channels are used to *communicate in between running go routines*.
- Value of an uninitialised channel is `nil`
```go
var ch chan int
fmt.Println(ch)  // <nil>
// initialising the channel
ch = make(chan int)
fmt.Println(ch) // hexadecimal address (pointer)
```
- Passing channels to functions is same as passing pointers to functions
- Initialisation and declaration
	- `ch := make(chan int)`
- A channel is a 2 way messaging object.
- We send and receive messages using the channel operator  (`<-`)
	- *Sending* value to the channel : `ch <- 10`
	- *Receiving* value from the channel : `num := <- ch`
		- `fmt.Println(<- ch)`
- Closing the channel : `close(ch)`
- The channel created above was a *bidirectional channel*. We can create *uni-directional channels* using : 
	- Only for receiving : `c1 := make(<-chan string)`
	- Only for sending: `c2 := make(chan<- string)`

- Simple example to communicate between 2 go routines.
	- **Remember `main` is also a go routine**
```go
func f1(n int, ch chan int) {
	ch <- n // sending value to the channel
}

func main() {
	ch := make(chan int)
	go f1(10, ch)
	fmt.Println(<-ch) // receiving value from the channel
	close(ch)         // closing the channel
}
```

- Another example
```go
func f1(n int, ch chan int) {
	fact := 1

	for i := 2; i <= n; i++ {
		fact = fact * i
	}
	ch <- fact
}

func main() {
	ch := make(chan int)
	defer close(ch)
	go f1(5, ch)
	fmt.Println(<-ch) // blocking call
	// The main go routine will wait to receive the value from the channel, this is a blocking call.
	// this is the reason why we don't need waitgroups

	// using anonymous functions
	for i := 5; i < 15; i++ {
	    go func(n int, c chan int) {
            f := 1
            for i := 2; i <= n; i++ {
                f *= i
            }
            c <- f
        }(i, ch) // passing values to anonymous functions
        fmt.Printf("Factorial of %d is %d\n", i, <-ch)
    }
}
```
