# Single Responsability Principle

### Definition

A class should have one and only one reason to change, meaning that a class should have only one job.

Example:


```go
type Color struct {
  ID int
  Name string
}

func (c *Color) GetDetails() string {
  return fmt.Sprintf("ID: %d - Name: %s", c.ID, c.Name)
}

func (c *Color) SaveColor() {
  // Code to save color details into a database
}
```

This example shows the Color struct has two responsabilities:

1. It holds color data and provides a way to get color details.
2. It saves the color data into a database.


```go
type Color struct {
  ID int
  Name string
}

func (c *Color) GetDetails() string {
  return fmt.Sprintf("ID: %d - Name: %s", c.ID, c.Name)
}

type ColorRepository struct {
  // Database related fields
}

func (r *ColorRepository) SaveColor(c *Color) {
  // Code to save color details into a database
}
```
Now, Color struct only has one single responsability, the responsibility of saving the color data into a database is transferred to the `ColorRespository` struct. This refactoring makes the code more modular, easier to read, test, and maintain.

### Can you explain the Single Responsibility Principle (SRP)?
A class should have only one reason to change. If a class has more than one responsibility, this can make the code complex. Separating the responsibilities makes the code more maintainable and less error-prone.

### How can you identify if a struct violates the SRP?
In Go, I can identify if a struct violates the Single Responsibility Principle (SRP) if the propesties in a struct refer to two or more abstract ideas, unrelated functionalities are associated with it, the code becomes complex, and it's difficult to test.

### Describe a scenario where applying SRP improved code maintainability.
* Separate structs responsibilities: each struct contains its own responsability.
* Improved maintainability: To make testing easier, clear and logical code is easier to read.
* Clearer code: The code becomes more focused and easier to understand. Developers can quickly grasp the purpose of each struct and its methods.
* Easier testing: Each smaller struct can be tested in isolation, improving test coverage and reducing the risk of regressions when making changes.
