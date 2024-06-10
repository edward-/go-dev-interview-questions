# Flyweight Design Pattern

## What is the Flyweight design pattern?
Flyweight is a structural design pattern that lets you fit more objects into the available amount of RAM by sharing common parts of state between multiple objects instead of keeping all of the data in each object.

## When should you use the Flyweight design pattern?
The Flyweight pattern should be used when:

- An application uses a large number of objects.
- The memory footprint of many objects is affecting performance.
- Most object states can be made extrinsic and shared across multiple objects.

## What are intrinsic and extrinsic states in the Flyweight pattern?
Intrinsic State: This is the state that is shared and stored in the Flyweight object. It is independent and remains constant.
Extrinsic State: This is the state that is not shared and varies with each object. It is passed to the Flyweight object when needed.

## What are the benefits of using the Flyweight pattern?
- Reduced Memory Usage: By sharing common data, memory usage is significantly reduced.
- Improved Performance: With less memory usage, the performance of the application can improve.
- Consistency: Shared state ensures consistency across similar objects.

## What are the downsides of the Flyweight pattern?
- Complexity: Increased complexity in managing shared and unique states.
- Tight Coupling: Clients and flyweights may become tightly coupled due to the need to maintain extrinsic state externally.

## How does the Flyweight pattern differ from other structural patterns?
The Flyweight pattern specifically focuses on sharing data to reduce memory usage, whereas other structural patterns like Adapter, Decorator, or Composite focus on different aspects such as interface compatibility, adding behavior, or tree structures, respectively.

## What is a real-world example of the Flyweight pattern?
A common real-world example is text editors. In a text editor, characters (glyphs) are often represented as flyweights to minimize memory usage by sharing character formatting information (intrinsic state) while the position of characters in the document (extrinsic state) is maintained separately.

## What are some common use cases of the Flyweight pattern?
- Rendering a large number of similar objects in graphical applications.
- Handling a large number of connections in network applications.
- Representing large datasets with many duplicate values efficiently.

## How do you ensure thread safety in the Flyweight pattern?
Ensure that the shared Flyweight objects are immutable or use appropriate synchronization mechanisms when accessing mutable shared state. This can include using locks or concurrent data structures.

# Example

```go
package main

import (
	"fmt"
)

// Flyweight interface
type Flyweight interface {
	Operation(extrinsicState string)
}

// ConcreteFlyweight is the concrete implementation of Flyweight
type ConcreteFlyweight struct {
	intrinsicState string
}

func (f *ConcreteFlyweight) Operation(extrinsicState string) {
	fmt.Printf("Intrinsic State: %s, Extrinsic State: %s\n", f.intrinsicState, extrinsicState)
}

// FlyweightFactory creates and manages flyweights
type FlyweightFactory struct {
	flyweights map[string]*ConcreteFlyweight
}

func NewFlyweightFactory() *FlyweightFactory {
	return &FlyweightFactory{
		flyweights: make(map[string]*ConcreteFlyweight),
	}
}

func (f *FlyweightFactory) GetFlyweight(key string) *ConcreteFlyweight {
	flyweight, exists := f.flyweights[key]
	if !exists {
		flyweight = &ConcreteFlyweight{intrinsicState: key}
		f.flyweights[key] = flyweight
	}
	return flyweight
}

func main() {
	factory := NewFlyweightFactory()

	flyweight1 := factory.GetFlyweight("state1")
	flyweight1.Operation("extrinsic1")

	flyweight2 := factory.GetFlyweight("state2")
	flyweight2.Operation("extrinsic2")

	flyweight3 := factory.GetFlyweight("state1")
	flyweight3.Operation("extrinsic3")

	fmt.Printf("Flyweight1 and Flyweight3 are the same instance: %v\n", flyweight1 == flyweight3)
}

```

[Go Playground Flyweight](https://go.dev/play/p/kf2LL8oiBrl)