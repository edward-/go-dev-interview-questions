# Strategy Design Pattern

## What is the Strategy design pattern?


Strategy is a behavioral design pattern that lets you define a family of algorithms, put each of them into a separate class, and make their objects interchangeable.

The Strategy pattern defines a family of algorithms, encapsulates each one, and makes them interchangeable. It allows the algorithm to vary independently from clients that use it.

## When should I use the Strategy design pattern?
- Use the Strategy pattern when you have multiple algorithms for a specific task and want to switch between them dynamically.
- When you want to avoid conditional statements for selecting algorithms.
- When you have classes that differ only in their behavior.


## What are the main components of the Strategy design pattern?
- Context: Maintains a reference to a strategy object.
- Strategy: An interface common to all supported algorithms.
- ConcreteStrategy: Implements the algorithm using the Strategy interface.

## What are the benefits of using the Strategy design pattern?
- Flexibility: Strategies can be switched at runtime.
- Encapsulation: Algorithms are encapsulated in separate classes.
- Maintainability: Adding new algorithms does not affect existing code.

## What are the drawbacks of using the Strategy design pattern?
- Overhead: Increased number of objects.
- Complexity: Requires understanding and managing the Strategy interface and its implementations.


## Can you provide real-world examples where the Strategy design pattern is useful?
- Sorting algorithms: Different sorting strategies (e.g., QuickSort, MergeSort).
- Compression algorithms: Various compression strategies (e.g., ZIP, RAR).
- Payment processing: Different payment methods (e.g., credit card, PayPal).

# How does the Strategy design pattern differ from the State design pattern?
- Strategy: Focuses on defining a family of algorithms.
- State: Focuses on changing the behavior of an object based on its state.

# How is the Strategy pattern different from the Template Method pattern?

- Strategy: Encapsulates interchangeable algorithms, chosen at runtime.
- Template Method: Defines the skeleton of an algorithm, with steps implemented in subclasses.

## How can you test classes implementing the Strategy design pattern?
- Use unit tests to verify that each ConcreteStrategy produces the correct results for given inputs.
- Test the Context to ensure it correctly switches between different strategies and executes them properly.

# Example

```go
package main

import "fmt"

// Strategy interface
type Strategy interface {
    Execute(a, b int) int
}

// ConcreteStrategyA
type AddStrategy struct{}

func (s *AddStrategy) Execute(a, b int) int {
    return a + b
}

// ConcreteStrategyB
type MultiplyStrategy struct{}

func (s *MultiplyStrategy) Execute(a, b int) int {
    return a * b
}

// Context
type Context struct {
    strategy Strategy
}

func (c *Context) SetStrategy(strategy Strategy) {
    c.strategy = strategy
}

func (c *Context) ExecuteStrategy(a, b int) int {
    return c.strategy.Execute(a, b)
}

func main() {
    context := &Context{}

    context.SetStrategy(&AddStrategy{})
    fmt.Println("AddStrategy:", context.ExecuteStrategy(3, 4))

    context.SetStrategy(&MultiplyStrategy{})
    fmt.Println("MultiplyStrategy:", context.ExecuteStrategy(3, 4))
}
```

[Go Playground Stratety](https://go.dev/play/p/Z6z0fLPZkg2)