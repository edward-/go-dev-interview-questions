# Proxy Design Pattern

## What is the Proxy design pattern?
The Proxy design pattern involves using an object, called the proxy, to represent another object. The proxy controls access to the original object, allowing for additional functionality to be added before or after the request is processed by the original object.

Proxy lets you provide a substitute or placeholder for another object. A proxy controls access to the original object, allowing you to perform something either before or after the request gets through to the original object.

## What are the types of Proxies?
There are several types of proxies, each serving different purposes:

Virtual Proxy: Delays the creation and initialization of an expensive object until it is actually needed.
Remote Proxy: Represents an object that resides in a different address space (e.g., on a different machine).
Protection Proxy: Controls access to the original object based on access rights.
Smart Proxy: Provides additional functionality, such as reference counting or logging, when an object is accessed.

## What are the benefits of using a Proxy pattern?
The Proxy pattern offers several benefits:

- Controlled Access: Proxies can control access to the real object, providing a layer of security.
- Lazy Initialization: Virtual proxies can defer the creation of expensive objects until they are needed.
- Remote Access: Remote proxies allow interaction with objects in different address spaces.
- Additional Functionality: Smart proxies can add extra functionality like logging, caching, or access control.

## Can you give an example of a Proxy pattern in real-world scenarios?
A common real-world example is a virtual proxy in a web browser that delays loading images until they are visible in the viewport, thus saving bandwidth and improving performance.

## How does a Proxy differ from a Decorator?
While both Proxy and Decorator patterns involve forwarding requests to other objects, their intentions differ:

- Proxy: Controls access to the object, potentially adding functionality related to access control, lazy initialization, etc.
- Decorator: Adds additional behavior to an object without affecting other objects of the same class.

## What are the use cases for a Protection Proxy?
Protection proxies are useful in scenarios where different users have different access levels to the functionalities provided by an object. For example, a protection proxy could be used in a file system to allow only users with the necessary permissions to read or write to a file.

## What are the challenges in implementing a Proxy pattern?
Some challenges include:
- Overhead: Adding a proxy layer introduces additional method calls, which can impact performance.
- Complexity: Managing proxies can add complexity to the codebase, making it harder to understand and maintain.
- Transparency: Ensuring the proxy behaves transparently to the client can be challenging, especially when adding functionality like caching or access control.

# Example

```go
package main

import "fmt"

// Subject is the common interface for RealSubject and Proxy.
type Subject interface {
	Request() string
}

// RealSubject is the real object that the proxy represents.
type RealSubject struct{}

func (rs *RealSubject) Request() string {
	return "RealSubject: Handling request."
}

// Proxy controls access to the RealSubject.
type Proxy struct {
	realSubject *RealSubject
}

func (p *Proxy) Request() string {
	if p.realSubject == nil {
		p.realSubject = &RealSubject{}
	}
	return "Proxy: Handling request. " + p.realSubject.Request()
}

func main() {
	proxy := &Proxy{}
	fmt.Println(proxy.Request())
}
```

[Go Playground Proxy](https://go.dev/play/p/FHLaKRsfs_0)