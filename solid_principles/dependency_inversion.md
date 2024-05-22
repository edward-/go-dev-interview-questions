# Dependency Inversion Principle

### Definition

Entities must depend on abstractions, not on concretions. It states that the high-level module must not depend on the low-level module, but they should depend on abstractions.

Example:


```go
type Worker struct {
  ID   int
  Name string
}

func (w Worker) GetID() int {
  return w.ID
}

func (w Worker) GetName() string {
  return w.Name
}

type Supervisor struct {
  ID   int
  Name string
}

func (s Supervisor) GetID() int {
  return s.ID
}

func (s Supervisor) GetName() string {
  return s.Name
}

type Employee interface {
  GetID() int
  GetName() string
}

type Department struct {
  Employees []Employee
}

func (d *Department) AddEmployee(e Employee) {
  d.Employees = append(d.Employees, e)
}

func (d *Department) GetEmployeeNames() (res []string) {
  for _, e := range d.Employees {
    res = append(res, e.GetName())
  }
  return
}

func (d *Department) GetEmployee(id int) Employee {
  for _, e := range d.Employees {
    if e.GetID() == id {
      return e
    }
  }
  return nil
}

func main() {
  dep := &Department{}
  dep.AddEmployee(Worker{ID: 1, Name: "John"})
  dep.AddEmployee(Supervisor{ID: 2, Name: "Jane"})

  fmt.Println(dep.GetEmployeeNames())

  e := dep.GetEmployee(1)
  switch v := e.(type) {
  case Worker:
    fmt.Printf("found worker %+v\n", v)
  case Supervisor:
    fmt.Printf("found supervisor %+v\n", v)
  default:
    fmt.Printf("could not find an employee by id: %d\n", 1)
  }
}
```

This demonstrates the Dependency Inversion Principle, as the Department struct depends on an abstraction (the Employee interface), rather than on a specific implementation (the Worker or Supervisor struct). This makes the code more flexible and easier to maintain, as changes to the implementation of workers and supervisors will not affect the Department struct.


### Explain the Dependency Inversion Principle (DIP).
This principle states that high-level modules should not depend on low-level modules, but rather both should depend on abstractions. This helps to reduce the coupling between components and make the code more flexible and maintainable.

### What's the difference between depending on concretions and abstractions?
Depending on concretions means relying on specific implementations of classes or objects, while depending on abstractions involves relying on interfaces or abstract classes. In essence, depending on concretions ties code directly to specific implementations, making it less flexible and harder to change, while depending on abstractions allows for greater flexibility and modularity, as it decouples components from concrete implementations, enabling easier substitution and extension.
