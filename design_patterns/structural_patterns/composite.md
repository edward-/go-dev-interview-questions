# Composite Design Pattern

## What is the Composite design pattern?
The Composite design pattern is a structural pattern used to represent part-whole hierarchies. It allows individual objects and compositions of objects to be treated uniformly by placing them in a tree structure.

## What problem does the Composite design pattern solve?
The Composite pattern solves the problem of treating individual objects and compositions of objects uniformly. It allows clients to work with complex tree structures in a way that simplifies code and improves flexibility.

## When should I use the Composite design pattern?
Use the Composite pattern when you need to represent a part-whole hierarchy, and you want to treat individual objects and compositions of objects uniformly. It is particularly useful when dealing with tree structures or when objects need to be composed recursively.

## How does the Composite design pattern work?
The Composite pattern works by defining a common interface for both simple and complex objects. This interface typically includes methods for adding, removing, and accessing child components. Composite objects contain a list of child components and implement the interface by delegating operations to their children.

## What are the components of the Composite design pattern?
The main components of the Composite pattern are:

Component: An interface or abstract class defining common operations.
Leaf: A concrete class implementing the Component interface for individual objects.
Composite: A concrete class implementing the Component interface for compositions of objects. It contains and manages child components.

## What are the benefits of using the Composite design pattern?
The benefits include:

- Simplified client code: Clients can treat individual objects and compositions uniformly.
- Flexible tree structures: Easily add or remove components.
- Promotes transparency: Component interface makes client code simpler and more flexible.

## What are the drawbacks of using the Composite design pattern?
The drawbacks include:

- Complexity: Can introduce complexity if there are many different component types.
- Overhead: Managing child components can add overhead.

## How does the Composite design pattern relate to other design patterns?
- Decorator pattern: Both can be used to manage tree structures, but Decorator adds responsibilities to objects.
- Flyweight pattern: Can be combined with Composite to reduce memory usage by sharing objects.

## How can I test code that uses the Composite design pattern?
To test code using the Composite pattern, ensure you have tests for both individual components (Leaf) and compositions (Composite). Use mocks or stubs to isolate components during testing.

# Example

```go
package main

import "fmt"

// Component interface
type Graphic interface {
    Draw()
}

// Leaf
type Circle struct{}

func (c *Circle) Draw() {
    fmt.Println("Drawing a Circle")
}

// Composite
type CompositeGraphic struct {
    graphics []Graphic
}

func (cg *CompositeGraphic) Add(graphic Graphic) {
    cg.graphics = append(cg.graphics, graphic)
}

func (cg *CompositeGraphic) Remove(graphic Graphic) {
    for i, g := range cg.graphics {
        if g == graphic {
            cg.graphics = append(cg.graphics[:i], cg.graphics[i+1:]...)
            break
        }
    }
}

func (cg *CompositeGraphic) Draw() {
    for _, g := range cg.graphics {
        g.Draw()
    }
}

func main() {
    circle1 := &Circle{}
    circle2 := &Circle{}

    composite := &CompositeGraphic{}
    composite.Add(circle1)
    composite.Add(circle2)

    fmt.Println("Drawing composite graphic:")
    composite.Draw()
}
```

[Go Playground Composite](https://go.dev/play/p/WLMPMrclxQV)