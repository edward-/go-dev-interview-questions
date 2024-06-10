# Builder Design Pattern

## What is the Builder design pattern?
Builder is a creational design pattern that lets you construct complex objects step by step. The pattern allows you to produce different types and representations of an object using the same construction code.

## When should I use the Builder design pattern?
Use the Builder pattern when:
- You need to create an object that requires multiple steps to construct.
- The construction process of an object should be independent of the parts that make up the object.
- You need to create different representations of a complex object.

## What are the main components of the Builder design pattern?
The main components are:
- Builder: An interface or abstract class defining the steps to build the product.
- Concrete Builder: A class that implements the Builder interface and provides specific implementations of the steps to build the product.
- Director: A class that constructs an object using the Builder interface.
- Product: The complex object that is being built.

## How does the Builder pattern differ from the Factory pattern?
The Factory pattern focuses on creating objects in a single step, while the Builder pattern focuses on creating objects through a step-by-step process. The Builder pattern is more suitable for creating complex objects that require multiple steps and configurations.

## What are the advantages of using the Builder design pattern?

Advantages include:
- Separation of Concerns: The construction process is separated from the representation.
- Reusability: The same construction process can be used to create different representations of an object.
- Flexibility: Objects can be constructed step-by-step, and the construction process can be more flexible and varied.

## What are some real-world examples of the Builder design pattern?

Some real-world examples include:
- Constructing complex UI elements: In GUI frameworks, the Builder pattern is used to construct complex elements with various configurations.
- Creating configuration objects: When configuring objects that require a lot of parameters, the Builder pattern helps in creating them in a readable and maintainable way.
- Building complex documents: In applications like word processors, the Builder pattern is used to construct complex documents step-by-step.

## Can the Builder design pattern be combined with other design patterns?

Yes, the Builder pattern can be combined with other design patterns such as:
- Abstract Factory: Builders can be used in conjunction with Abstract Factories to create complex objects.
- Prototype: Builders can use prototypes to create parts of the product.
- Composite: Builders can be used to construct complex hierarchical structures.

# Example

```go
package main

import "fmt"

// Product represents the complex object being built
type Product struct {
	partA string
	partB string
	partC string
}

// Builder is the interface that specifies the steps to build a Product
type Builder interface {
	SetPartA()
	SetPartB()
	SetPartC()
	GetResult() Product
}

// ConcreteBuilder is a concrete implementation of the Builder interface
type ConcreteBuilder struct {
	product Product
}

func (b *ConcreteBuilder) SetPartA() {
	b.product.partA = "Part A"
}

func (b *ConcreteBuilder) SetPartB() {
	b.product.partB = "Part B"
}

func (b *ConcreteBuilder) SetPartC() {
	b.product.partC = "Part C"
}

func (b *ConcreteBuilder) GetResult() Product {
	return b.product
}

// Director constructs a Product using the Builder interface
type Director struct {
	builder Builder
}

func (d *Director) Construct() {
	d.builder.SetPartA()
	d.builder.SetPartB()
	d.builder.SetPartC()
}

func main() {
	builder := &ConcreteBuilder{}
	director := Director{builder}
	director.Construct()
	product := builder.GetResult()
	fmt.Printf("Product: %+v\n", product)
}
```

[Go Playground Buider](https://go.dev/play/p/4JEVkO-zohk)