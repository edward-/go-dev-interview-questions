# Prototipe Design Pattern

## What is the Prototype design pattern?
The Prototype design pattern is a creational design pattern used to create new objects by copying an existing object, known as the prototype. It involves implementing a prototype interface that specifies a method for cloning objects.

## When should I use the Prototype design pattern?
The Prototype pattern is useful when:

The cost of creating a new object is expensive or complicated.
You need to reduce the number of subclasses required to create an object.
You need to create new instances of objects at runtime without knowing the exact types and classes.

## What are the benefits of the Prototype design pattern?
Reduces the need for subclassing.
Hides the complexities of object creation.
Allows adding or removing objects at runtime.
Provides a way to specify new objects by copying existing ones.

## What are the potential drawbacks of using the Prototype design pattern?
Cloning complex objects that have circular references can be tricky.
Requires implementing a cloning method, which might be complex for some objects.
Shallow copy vs. deep copy issues need to be handled carefully.

## How does the Prototype design pattern differ from other creational patterns like Factory Method or Abstract Factory?
Factory Method: Defines an interface for creating an object but lets subclasses alter the type of objects that will be created.
Abstract Factory: Provides an interface for creating families of related or dependent objects without specifying their concrete classes.
Prototype: Creates objects by cloning an existing object (prototype).

## What is a shallow copy and a deep copy in the context of the Prototype design pattern?
Shallow Copy: Copies all the field values. If the field value is a reference to an object, only the reference is copied, hence both the original and the copy refer to the same object.
Deep Copy: Copies all fields, and if a field is a reference to an object, it creates a new copy of the referenced object, so the original and the copy do not share the same reference.

## How does the Prototype pattern handle complex object structures?
For complex objects, each nested object within the structure must also implement the Clone method. The main object's Clone method should call the Clone method of the nested objects to ensure a deep copy is performed.

## Are there any real-world examples where the Prototype pattern is used?
The Prototype pattern is used in situations such as:

Copying configurations or settings objects.
Cloning documents in document management systems.
Game development, where multiple similar objects like enemies or obstacles need to be created.


# Example

```go
package main

import (
	"fmt"
)

// Cloneable is the prototype interface that defines a clone method.
type Cloneable interface {
	Clone() Cloneable
}

// ConcretePrototype1 is a concrete implementation of Cloneable.
type ConcretePrototype1 struct {
	Field1 string
	Field2 int
}

func (p *ConcretePrototype1) Clone() Cloneable {
	return &ConcretePrototype1{
		Field1: p.Field1,
		Field2: p.Field2,
	}
}

func main() {
	prototype := &ConcretePrototype1{
		Field1: "example",
		Field2: 42,
	}

	// Create a clone of the prototype
	clone := prototype.Clone().(*ConcretePrototype1)

	fmt.Printf("Original: %+v\n", prototype)
	fmt.Printf("Clone: %+v\n", clone)
}
```

[Go Playground Prototipe](https://go.dev/play/p/WYfkq7g2j4G)