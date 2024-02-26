## Factory Method Pattern

The Factory Method Pattern is a creational design pattern that provides an interface for creating objects in a superclass but allows subclasses to alter the type of objects that will be created.

##### NodeJS example:
```javascript
// Product interface
class Animal {
  makeSound() {}
}

// Concrete Product classes
class Dog extends Animal {
  makeSound() {
    return 'Woof';
  }
}

class Cat extends Animal {
  makeSound() {
    return 'Meow';
  }
}

// Creator class with factory method
class AnimalFactory {
  createAnimal(type) {
    switch (type) {
      case 'dog':
        return new Dog();
      case 'cat':
        return new Cat();
      default:
        throw new Error('Invalid animal type.');
    }
  }
}

// Usage
const factory = new AnimalFactory();
const dog = factory.createAnimal('dog');
console.log(dog.makeSound()); // Output: Woof

const cat = factory.createAnimal('cat');
console.log(cat.makeSound()); // Output: Meow

```

#### Pros:

1. **Encapsulation**: It encapsulates the object creation process, allowing the client code to be decoupled from the actual implementation of the objects being created.

2. **Flexibility**: It allows subclasses to decide which class to instantiate, providing flexibility in object creation without changing the overall structure of the client code.

3. **Code Reusability**: By defining a common interface for creating objects, it promotes code reuse as multiple subclasses can use the same factory method to create different types of objects.

4. **Easy Maintenance**: Since object creation logic is centralized within the factory method, making changes to the object creation process is easier and less error-prone.

5. **Dependency Inversion**: It adheres to the Dependency Inversion Principle by allowing high-level modules to depend on abstractions (the factory method interface) rather than concrete implementations.

#### Cons:

1. **Complexity**: Introducing the Factory Method Pattern may add complexity to the codebase, especially if there are many subclasses and variations of objects to be created.

2. **Class Proliferation**: It can lead to the proliferation of subclasses if there are many variations of objects to be created, which may make the codebase harder to maintain.

3. **Tight Coupling**: Subclasses are tightly coupled to the factory method interface, which may reduce flexibility in certain scenarios where dynamic object creation is required.

4. **Potential Overhead**: In some cases, using the Factory Method Pattern might introduce overhead, especially if the object creation process is simple and straightforward.