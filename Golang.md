
## Enable dependency tracking for your code

```go
$ go mod init example/hello
```

# Interface 

Go language interfaces are different from other languages. In Go language, the interface is a custom type that is used to specify a set of one or more method signatures and the interface is abstract, so you are not allowed to create an instance of the interface. But you are allowed to create a variable of an interface type and this variable can be assigned with a concrete type value that has the methods the interface requires. Or in other words, the interface is a collection of methods as well as it is a custom type.

``` go
package main
  
import "fmt"
  
// Creating an interface
type tank interface {
  
    // Methods
    Tarea() float64
    Volume() float64
}
  
type myvalue struct {
    radius float64
    height float64
}
  
// Implementing methods of
// the tank interface
func (m myvalue) Tarea() float64 {
  
    return 2*m.radius*m.height +
        2*3.14*m.radius*m.radius
}
  
func (m myvalue) Volume() float64 {
  
    return 3.14 * m.radius * m.radius * m.height
}
  
// Main Method
func main() {
  
    // Accessing elements of
    // the tank interface
    var t tank
    t = myvalue{10, 14}
    fmt.Println("Area of tank :", t.Tarea())
    fmt.Println("Volume of tank:", t.Volume())
}
```

# Goroutine

Goroutines are functions or methods that run concurrently with other functions or methods. Goroutines can be thought of as lightweight threads
Let's create a Goroutine :)
```go
package main

import (  
    "fmt"
)

func hello() {  
    fmt.Println("Hello world goroutine")
}
func main() {  
    go hello()
    fmt.Println("main function")
}
```
Output: 
main function


## Fixed
```go
package main

import (  
    "fmt"
    "time"
)

func hello() {  
    fmt.Println("Hello world goroutine")
}
func main() {  
    go hello()
    time.Sleep(1 * time.Second)
    fmt.Println("main function")
}
```

# Channel

Channels can be thought of as pipes using which Goroutines communicate. Similar to how water flows from one end to another in a pipe, data can be sent from one end and received from the other end using channels.

```go
data := <- a // read from channel a  
a <- data // write to channel a  
```

## Usage of Channel

```go
package main

import (  
    "fmt"
)

func hello(done chan bool) {  
    fmt.Println("Hello world goroutine")
    done <- true
}
func main() {  
    done := make(chan bool)
    go hello(done)
    <-done
    fmt.Println("main function")
}
```
