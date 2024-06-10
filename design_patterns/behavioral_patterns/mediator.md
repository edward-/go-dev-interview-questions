# Mediator Design Pattern 

## What is Mediatot Design Pattern?
Mediator is a behavioral design pattern that lets you reduce chaotic dependencies between objects. The pattern restricts direct communications between the objects and forces them to collaborate only via a mediator object.

## When should the Mediator pattern be used?
The Mediator pattern should be used when:

- A set of objects communicate in complex but well-defined ways.
- Reuse is difficult because the interactions between objects are entangled.
- You want to customize a behavior that’s distributed between several objects without a lot of subclassing.
- You need to reduce the dependencies between communicating objects, leading to a more maintainable system.

## What are the main components of the Mediator pattern?
The main components of the Mediator pattern include:

- Mediator Interface: Declares a method for communicating with Colleague objects.
- Concrete Mediator: Implements the Mediator interface and coordinates communication between Colleague objects.
- Colleague Class: Each Colleague communicates with its Mediator whenever it would have otherwise communicated with another Colleague.

## What are the advantages of using the Mediator pattern?
The advantages include:

- Reduced Class Interdependencies: Classes are not aware of each other and only interact through the mediator.
- Simplified Communication: Reduces the number of communication pathways, making the system easier to understand and maintain.
- Flexible Code: Changes to communication logic can be made in one place (the mediator) rather than across multiple classes.

## What are the disadvantages of the Mediator pattern?
The disadvantages include:

Mediator Complexity: The Mediator can become complex and difficult to maintain as it centralizes the communication logic.
Potential Overhead: If the mediator handles many interactions, it can become a performance bottleneck.

## How is the Mediator pattern different from the Observer pattern?
The Mediator pattern centralizes communication among a set of objects, while the Observer pattern defines a one-to-many dependency between objects so that when one object changes state, all its dependents are notified and updated automatically. The key difference is that the Mediator involves explicit communication through a mediator object, whereas the Observer involves implicit notification.

## How does the Mediator pattern enhance testability?
The Mediator pattern enhances testability by isolating the communication logic within the mediator. This makes it easier to test the communication in isolation without involving the complex interactions between different colleague objects.

# Example

```go
package main

import "fmt"

// Mediator interface
type Mediator interface {
	SendMessage(msg string, colleague Colleague)
}

// Colleague interface
type Colleague interface {
	SetMediator(mediator Mediator)
	Send(msg string)
	Receive(msg string)
}

// ConcreteMediator implements the Mediator interface
type ConcreteMediator struct {
	colleague1 Colleague
	colleague2 Colleague
}

func (m *ConcreteMediator) SetColleague1(colleague Colleague) {
	m.colleague1 = colleague
}

func (m *ConcreteMediator) SetColleague2(colleague Colleague) {
	m.colleague2 = colleague
}

func (m *ConcreteMediator) SendMessage(msg string, colleague Colleague) {
	if colleague == m.colleague1 {
		m.colleague2.Receive(msg)
	} else {
		m.colleague1.Receive(msg)
	}
}

// ConcreteColleague1 implements the Colleague interface
type ConcreteColleague1 struct {
	mediator Mediator
}

func (c *ConcreteColleague1) SetMediator(mediator Mediator) {
	c.mediator = mediator
}

func (c *ConcreteColleague1) Send(msg string) {
	fmt.Printf("Colleague1 sending message: %s\n", msg)
	c.mediator.SendMessage(msg, c)
}

func (c *ConcreteColleague1) Receive(msg string) {
	fmt.Printf("Colleague1 received message: %s\n", msg)
}

// ConcreteColleague2 implements the Colleague interface
type ConcreteColleague2 struct {
	mediator Mediator
}

func (c *ConcreteColleague2) SetMediator(mediator Mediator) {
	c.mediator = mediator
}

func (c *ConcreteColleague2) Send(msg string) {
	fmt.Printf("Colleague2 sending message: %s\n", msg)
	c.mediator.SendMessage(msg, c)
}

func (c *ConcreteColleague2) Receive(msg string) {
	fmt.Printf("Colleague2 received message: %s\n", msg)
}

func main() {
	mediator := &ConcreteMediator{}

	colleague1 := &ConcreteColleague1{}
	colleague2 := &ConcreteColleague2{}

	colleague1.SetMediator(mediator)
	colleague2.SetMediator(mediator)

	mediator.SetColleague1(colleague1)
	mediator.SetColleague2(colleague2)

	colleague1.Send("Hello, Colleague2!")
	colleague2.Send("Hi, Colleague1!")
}

```