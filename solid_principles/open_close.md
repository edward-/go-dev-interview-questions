# Open/Close Principle

### Definition

Objects or entities should be open for extension but closed for modification.

Example:


```go
type DeviceMethod interface {
  Notification()
}

type Device struct{}

func (p Device) Process(pm DeviceMethod) {
  pm.Notification()
}

type Android struct {
  message string
}

func (an Android) Notification() {
  fmt.Printf("Notification sent to Android device: %s", an.message)
}

func main() {
  d := Device{}
  an := Android{"Alert"}
  d.Process(an)
}
```

with this the Payment struct is open for extension and closed for modification. Now, we can add other payment method, for instance:

```go
type IOS struct {
  message string
}

func (io IOS) Notification() {
  fmt.Printf("Notification sent to IOS device: %s", io.message)
}

// then in main()
ios := IOS{"Alert"}
d.Process(ios)
```


### What is the Open-Closed Principle (OCP)?
OCP says a struct should be open to extensions and closed for modifications.

### How do interfaces help achieve the OCP?
Interfaces define a contract – a set of methods that a class must implement. This contract specifies the behavior a class must exhibit, without dictating how that behavior is achieved. Here's how interfaces promote OCP:

* Focus on What, Not How:  Code that uses an interface interacts with the defined functionality, not the specific implementation details. This allows for different classes to implement the interface in their own way, as long as they provide the required behavior.

* Easy Extension: New functionality can be added by creating new classes that implement the interface. The existing code using the interface doesn't need to be modified, as long as the new class fulfills the contract. This promotes code reusability and maintainability.
