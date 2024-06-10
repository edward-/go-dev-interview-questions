# Bridge Design Pattern

## What is the Bridge design pattern?
The Bridge design pattern is a structural design pattern that aims to decouple an abstraction from its implementation, allowing the two to vary independently. This pattern involves an interface that acts as a bridge, making the functionality of concrete classes independent from the interface implementer classes.

## When should I use the Bridge design pattern?
The Bridge pattern is particularly useful when:

You want to avoid a permanent binding between an abstraction and its implementation.
Both the abstractions and their implementations should be extensible by subclassing.
Changes in the implementation should have no impact on clients using the abstraction.
You want to share an implementation among multiple objects.

## How does the Bridge design pattern differ from the Adapter pattern?
- Bridge: Used to separate an abstraction from its implementation so that both can be modified independently.
- Adapter: Used to make incompatible interfaces compatible without changing their code.

## What are the components of the Bridge design pattern?
The Bridge pattern involves the following components:

- Abstraction: Defines the abstraction's interface and maintains a reference to an object of type Implementor.
- Refined Abstraction: Extends the interface defined by Abstraction.
- Implementor: Defines the interface for implementation classes.
- Concrete Implementor: Implements the Implementor interface and defines its concrete implementation.

## How does the Bridge pattern help in reducing code complexity?
The Bridge pattern helps in reducing code complexity by:

- Allowing the separation of concerns. Abstraction and implementation can be developed independently.
- Reducing the number of subclasses needed to achieve a flexible design.
- Making it easier to add new implementations or abstractions without affecting the existing codebase.

## What are some real-world scenarios where the Bridge pattern can be applied?
GUI Toolkits: Decoupling the interface of the toolkit from its underlying operating system-specific implementation.
Database Drivers: Decoupling database access logic from specific database driver implementations.
Logging Frameworks: Separating logging interfaces from their concrete logging implementation (e.g., file log, database log).

## What are the benefits of using the Bridge design pattern?
Decoupling Interface and Implementation: Facilitates independent development of interface and implementation.
Increased Flexibility: Enhances code flexibility by allowing the abstraction and the implementation to evolve independently.
Improved Scalability: Makes it easier to extend the system by adding new abstractions and implementations without modifying existing code.

## Are there any drawbacks to using the Bridge design pattern?
- Complexity: Increases the number of classes and interfaces, which can make the system more complex.
- Initial Setup: Requires careful planning and setup to correctly identify and separate abstraction from implementation.

## How does the Bridge pattern relate to other design patterns?
- Adapter: Both involve abstraction, but Adapter is focused on converting one interface to another, while Bridge separates an abstraction from its implementation.
- Strategy: Strategy pattern encapsulates algorithms, while Bridge decouples an abstraction from its implementation.
- Abstract Factory: Can work alongside the Bridge pattern to create implementations of the bridge interface.

# Example

```go
package main

import "fmt"

// Implementor
type MessageSender interface {
	SendMessage(message string) string
}

// Concrete Implementor 1
type EmailSender struct{}

func (e *EmailSender) SendMessage(message string) string {
	return "Email: " + message
}

// Concrete Implementor 2
type SmsSender struct{}

func (s *SmsSender) SendMessage(message string) string {
	return "SMS: " + message
}

// Abstraction
type Message struct {
	sender MessageSender
}

func (m *Message) Send(message string) string {
	return m.sender.SendMessage(message)
}

// Refined Abstraction
type UrgentMessage struct {
	Message
}

func (u *UrgentMessage) Send(message string) string {
	return "Urgent: " + u.sender.SendMessage(message)
}

func main() {
	email := &EmailSender{}
	sms := &SmsSender{}

	msg := &Message{sender: email}
	fmt.Println(msg.Send("Hello"))

	urgentMsg := &UrgentMessage{Message{sender: sms}}
	fmt.Println(urgentMsg.Send("Hello"))
}
```

[Go Playground Bridge](https://go.dev/play/p/NBE_mX4XXld)