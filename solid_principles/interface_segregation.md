# Interface Segregation Principle

### Definition

A client should never be forced to implement an interface that it doesn’t use, or clients shouldn’t be forced to depend on methods they do not use.

Example:


```go
// smaller interfaces
type Measurable interface {
  Area() float64
}

type Voluminous interface {
  Volume() float64
}

// object
type Square struct {
  side float64
}

func (s Square) Area() float64 {
  return s.side * s.side
}

// object
type Sphere struct {
  radius float64
}

func (s Sphere) Area() float64 {
  return 4 * math.Pi * s.radius * s.radius
}

func (s Sphere) Volume() float64 {
  return (4 * math.Pi * s.radius * s.radius * s.radius) / 3
}
```

This reduced coupling means that the code using shapes only depends on the interface they need (Measurable or both). Clearer Responsibilities, Interfaces have a specific purpose (area or volume).


### What is the Interface Segregation Principle (ISP)?
ISP states that clients should not be forced to depend on interfaces they do not use, meaning that the interfaces should be designed to be as small and specific as possible. This helps to keep the code flexible and avoids unnecessary coupling between classes.

### Why is it better to have smaller, specific interfaces than large, general ones?
* Smaller, specific interfaces promote better design practices, improve code readability, maintainability, and scalability, and contribute to the creation of more cohesive and adaptable software systems.
* It becomes easier to understand and maintain the code.
* Each component's purpose is more precisely delineated.
* Smaller interfaces lead to reduced dependencies between components.
* Minimize unnecessary coupling and enhancing the modularity and flexibility of the system.
* Smaller interfaces facilitate easier extension of the system. When new functionalities need to be added, developers can introduce new interfaces without needing to modify existing large interfaces, thus adhering to the Open/Closed Principle.
