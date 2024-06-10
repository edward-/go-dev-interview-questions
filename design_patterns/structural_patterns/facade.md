# Facade Design Pattern

## What is the Facade design pattern?
The Facade design pattern provides a simplified, unified interface to a set of interfaces in a subsystem, making it easier to use and reducing the dependencies on the complex subsystem.

## When should you use the Facade design pattern?
- When you want to provide a simple interface to a complex subsystem.
- When you want to reduce the dependencies of the client code on the inner workings of a subsystem.
- When you want to improve the readability and usability of a library or framework.

## How does the Facade design pattern work?
The Facade pattern involves creating a single class that provides simplified methods that delegate calls to the more complex classes in the subsystem. This class acts as an intermediary between the client code and the subsystem.

## What are the benefits of using the Facade design pattern?
Simplifies the interface of a complex subsystem.
Reduces the dependencies between the client code and the subsystem.
Makes the subsystem easier to use and understand.
Provides a layer of abstraction that can hide the implementation details of the subsystem.

## What are the drawbacks of the Facade design pattern?
- Can lead to more code if not used judiciously.
- May hide the complexity too much, making it harder to understand the underlying subsystem when needed.
- If the Facade class itself becomes too complex, it can become a "god object."

## How does the Facade pattern differ from other structural patterns like Adapter or Proxy?
The Facade pattern provides a simplified interface to a subsystem without altering its interface.
The Adapter pattern changes the interface of an existing object to make it compatible with another interface.
The Proxy pattern provides a surrogate or placeholder for another object to control access to it.

## Can the Facade pattern be combined with other design patterns?
Yes, the Facade pattern can be combined with other patterns like Singleton (to ensure a single instance of the Facade), Adapter (to adapt interfaces before passing them to the Facade), and others to enhance its functionality and usability.

# Example

```go
package main

import "fmt"

// Subsystem1 provides the implementation of a subsystem.
type Subsystem1 struct{}

func (s *Subsystem1) Operation1() {
    fmt.Println("Subsystem1: Operation1")
}

// Subsystem2 provides the implementation of another subsystem.
type Subsystem2 struct{}

func (s *Subsystem2) Operation2() {
    fmt.Println("Subsystem2: Operation2")
}

// Facade provides a simplified interface to the subsystems.
type Facade struct {
    subsystem1 *Subsystem1
    subsystem2 *Subsystem2
}

func NewFacade() *Facade {
    return &Facade{
        subsystem1: &Subsystem1{},
        subsystem2: &Subsystem2{},
    }
}

func (f *Facade) SimplifiedOperation() {
    f.subsystem1.Operation1()
    f.subsystem2.Operation2()
}

func main() {
    facade := NewFacade()
    facade.SimplifiedOperation()
}
```

[Go Playground Facade](https://go.dev/play/p/ugnOdNR7aRp)