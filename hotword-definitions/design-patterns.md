## Design patterns

Design patterns are reusable solutions to common problems encountered during software development. They represent best practices and proven solutions to recurring design challenges, providing a way to structure code in a flexible, maintainable, and scalable manner.

There are three main categories of design patterns (And I've written MD files on lots of different patterns, see [design patterns](./../design-patterns))

1. **Creational Patterns**: These patterns deal with the creation of objects, providing mechanisms for object instantiation that promote flexibility and decoupling.

   - Examples include:
     - **Singleton**: Ensures that a class has only one instance and provides a global point of access to that instance.
     - **Factory Method**: Defines an interface for creating objects but allows subclasses to alter the type of objects that will be created.
     - **Builder**: Separates the construction of a complex object from its representation, allowing the same construction process to create different representations.
     - **Prototype**: Creates new objects by copying an existing object, avoiding the need for subclassing.

2. **Structural Patterns**: These patterns focus on the composition of classes and objects, defining ways to organize and structure relationships between them.

   - Examples include:
     - **Adapter**: Allows incompatible interfaces to work together by wrapping an interface around an existing class.
     - **Decorator**: Dynamically adds behavior to objects by wrapping them in an object of a decorator class.
     - **Composite**: Represents objects hierarchically in a tree structure, allowing clients to treat individual objects and compositions of objects uniformly.
     - **Proxy**: Provides a surrogate or placeholder for another object to control access to it.

3. **Behavioral Patterns**: These patterns focus on the interaction and communication between objects, defining algorithms and responsibilities.

   - Examples include:
     - **Observer**: Defines a one-to-many dependency between objects, so that when one object changes state, all its dependents are notified and updated automatically.
     - **Strategy**: Defines a family of algorithms, encapsulates each one, and makes them interchangeable. Strategy lets the algorithm vary independently from clients that use it.
     - **Chain of Responsibility**: Passes a request along a chain of handlers, allowing multiple objects to handle the request without explicitly specifying the receiver.
     - **Command**: Encapsulates a request as an object, thereby allowing parameterization of clients with queues, requests, and operations.

It's important to note that design patterns are not a one-size-fits-all solution, and their application should be context-specific. They provide guidance and common solutions to design problems, but they should be used judiciously and adapted to the specific requirements and constraints of each project.