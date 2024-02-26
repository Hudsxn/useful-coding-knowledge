## Command Pattern

The Command Pattern is a behavioral design pattern that encapsulates a request as an object, thereby allowing parameterization of clients with queues, requests, and operations. This pattern allows for the decoupling of senders and receivers, and it supports undoable operations.

##### Example in Node.js:
In this example, the Command Pattern is used to control a light bulb. `Bulb` is the receiver of the command. `Command` is the interface that defines the `execute` and `undo` methods. Concrete commands (`TurnOnCommand` and `TurnOffCommand`) encapsulate the actions of turning the bulb on and off, respectively. `RemoteControl` is the invoker that submits commands to the receiver. Clients can control the bulb without knowing the specific details of how the bulb is controlled or what actions are performed.
```javascript
// Receiver
class Bulb {
  turnOn() {
    console.log('Bulb has been lit');
  }

  turnOff() {
    console.log('Darkness!');
  }
}

// Command interface
class Command {
  execute() {}
  undo() {}
}

// Concrete Command
class TurnOnCommand extends Command {
  constructor(bulb) {
    super();
    this.bulb = bulb;
  }

  execute() {
    this.bulb.turnOn();
  }

  undo() {
    this.bulb.turnOff();
  }
}

// Concrete Command
class TurnOffCommand extends Command {
  constructor(bulb) {
    super();
    this.bulb = bulb;
  }

  execute() {
    this.bulb.turnOff();
  }

  undo() {
    this.bulb.turnOn();
  }
}

// Invoker
class RemoteControl {
  submit(command) {
    command.execute();
  }
}

// Usage
const bulb = new Bulb();
const turnOnCommand = new TurnOnCommand(bulb);
const turnOffCommand = new TurnOffCommand(bulb);

const remoteControl = new RemoteControl();
remoteControl.submit(turnOnCommand); // Output: Bulb has been lit
remoteControl.submit(turnOffCommand); // Output: Darkness!
```

##### Pros:

1. **Decoupling**: The Command Pattern decouples the sender of a request from the object that performs the action, allowing them to vary independently.

2. **Encapsulation**: Commands encapsulate all the details of an operation, including the action to be taken, the receiver of the action, and any parameters needed to perform the action.

3. **Supports Undo Operations**: The Command Pattern makes it easy to implement undo functionality by storing the state necessary to reverse the command's effects.

4. **Flexible and Extensible**: New commands can be added without changing existing client or receiver code, making the system more flexible and extensible.

5. **Queueing and Logging**: Commands can be stored in queues and executed later, or logged for auditing or debugging purposes.

##### Cons:

1. **Increased Complexity**: Implementing the Command Pattern may introduce additional complexity, especially if there are many different types of commands or if undo functionality is required.

2. **Overhead**: Using commands may introduce a slight runtime overhead due to the additional layers of abstraction involved, although this is usually negligible in most applications.

3. **Potential for Bloated Command Classes**: If commands become too complex or if too many responsibilities are added to them, they may become bloated and violate the Single Responsibility Principle.

4. **Command Duplication**: If similar commands are required with minor variations, there may be duplication of command classes, leading to maintenance issues.

5. **Limited Scope**: The Command Pattern is most useful for actions that can be represented as objects and where undo functionality is needed. It may not be suitable for all types of operations.