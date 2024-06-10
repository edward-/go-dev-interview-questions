# Factory Method Design Pattern

## What is the Factory Method design pattern?
The Factory Method is a creational design pattern that defines an interface for creating an object but allows subclasses to alter the type of objects that will be created. Instead of calling a constructor directly, clients call a factory method, which abstracts the creation process.

## What problem does the Factory Method design pattern solve?
The Factory Method pattern solves the problem of creating objects without specifying the exact class of the object that will be created. This promotes loose coupling by allowing the client code to work with abstract interfaces rather than concrete implementations.

## How does the Factory Method pattern differ from the Abstract Factory pattern?
The Factory Method pattern involves a single method that creates objects, while the Abstract Factory pattern provides an interface for creating families of related or dependent objects without specifying their concrete classes. The Factory Method is more focused on a single object creation, whereas Abstract Factory deals with multiple related objects.

## When should you use the Factory Method pattern?
You should use the Factory Method pattern when:

- A class can't anticipate the type of objects it needs to create.
- A class wants its subclasses to specify the objects it creates.
- You want to localize the creation of objects to maintain the flexibility and extendability of the code.

## What are the benefits of using the Factory Method pattern?
- Encapsulation of object creation: The factory method encapsulates the creation of objects, which helps manage and maintain the codebase.
- Flexibility and scalability: Subclasses can specify the type of objects they create, making it easy to extend and add new types without modifying existing code.
- Loose coupling: Clients work with interfaces rather than concrete classes, reducing dependencies and enhancing maintainability.

## What are the potential drawbacks of using the Factory Method pattern?
- Complexity: The pattern can introduce additional complexity to the codebase, especially when dealing with a large number of concrete products and creators.
- Overhead: It may add an extra layer of abstraction that might not be necessary for simple applications.

## How does the Factory Method pattern promote the Open/Closed Principle?
The Factory Method pattern promotes the Open/Closed Principle by allowing the creation of new types of products through subclassing without modifying the existing code. The code that uses the factory remains unchanged, and new product types can be added by creating new subclasses.

# Example 

```go
package main

import "fmt"

// Product is the interface that all products should implement
type Product interface {
	Use() string
}

// ConcreteProductA is one implementation of the Product interface
type ConcreteProductA struct{}

func (p ConcreteProductA) Use() string {
	return "Using product A"
}

// ConcreteProductB is another implementation of the Product interface
type ConcreteProductB struct{}

func (p ConcreteProductB) Use() string {
	return "Using product B"
}

// Creator is the abstract factory with a factory method
type Creator interface {
	CreateProduct() Product
}

// ConcreteCreatorA is a concrete factory that creates ConcreteProductA
type ConcreteCreatorA struct{}

func (c ConcreteCreatorA) CreateProduct() Product {
	return ConcreteProductA{}
}

// ConcreteCreatorB is a concrete factory that creates ConcreteProductB
type ConcreteCreatorB struct{}

func (c ConcreteCreatorB) CreateProduct() Product {
	return ConcreteProductB{}
}

func main() {
	var creator Creator

	creator = ConcreteCreatorA{}
	productA := creator.CreateProduct()
	fmt.Println(productA.Use())

	creator = ConcreteCreatorB{}
	productB := creator.CreateProduct()
	fmt.Println(productB.Use())
}
```

[Go Playground Factory Method](https://go.dev/play/p/xaX5hUsSW1Y)