# Command Design Pattern

## What is the Command design pattern?
Command is a behavioral design pattern that turns a request into a stand-alone object that contains all information about the request. This transformation lets you pass requests as a method arguments, delay or queue a request’s execution, and support undoable operations.

## What are the key components of the Command design pattern?
- **Command**: An interface or abstract class defining the execute method.
- **Concrete Command**: A class that implements the Command interface and defines the binding between a Receiver object and an action.
- **Receiver**: The object that performs the actual work when the command's execute method is called.
- **Invoker**: The object that knows how to execute a command but does not know how the command has been implemented.
- **Client**: The object that creates the command and sets the receiver.

## When should you use the Command pattern?
- When you need to parameterize objects with operations.
- When you need to queue operations, schedule their execution, or execute them at different times.
- When you need to support undo, logging, or transactional behavior.

## How does the Command pattern support undoable operations?
By storing the state of the receiver before the command executes and providing an undo method that restores the receiver to its previous state.

## Can you provide an example of the Command pattern?
For example, in a text editor application, commands such as `Copy`, `Paste`, and `Undo` can be implemented as command objects. The editor acts as the receiver, and each command manipulates the editor in a specific way.

## What are the advantages of using the Command pattern?
- It decouples the object that invokes the operation from the one that knows how to perform it.
- It allows for easy implementation of additional functionalities like logging, undo, and redo.
- It makes it easy to add new commands without changing existing code.

## What are the potential drawbacks of the Command pattern?
- It can increase the number of classes in the system, as each command requires a new class.
- It might introduce complexity if not used judiciously.

## How do you implement the Command pattern in a specific programming language (e.g., Java, Python, C#)?
Implementation details can vary based on the language, but generally, it involves creating command interfaces, concrete command classes, and an invoker class. Specific syntax and idioms will depend on the language.

## How does the Command pattern relate to other design patterns?
The Command pattern is often used in conjunction with other patterns such as the Memento pattern (for undo operations), the Composite pattern (to create macro commands), and the Strategy pattern (to encapsulate algorithms).

## What are some real-world applications of the Command pattern?
- GUI buttons and menu items in software applications.
- Transaction management in databases.
- Task scheduling systems.

# Example

Command Interface: Defines the Execute and Undo methods that all command types must implement.
```go
package main

import "fmt"

// Command interface
type Command interface {
    Execute()
    Undo()
}
```


Concrete Commands: CopyCommand, PasteCommand, and UndoCommand implement the Command interface.
```go
package main

import "fmt"

// CopyCommand struct
type CopyCommand struct {
    editor *Editor
    backup string
}

func (c *CopyCommand) Execute() {
    c.backup = c.editor.text
    c.editor.Copy()
}

func (c *CopyCommand) Undo() {
    c.editor.text = c.backup
}

// PasteCommand struct
type PasteCommand struct {
    editor *Editor
    backup string
}

func (p *PasteCommand) Execute() {
    p.backup = p.editor.text
    p.editor.Paste()
}

func (p *PasteCommand) Undo() {
    p.editor.text = p.backup
}

// UndoCommand struct
type UndoCommand struct {
    editor *Editor
}

func (u *UndoCommand) Execute() {
    u.editor.Undo()
}

func (u *UndoCommand) Undo() {
    // No operation for UndoCommand's undo
}

```

Receiver: The Editor struct which performs the actual operations.
```go
package main

import "fmt"

// Editor struct
type Editor struct {
    text    string
    clipboard string
    history []Command
}

func (e *Editor) Copy() {
    e.clipboard = e.text
    fmt.Println("Copied text:", e.clipboard)
}

func (e *Editor) Paste() {
    e.text += e.clipboard
    fmt.Println("Pasted text:", e.text)
}

func (e *Editor) Undo() {
    if len(e.history) == 0 {
        fmt.Println("No commands to undo")
        return
    }
    command := e.history[len(e.history)-1]
    e.history = e.history[:len(e.history)-1]
    command.Undo()
    fmt.Println("Undo executed, current text:", e.text)
}

func (e *Editor) ExecuteCommand(command Command) {
    command.Execute()
    e.history = append(e.history, command)
}
```

Invoker: The Application struct which stores and executes commands.
```go
package main

// Application struct acting as Invoker
type Application struct {
    editor   *Editor
    commands []Command
}

func (a *Application) AddCommand(command Command) {
    a.commands = append(a.commands, command)
}

func (a *Application) Run() {
    for _, command := range a.commands {
        a.editor.ExecuteCommand(command)
    }
}

func main() {
    editor := &Editor{}
    app := &Application{editor: editor}

    copyCommand := &CopyCommand{editor: editor}
    pasteCommand := &PasteCommand{editor: editor}
    undoCommand := &UndoCommand{editor: editor}

    editor.text = "Hello World!"

    app.AddCommand(copyCommand)
    app.AddCommand(pasteCommand)
    app.Run()

    app.AddCommand(undoCommand)
    app.Run()
}
```

(Go Playground Command)[https://go.dev/play/p/-7pkaGpEoyh]