# Singleton Design Pattern

## What is the Singleton design pattern?
The Singleton pattern ensures that a class has only one instance and provides a global point of access to that instance.

## Why use the Singleton pattern?
It is used to control access to a shared resource, such as a database connection or a file, ensuring that only one instance of the resource is created and used throughout the application.

## What are the key characteristics of the Singleton pattern?
- Single instance: Only one instance of the class exists.
- Global access: The single instance is accessible globally.
- Lazy initialization: The instance is created only when it is needed.

## What are the benefits of using the Singleton pattern?
- Controlled access to the single instance.
- Reduced memory footprint since only one instance is created.
- Provides a single point of access to a resource.

## What are the drawbacks of the Singleton pattern?
- It can introduce global state into an application, making it harder to manage.
- It can make unit testing difficult because it introduces tight coupling and makes dependency injection challenging.
- If not implemented correctly, it can lead to issues in multi-threaded environments.

## How can you ensure thread safety in a Singleton implementation?
In Go, you can use the sync.Once type to ensure that the initialization code is executed only once, regardless of how many goroutines are attempting to access the Singleton instance.

## When should you avoid using the Singleton pattern?
Avoid using Singleton if you need multiple instances of a class.
If the Singleton holds state that can change over time, it may lead to unexpected behaviors.
If it introduces tight coupling and makes your codebase harder to maintain and test.

## Can a Singleton be subclassed?
Subclassing a Singleton can be tricky and is generally discouraged because it can defeat the purpose of having a single instance and complicate the design.

## How does Singleton differ from other creational patterns?
Singleton ensures a class has only one instance and provides a global point of access to it, while other creational patterns like Factory Method or Abstract Factory focus on creating families of related objects without specifying their concrete classes.

# Example

```go
package main

import (
	"fmt"
	"sync"
)

type Singleton struct {
	// Fields
	Value int
}

var (
	instance *Singleton
	once     sync.Once
)

func GetInstance() *Singleton {
	once.Do(func() {
		instance = &Singleton{}
	})
	return instance
}

func main() {
	i1 := GetInstance()
	i2 := GetInstance()

	i1.Value = 10
	i2.Value = 20
	fmt.Println(i1)
	fmt.Println(i2)
}

```

[Go Playground Singleton](https://go.dev/play/p/NEn9tNEMBux)