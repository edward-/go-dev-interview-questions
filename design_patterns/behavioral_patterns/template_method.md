# Template Method Design Pattern

## What is the Template Method design pattern?

Template Method is a behavioral design pattern that defines the skeleton of an algorithm in the superclass but lets subclasses override specific steps of the algorithm without changing its structure.

The Template Method design pattern defines the skeleton of an algorithm in a base class and lets subclasses override specific steps of the algorithm without changing its structure.

## What are the key components of the Template Method design pattern?

- Abstract Class: Contains the template method and defines the abstract steps of the algorithm.
- Concrete Class: Implements the abstract steps defined in the abstract class.

## When should the Template Method design pattern be used?
When you have an algorithm that can be broken into steps, and you want to allow subclasses to provide specific implementations for one or more of these steps without altering the algorithm's structure.
When you want to avoid code duplication by sharing common parts of the implementation in a base class.

## What are the advantages of using the Template Method design pattern?

- Promotes code reuse and avoids code duplication.
- Simplifies the algorithm structure by defining common steps in a base class.
- Allows subclasses to define specific behaviors while adhering to a common interface.

## What are the disadvantages of using the Template Method design pattern?
- Can lead to an increase in the number of classes, which might complicate the class hierarchy.
- Subclassing can make the code more rigid and less flexible to changes.

## How does the Template Method pattern differ from the Strategy pattern?
The Template Method pattern defines an algorithm's structure in a base class and lets subclasses implement specific steps. The algorithm's skeleton is defined once in the base class.
The Strategy pattern defines a family of algorithms, encapsulates each one, and makes them interchangeable. The client can choose which algorithm to use at runtime.

## Can the Template Method pattern be combined with other patterns?
Yes, the Template Method pattern can be combined with other patterns like Factory Method, Strategy, and Composite to solve more complex design problems and enhance flexibility.

# Example 

```go
package main

import "fmt"

// Template Method
type IGame interface {
	Initialize()
	StartPlay()
	EndPlay()
}

type Game struct {
	igame IGame
}

func (g *Game) Play() {
	g.igame.Initialize()
	g.igame.StartPlay()
	g.igame.EndPlay()
}

// Concrete class
type Football struct {
	Game
}

func (f *Football) Initialize() {
	fmt.Println("Football Game Initialized! Start playing.")
}

func (f *Football) StartPlay() {
	fmt.Println("Football Game Started. Enjoy the game!")
}

func (f *Football) EndPlay() {
	fmt.Println("Football Game Finished!")
}

func main() {
	football := &Football{}
	g := Game{
		igame: football,
	}

	g.Play()
}
```

[Go Playground Template Method](https://go.dev/play/p/Hik9XmW-fnD)