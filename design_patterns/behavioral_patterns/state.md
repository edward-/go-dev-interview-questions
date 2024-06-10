# State Design Pattern

## What is the State design pattern?
State is a behavioral design pattern that lets an object alter its behavior when its internal state changes. It appears as if the object changed its class.

## When should I use the State design pattern?

Use the State pattern when an object's behavior depends on its state, and it must change behavior at runtime depending on that state.
It is particularly useful when you have a lot of conditional logic related to state-specific behavior.

## What are the key components of the State design pattern?
- Context: The class that has a state object representing the current state.
- State Interface: An interface or abstract class that defines the behavior associated with a state.
- Concrete States: Classes that implement the state interface and provide specific behavior for each state.

## How does the State pattern improve code maintainability?
By encapsulating state-specific behavior into separate classes, the State pattern simplifies the context class and makes the code easier to maintain and extend.

## Can you give a real-world example of the State design pattern?
A common example is a TCP connection that can be in different states (e.g., Established, Listening, Closed) and has different behaviors depending on its state.
Another example is a media player that can be in states like Playing, Paused, or Stopped.

## How does the State pattern differ from the Strategy pattern?
While both patterns encapsulate behaviors, the State pattern is used for state-specific behavior changes at runtime, whereas the Strategy pattern is used to choose an algorithm at runtime. The State pattern involves state transitions, whereas the Strategy pattern does not.

## What are the advantages of using the State design pattern?
- Simplifies the context: Reduces complexity by eliminating conditional statements for state-specific behavior.
- Encapsulation: Encapsulates state-specific behavior in separate classes.
- Flexibility: Makes it easy to add new states without changing the context class.

## What are the disadvantages of using the State design pattern?

- Increased number of classes: The pattern requires creating a class for each state, which can increase the number of classes in the system.
- Overhead: May introduce overhead if the state transitions are frequent or if the state classes have significant overhead.


## How does the State pattern handle state transitions?
State transitions are handled by changing the current state object within the context. Each state object can define the logic for transitions.

# Example

```go
package main

import "fmt"

// State interface
type State interface {
    DoAction(context *Context)
}

// Concrete States
type StartState struct{}
type StopState struct{}

func (s *StartState) DoAction(context *Context) {
    fmt.Println("Player is in start state")
    context.SetState(s)
}

func (s *StopState) DoAction(context *Context) {
    fmt.Println("Player is in stop state")
    context.SetState(s)
}

// Context
type Context struct {
    state State
}

func (c *Context) SetState(state State) {
    c.state = state
}

func (c *Context) GetState() State {
    return c.state
}

func main() {
    context := &Context{}

    startState := &StartState{}
    startState.DoAction(context)

    fmt.Println("Current state:", context.GetState())

    stopState := &StopState{}
    stopState.DoAction(context)

    fmt.Println("Current state:", context.GetState())
}
```

[Go Playground State](https://go.dev/play/p/TJOH6WzPBqM)