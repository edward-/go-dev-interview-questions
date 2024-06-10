# Adapte Design Pattern

## What is the Adapter design pattern?
The Adapter design pattern is a structural pattern that allows two incompatible interfaces to work together. It acts as a bridge between two interfaces, converting one interface into another.

## Why would you use the Adapter pattern?
- To integrate classes that wouldn't otherwise work together due to incompatible interfaces.
- To reuse existing classes without modifying their source code.
- To achieve a higher level of flexibility and decoupling in your code.

## What are the main components of the Adapter pattern?
- Target: Defines the domain-specific interface that the client uses.
- Adapter: Adapts the interface of the Adaptee to the Target interface.
- Adaptee: Defines an existing interface that needs adapting.
- Client: Collaborates with objects conforming to the Target interface.

## What are the types of Adapter patterns?
Class Adapter: Uses multiple inheritance to adapt one interface to another.
Object Adapter: Uses composition to adapt one interface to another.

## What are the advantages of using the Adapter pattern?
- Flexibility: Allows objects with incompatible interfaces to work together.
- Reusability: Enables the reuse of existing functionalities in new contexts without altering the existing code.
- Separation of Concerns: Helps in decoupling the client code from the interface that needs to be adapted.

## What are the potential drawbacks of the Adapter pattern?
- Complexity: Adds an extra layer of abstraction, which can make the code more complex and harder to understand.
- Overhead: The adapter adds a level of indirection, which can introduce slight performance overhead.

## When should you avoid using the Adapter pattern?
When the existing interface can be modified directly to suit the new requirements.
When performance is critical, and the added indirection of the Adapter pattern could introduce unnecessary overhead.

## Can you give a real-world example of the Adapter pattern?
Legacy System Integration: Suppose you have a legacy system that provides data in XML format, but your new application expects JSON. An Adapter can be created to convert XML data into JSON format so that the new application can consume it seamlessly.

## What is the difference between the Adapter pattern and the Facade pattern?
The Adapter pattern changes the interface of an existing object to make it compatible with another interface.
The Facade pattern provides a simplified interface to a complex subsystem without modifying the subsystem itself.

## How does the Adapter pattern relate to dependency injection?
The Adapter pattern can be used in conjunction with dependency injection to inject dependencies that conform to a specific interface, thus allowing for flexible swapping of implementations.

## What are some common pitfalls when implementing the Adapter pattern?
- Overusing the Adapter: Relying too heavily on Adapters can lead to a system that's hard to maintain.
- Poor Performance: The additional layer introduced by the Adapter can lead to performance issues if not used judiciously.
- Incompatibility: Ensuring that the adapted interface correctly matches the expected interface can be challenging and may introduce bugs.

# Example

```go
package main

import "fmt"

// Target interface
type Target interface {
	Request() string
}

// Adaptee interface
type Adaptee interface {
	SpecificRequest() string
}

// Concrete Adaptee
type ConcreteAdaptee struct{}

func (a *ConcreteAdaptee) SpecificRequest() string {
	return "Specific request"
}

// Adapter
type Adapter struct {
	adaptee Adaptee
}

func (a *Adapter) Request() string {
	return a.adaptee.SpecificRequest()
}

func main() {
	adaptee := &ConcreteAdaptee{}
	adapter := &Adapter{adaptee: adaptee}
	fmt.Println(adapter.Request())
}
```

[Go Palyground Adapter](https://go.dev/play/p/z1NV-yjFDNU)