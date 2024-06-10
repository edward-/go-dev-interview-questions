# Memento Design Pattern

# What is the Memento design pattern?
Memento is a behavioral design pattern that lets you save and restore the previous state of an object without revealing the details of its implementation.

## What are the main components of the Memento design pattern?
Memento: Stores the internal state of the Originator object. It can have a narrow or wide interface.
Originator: Creates a memento containing a snapshot of its current internal state and uses the memento to restore its internal state.
Caretaker: Responsible for the memento's safekeeping and doesn't modify or inspect its contents.

## When should you use the Memento pattern?
- When you need to save and restore the state of an object.
- When you want to provide undo/redo functionality.
- When you need to preserve the encapsulation of an object’s state.

## What are the advantages of using the Memento pattern?
- Encapsulation: It keeps the Originator's state encapsulated.
- Simplifies the Originator: The Originator handles only its state; the Caretaker handles the mementos.

## What are the disadvantages of using the Memento pattern?
- Memory Overhead: Storing mementos can be expensive if the Originator's state is large or if there are many mementos.
- Serialization Issues: Care must be taken when storing state that includes references to other objects.

## How does the Memento pattern compare to the Command pattern?
- The Memento pattern is mainly used to capture and restore an object's state, focusing on state management.
- The Command pattern is used to encapsulate a request as an object, allowing parameterization and queuing of requests, and supporting undo/redo operations.

## Can the Memento pattern violate encapsulation?
No, one of the main benefits of the Memento pattern is that it preserves encapsulation. The internal state is only accessible to the Originator and not to other objects, maintaining the integrity of the state management.

## How do you handle large state objects with the Memento pattern?
Use optimizations such as storing only deltas (changes) instead of complete states, or implementing a strategy to manage memory usage, such as limiting the number of stored mementos or compressing the state data.

## What are some real-world examples of the Memento pattern?
- Undo/redo functionality in text editors and graphic design software.
- State checkpoints in games.
- Transactional memory in database systems.

# Example

```go
package main

import "fmt"

// Memento stores the state of the Originator
type Memento struct {
    state string
}

// Originator creates a memento containing its current state
// and uses the memento to restore its state.
type Originator struct {
    state string
}

func (o *Originator) SaveState() Memento {
    return Memento{state: o.state}
}

func (o *Originator) RestoreState(m Memento) {
    o.state = m.state
}

func (o *Originator) SetState(state string) {
    o.state = state
}

func (o *Originator) GetState() string {
    return o.state
}

// Caretaker keeps track of the originator's mementos
type Caretaker struct {
    mementos []Memento
}

func (c *Caretaker) AddMemento(m Memento) {
    c.mementos = append(c.mementos, m)
}

func (c *Caretaker) GetMemento(index int) Memento {
    return c.mementos[index]
}

func main() {
    originator := &Originator{}
    caretaker := &Caretaker{}

    originator.SetState("State 1")
    caretaker.AddMemento(originator.SaveState())

    originator.SetState("State 2")
    caretaker.AddMemento(originator.SaveState())

    originator.SetState("State 3")
    fmt.Println("Current State:", originator.GetState())

    originator.RestoreState(caretaker.GetMemento(1))
    fmt.Println("Restored to State:", originator.GetState())

    originator.RestoreState(caretaker.GetMemento(0))
    fmt.Println("Restored to State:", originator.GetState())
}
```

[Go Playground Memento](https://go.dev/play/p/uzlGcN5nP66)