# Chain of Responsibility Design Pattern

## What is the Chain of Responsibility design pattern?
Chain of Responsibility is a behavioral design pattern that lets you pass requests along a chain of handlers. Upon receiving a request, each handler decides either to process the request or to pass it to the next handler in the chain.

## When should the Chain of Responsibility pattern be used?
The pattern should be used when:
- There are multiple objects that can handle a request, and the handler is determined at runtime.
- You want to decouple the sender and receiver of a request.
- You want to simplify the object by removing conditional statements for handling the request.

## What are the main components of the Chain of Responsibility pattern?
The main components are:
- **Handler**: An interface or abstract class defining a method for handling requests.
- **Concrete Handler**: A class that implements the handler interface and processes the request or passes it to the next handler.
- **Client**: The object that initiates the request.

## How does the Chain of Responsibility pattern work?
A client sends a request to a handler. If the handler can process the request, it does so; otherwise, it forwards the request to the next handler in the chain. This continues until a handler processes the request or the end of the chain is reached.

## What are the benefits of using the Chain of Responsibility pattern?
- **Decoupling**: The sender and receiver of a request are decoupled.
- **Flexibility**: New handlers can be added to the chain without modifying existing code.
- **Simplified Code**: Reduces the need for complex conditional statements in request handling.

## What are the drawbacks of the Chain of Responsibility pattern?
- **No Guarantee of Handling**: There's no guarantee that a request will be handled if no handler in the chain processes it.
- **Debugging Difficulty**: Can be harder to debug due to the dynamic nature of the handler chain.

## How can you ensure a request gets handled if no handler in the chain processes it?
You can add a default handler at the end of the chain to handle requests that no other handlers process. This ensures that every request gets handled.

## Can the Chain of Responsibility pattern be combined with other patterns?
Yes, it can be combined with other patterns such as the Command pattern, Composite pattern, and others to create more flexible and reusable solutions.

## What are some real-world examples of the Chain of Responsibility pattern?
- Event Handling Systems: GUI frameworks often use this pattern to handle events.
- Logging: Multiple logging handlers can process log messages.
- Customer Support: Support tickets passed through different levels of support.



# Example

```go
package main

import "fmt"

// Handler defines the interface for handling requests.
type Handler interface {
	SetNext(handler Handler)
	Handle(request string)
}

// BaseHandler provides default behavior for chaining handlers.
type BaseHandler struct {
	next Handler
}

func (h *BaseHandler) SetNext(handler Handler) {
	h.next = handler
}

func (h *BaseHandler) Handle(request string) {
	if h.next != nil {
		h.next.Handle(request)
		return
	}
	fmt.Println("No handler is available to manage the request ", request)
}

// ConcreteHandlerA handles requests it is interested in.
type ConcreteHandlerA struct {
	BaseHandler
}

func (h *ConcreteHandlerA) Handle(request string) {
	if request == "A" {
		fmt.Println("ConcreteHandlerA handled the request.")
	} else {
		h.BaseHandler.Handle(request)
	}
}

// ConcreteHandlerB handles requests it is interested in.
type ConcreteHandlerB struct {
	BaseHandler
}

func (h *ConcreteHandlerB) Handle(request string) {
	if request == "B" {
		fmt.Println("ConcreteHandlerB handled the request.")
	} else {
		h.BaseHandler.Handle(request)
	}
}

func main() {
	handlerA := &ConcreteHandlerA{}
	handlerB := &ConcreteHandlerB{}

	handlerA.SetNext(handlerB)

	requests := []string{"A", "B", "C"}

	for _, request := range requests {
		handlerA.Handle(request)
	}
}
```


[Go Playground Chain Of Responsability](https://go.dev/play/p/brPWlK1DUMT)