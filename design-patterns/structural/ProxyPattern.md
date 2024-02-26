## Proxy Pattern

The Proxy design pattern provides a surrogate or placeholder for another object to control access to it. In other words, it allows you to create a proxy object that acts as an intermediary between a client and the real object, providing an additional layer of control over how the client interacts with the real object. The proxy can perform tasks such as lazy initialization, access control, logging, caching, and more, without the client being aware of it.

Here's a brief description of the Proxy pattern components:

1. **Subject**: This is the interface or abstract class that defines the common interface for the RealSubject and Proxy so that the Proxy can be used anywhere the RealSubject is expected.

2. **RealSubject**: This is the real object that the proxy represents. It defines the functionality that the client wants to access indirectly.

3. **Proxy**: This is the proxy object that acts as an intermediary between the client and the real object. It has the same interface as the RealSubject so that it can be used interchangeably with it. The proxy typically manages the lifecycle of the RealSubject and may perform additional tasks before or after delegating calls to the RealSubject.

Here's an example of the Proxy pattern in Node.js:

```javascript
// Subject interface
class Door {
    open() {}
    close() {}
}

// RealSubject
class LabDoor extends Door {
    open() {
        console.log('Opening lab door');
    }
    close() {
        console.log('Closing lab door');
    }
}

// Proxy
class SecurityProxy extends Door {
    constructor(door) {
        super();
        this.door = door;
        this.isOpen = false;
    }

    open() {
        if (this.authenticate()) {
            this.door.open();
            this.isOpen = true;
        } else {
            console.log('Access denied');
        }
    }

    close() {
        this.door.close();
        this.isOpen = false;
    }

    authenticate() {
        // Simulate authentication logic
        return Math.random() < 0.5;
    }
}

// Usage
const door = new SecurityProxy(new LabDoor());
door.open(); // Access denied or Opening lab door
door.close(); // Closing lab door
```

In this example:

- `Door` is the Subject interface that defines the common interface for both the RealSubject (`LabDoor`) and the Proxy (`SecurityProxy`).
- `LabDoor` is the RealSubject that represents the actual door.
- `SecurityProxy` is the Proxy that acts as a security layer for accessing the lab door. It checks for authentication before opening the door.
- The client interacts with the Proxy (`SecurityProxy`), which in turn delegates the calls to the RealSubject (`LabDoor`) after performing authentication checks.

This example demonstrates how the Proxy pattern can be used to control access to a real object (`LabDoor`) by adding additional functionality (authentication) without modifying the real object itself.