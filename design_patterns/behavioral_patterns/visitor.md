# Visitor Design Pattern

## What is the Visitor design pattern?
The Visitor design pattern is a way of separating an algorithm from an object structure on which it operates. This pattern is particularly useful for adding new operations to existing object structures without modifying those structures.

## What problem does the Visitor pattern solve?
The Visitor pattern addresses the problem of adding new operations to existing class hierarchies without altering the classes. It provides a way to centralize the operations on objects, making the code more maintainable and extensible.

## How does the Visitor pattern work?
The Visitor pattern involves two main components:

- Visitor Interface: Declares a visit method for each type of element that can be visited.
- Concrete Visitor: Implements the visitor interface and defines the operations to be performed on the elements.
- Element Interface: Declares an accept method that takes a visitor as an argument.
- Concrete Element: Implements the accept method and calls the appropriate visit method on the visitor.

## When should you use the Visitor pattern?
The Visitor pattern is useful when:

- You have a complex object structure and you need to perform operations on it.
- You want to add new operations without modifying the existing object structure.
- The object structure rarely changes, but you often need to define new operations.

## What are the advantages of the Visitor pattern?
- Separation of concerns: It separates the algorithm from the object structure.
- Easy to add new operations: New operations can be added without changing the classes of the elements.
- Single Responsibility Principle: It allows you to keep related operations together by defining them in one class.

## What are the disadvantages of the Visitor pattern?
- Difficulty adding new element types: Adding new element types requires changes to the visitor interface and all its implementations.
- Circular dependency: There can be a circular dependency between the element and the visitor.

## How does the Visitor pattern adhere to the Open/Closed Principle?
The Visitor pattern adheres to the Open/Closed Principle by allowing new operations to be added without modifying the existing structure. Instead of changing the classes of the elements, you create new visitor classes that implement the new operations.

## What are some real-world examples of the Visitor pattern?
Some real-world examples of the Visitor pattern include:

- Compilers that traverse and perform operations on a syntax tree.
- Graphic applications that process different types of shapes.
- Document converters that transform documents into different formats.

## What are the alternatives to the Visitor pattern?
Alternatives to the Visitor pattern include:

- Using double dispatch to handle multiple types.
- Implementing operations directly within the element classes if the operations are few and unlikely to change.
- Using reflection to dynamically perform operations, although this can reduce type safety and performance.


# Example

```go
package main

import "fmt"

// Visitor interface
type Visitor interface {
    VisitCircle(*Circle)
    VisitRectangle(*Rectangle)
}

// Element interface
type Shape interface {
    Accept(Visitor)
}

// Concrete Element: Circle
type Circle struct {
    Radius int
}

func (c *Circle) Accept(v Visitor) {
    v.VisitCircle(c)
}

// Concrete Element: Rectangle
type Rectangle struct {
    Width, Height int
}

func (r *Rectangle) Accept(v Visitor) {
    v.VisitRectangle(r)
}

// Concrete Visitor
type AreaCalculator struct {
    Area int
}

func (a *AreaCalculator) VisitCircle(c *Circle) {
    a.Area = 3 * c.Radius * c.Radius // Approximation of π * r^2
    fmt.Printf("Circle area: %d\n", a.Area)
}

func (a *AreaCalculator) VisitRectangle(r *Rectangle) {
    a.Area = r.Width * r.Height
    fmt.Printf("Rectangle area: %d\n", a.Area)
}

func main() {
    circle := &Circle{Radius: 5}
    rectangle := &Rectangle{Width: 4, Height: 6}

    areaCalculator := &AreaCalculator{}

    circle.Accept(areaCalculator)
    rectangle.Accept(areaCalculator)
}

```

[Go Playground Visitor](https://go.dev/play/p/mEj6g2AHemd)