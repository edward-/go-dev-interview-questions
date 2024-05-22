# Liskov Substitution Principle

### Definition

Let q(x) be a property provable about objects of x of type T. Then q(y) should be provable for objects y of type S where S is a subtype of T.
This means that every subclass or derived class should be substitutable for their base or parent class.


Example:

```go
// super class
type Animal struct {
  Name string
}

func (a Animal) MakeSound() {
  fmt.Println("Animal sound")
}

// bird represents a specific type of animal
type Bird struct {
  Animal
}

func (b Bird) MakeSound() {
  fmt.Println("Chirp chirp")
}

// interface
type AnimalBehavior interface {
  MakeSound()
}

// MakeSound represent a program that works with animals and is expected
// to work with base class (Animal) or any subclass (Bird in this case)
func MakeSound(ab AnimalBehavior) {
  ab.MakeSound()
}

a := Animal{}
b := Bird{}
MakeSound(a)
MakeSound(b)
```

This demonstrates inheritance in Go, as well as the Liskov Substitution Principle, as objects of a subtype Bird can be used wherever objects of the base type Animal are expected, without affecting the correctness of the program.

### Explain the Liskov Substitution Principle (LSP).
This principle states that objects of a superclass should be replaceable with objects of a subclass without affecting the correctness of the program. This helps to ensure that the relationships between classes are well-defined and maintainable.

### Can a subclass break the LSP? If so, how?
A subclass can break the LSP when the contract is different. it brokes the behabior of a superclass.

### How can you ensure that your subclasses adhere to the LSP?
Ensure that subclasses involve careful design and adherence to the contracts defined by the superclass. Even if all interfaces contain the same contract, you still need to ensure that implementations of those interfaces in subclasses maintain substitutability.
