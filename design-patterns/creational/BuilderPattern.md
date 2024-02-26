## Builder Pattern

The Builder Pattern is a creational design pattern that separates the construction of a complex object from its representation, allowing the same construction process to create different representations. 

##### NodeJS Example
```javascript
// Product class
class Pizza {
  constructor() {
    this.toppings = [];
  }

  addTopping(topping) {
    this.toppings.push(topping);
  }

  describe() {
    console.log(`Pizza with toppings: ${this.toppings.join(', ')}`);
  }
}

// Builder class
class PizzaBuilder {
  constructor() {
    this.pizza = new Pizza();
  }

  addCheese() {
    this.pizza.addTopping('cheese');
    return this;
  }

  addPepperoni() {
    this.pizza.addTopping('pepperoni');
    return this;
  }

  addMushrooms() {
    this.pizza.addTopping('mushrooms');
    return this;
  }

  build() {
    return this.pizza;
  }
}

// Usage
const pizza = new PizzaBuilder()
  .addCheese()
  .addPepperoni()
  .addMushrooms()
  .build();

pizza.describe(); // Output: Pizza with toppings: cheese, pepperoni, mushrooms
```

##### Pros:

1. **Separation of Concerns**: It separates the construction logic from the representation of the object, making the construction process more modular and easier to manage.

2. **Flexible Object Creation**: Builders allow constructing objects step by step, providing flexibility to create different configurations or variations of the same object.

3. **Encapsulation**: It encapsulates the construction process within the builder class, hiding the details of object creation from the client code.

4. **Reusable Building Steps**: Builders can define reusable building steps, allowing the construction of similar objects with different configurations by reusing common building blocks.

5. **Fluent Interface**: Builders often use a fluent interface, enabling a more readable and expressive way to construct objects by chaining method calls.

##### Cons:

1. **Increased Complexity**: Introducing a builder can add complexity to the codebase, especially if the object being constructed is simple or does not have many configuration options.

2. **Boilerplate Code**: Implementing a builder requires defining a separate builder class and often involves writing additional code for each building step, which can lead to boilerplate code.

3. **Memory Overhead**: Builders may introduce additional memory overhead, especially if the object being constructed is large or requires significant resources.

4. **Immutable Objects**: If the object being constructed is immutable, builders may not be as effective since they typically involve modifying an object's state during construction.

5. **Performance Impact**: Depending on the implementation, using a builder may have a slight performance impact compared to directly instantiating an object, especially if there are many building steps involved.