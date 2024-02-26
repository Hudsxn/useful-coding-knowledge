## Adapter Pattern

The Adapter Pattern is a structural design pattern that allows objects with incompatible interfaces to work together. It acts as a bridge between two incompatible interfaces, converting the interface of one class into another interface that a client expects.

##### NodeJS Example:
In this example, the AmericanSocket class represents an existing class with an incompatible interface. The EuropeanSocket class represents the target interface expected by the client code. The AmericanToEuropeanAdapter class acts as the adapter, converting the interface of the AmericanSocket class into the EuropeanSocket interface. Finally, the client code plugs a European plug into the adapter, which in turn uses the American socket and converts the plug type as needed.

```javascript
// Adaptee
class AmericanSocket {
  plugIn(type) {
    switch (type) {
      case 'US':
        console.log('Plugged into American socket');
        break;
      default:
        console.log('Unknown plug type');
    }
  }
}

// Target interface
class EuropeanSocket {
  plugIn(type) {}
}

// Adapter
class AmericanToEuropeanAdapter extends EuropeanSocket {
  constructor(americanSocket) {
    super();
    this.americanSocket = americanSocket;
  }

  plugIn(type) {
    switch (type) {
      case 'EU':
        this.americanSocket.plugIn('US');
        console.log('Adapter: Converted American plug to European plug');
        break;
      default:
        console.log('Unknown plug type');
    }
  }
}

// Client code
const americanSocket = new AmericanSocket();
const adapter = new AmericanToEuropeanAdapter(americanSocket);
adapter.plugIn('EU'); // Output: Plugged into American socket, Adapter: Converted American plug to European plug
```

Now for the pros & cons.

##### Pros:

1. **Interoperability**: It enables the integration of existing classes with incompatible interfaces, allowing them to work together seamlessly without modifying their original code.

2. **Reusability**: Adapters can be reused across different client classes and scenarios, reducing code duplication and promoting maintainability.

3. **Encapsulation**: It encapsulates the process of interface conversion within the adapter class, isolating the complexities of adaptation from the client code.

4. **Solves Design Issues**: It provides a solution when it's not feasible or practical to modify the interfaces of existing classes, such as when dealing with legacy code or third-party libraries.

5. **Open/Closed Principle**: Adapters facilitate adhering to the Open/Closed Principle by allowing the addition of new adapters to support new interfaces without modifying existing client code.

##### Cons:

1. **Complexity**: Introducing adapters may add complexity to the codebase, especially if there are multiple adapters and interfaces involved, leading to increased cognitive load and potential maintenance issues.

2. **Runtime Overhead**: Adapters may introduce a slight runtime overhead due to the additional layer of indirection involved in interface conversion, although this overhead is usually negligible.

3. **Potential Performance Impact**: Depending on the implementation, using adapters may have a performance impact, especially if the adaptation process involves costly operations or if adapters are used extensively in the system.

4. **Design Clutter**: Adapters can clutter the codebase, especially if there are many adapters for different interfaces, potentially making the code harder to understand and maintain.

5. **Potential Misuse**: In some cases, adapters may be misused or overused, leading to unnecessarily complex designs or introducing unnecessary abstraction layers.