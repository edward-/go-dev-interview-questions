# Decorator Design Pattern

## What is the Decorator Design Pattern?
The Decorator pattern is a structural pattern that allows behavior to be added to individual objects, dynamically, without affecting the behavior of other objects from the same class. It’s often used to adhere to the Single Responsibility Principle, as it allows functionality to be divided between classes with unique areas of concern.

## When should I use the Decorator pattern?
You should use the Decorator pattern when:

You need to add responsibilities to individual objects dynamically and transparently, that is, without affecting other objects.
You need to add functionality to an object that can be withdrawn.
Extension by subclassing is impractical. Sometimes a large number of independent extensions are possible, and would produce an explosion of subclasses to support every combination.

## How does the Decorator pattern differ from inheritance?
The Decorator pattern uses composition instead of inheritance to extend the functionality of objects. While inheritance extends a class by creating a new class, the Decorator pattern wraps the original class with a new class that provides the additional functionality.

## What are the components of the Decorator pattern?
The Decorator pattern has four main components:

Component: The interface or abstract class defining the methods that will be implemented.
ConcreteComponent: The class that implements the Component interface.
Decorator: An abstract class that implements the Component interface and has a reference to a Component object.
ConcreteDecorator: Classes that extend the Decorator class to add functionalities to the Component.

## What are the advantages of the Decorator pattern?
- Flexibility: You can mix and match different decorators to create combinations of functionalities at runtime.
- Open/Closed Principle: You can extend an object's behavior without modifying the original object's code.
- Single Responsibility Principle: Functionality is added in a way that each class has a single concern.

## What are the disadvantages of the Decorator pattern?
- Complexity: It can result in a system with many small classes that are hard to understand and manage.
- Debugging: It can be difficult to debug since there are many layers of wrapping.

## Can the Decorator pattern be used with any object-oriented language?
Yes, the Decorator pattern can be implemented in any object-oriented language that supports interfaces or abstract classes and object composition.

# Example 

```go
package main

import (
	"fmt"
)

// Component interface
type Coffee interface {
	GetCost() int
	GetDescription() string
}

// ConcreteComponent
type SimpleCoffee struct{}

func (c *SimpleCoffee) GetCost() int {
	return 5
}

func (c *SimpleCoffee) GetDescription() string {
	return "Simple coffee"
}

// Decorator
type CoffeeDecorator struct {
	Coffee
}

func (d *CoffeeDecorator) GetCost() int {
	return d.Coffee.GetCost()
}

func (d *CoffeeDecorator) GetDescription() string {
	return d.Coffee.GetDescription()
}

// Concrete Decorators
type MilkDecorator struct {
	CoffeeDecorator
}

func (m *MilkDecorator) GetCost() int {
	return m.Coffee.GetCost() + 2
}

func (m *MilkDecorator) GetDescription() string {
	return m.Coffee.GetDescription() + ", milk"
}

type SugarDecorator struct {
	CoffeeDecorator
}

func (s *SugarDecorator) GetCost() int {
	return s.Coffee.GetCost() + 1
}

func (s *SugarDecorator) GetDescription() string {
	return s.Coffee.GetDescription() + ", sugar"
}

func main() {
	coffee := &SimpleCoffee{}
	fmt.Println(coffee.GetDescription(), ":", coffee.GetCost())

	milkCoffee := &MilkDecorator{CoffeeDecorator{coffee}}
	fmt.Println(milkCoffee.GetDescription(), ":", milkCoffee.GetCost())

	sugarMilkCoffee := &SugarDecorator{CoffeeDecorator{milkCoffee}}
	fmt.Println(sugarMilkCoffee.GetDescription(), ":", sugarMilkCoffee.GetCost())
}
```

[Go Playground Decorator](https://go.dev/play/p/41CXxqur0z5)