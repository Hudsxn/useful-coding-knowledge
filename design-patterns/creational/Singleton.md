## Singleton design pattern

The singleton design pattern enforces that there is a global, single instance of an object/class. This is used in OOP contexts. This can be useful for resources such as database connections, ensuring only a single connection is made to a database across the entire application. There are far more use cases for a singleton, as a learning exercise, see if you can come up with some use cases!

As you can see below, singletons all follow a certain pattern as defined below, you have a class with a private static instance field (if visibility modifiers exist, unlucky JavaScript developers). Then in the class constructor, the instantiated class reference is assigned to the static field, enabling you to access the instance globally.

##### Example singleton in NodeJS
```javascript

export class MySingleton {
    static _self;

    constructor() {
        if (MySingleton._self) {
            throw new Error('Use MySingleton::Get');
        }
        MySingleton._self = this;
    }

    // other methods here
    
    static getInstance() {
        return MySingleton._self ?? new MySingleton();
    }
}
```

##### Example singleton in PHP
```php
class MySingleton
{
    private static ?MySingleton $self;

    private function __construct() 
    {
        self::$self = $this;
    }

    public static function getInstance(): self
    {
        return self::$self ?? new MySingleton();
    }
}
```

##### Example singleton in Java
```java
package my.app;

public class MySingleton {
    private static MySingleton self;
    
    private MySingleton() {
        self = this;
    }

    public static MySingleton getInstance() {
        return self ?? new MySingleton();
    }
}
```

## Pros & Cons

#### Pros

1. **Single Instance**: It ensures that a class has only one instance, which is particularly useful when exactly one object is needed to coordinate actions across the system.

2. **Global Access**: It provides a global point of access to that instance, making it easy to access the singleton object from anywhere in the codebase.

3. **Lazy Initialization**: It supports lazy initialization, i.e., the instance is created only when it's requested for the first time, which can save resources in situations where the object is not always needed.

4. **Thread Safety**: A properly implemented Singleton can provide thread safety if needed, ensuring that concurrent access does not result in unexpected behavior.

5. **Memory Management**: It helps in managing resources efficiently by ensuring that there's only one instance consuming memory throughout the application's lifecycle.

#### Cons

1. **Global State**: While global access is a benefit, it can also be considered a downside as it introduces global state, which can lead to tight coupling and make it difficult to track and manage dependencies.

2. **Testing Difficulties**: Singletons can be difficult to unit test since they often rely on global state, making it hard to isolate their behavior for testing purposes.

3. **Singleton Lifetime**: The lifecycle of a singleton is tied to the lifecycle of the application, which might not always be desirable. It can lead to issues if the singleton instance needs to be destroyed or recreated during runtime.

4. **Hard to** Subclass: Implementing inheritance with a Singleton can be challenging since the constructor is typically private or protected, making it difficult to subclass the Singleton class.

5. **Concurrency Concerns**: While Singleton patterns can provide thread safety, improper implementation can lead to concurrency issues such as race conditions or deadlocks.

6. **Dependency Injection Issues**: Singletons can make it difficult to use dependency injection since they hide their dependencies and manage their instantiation internally.