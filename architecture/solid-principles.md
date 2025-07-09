# SOLID Principles with Examples in TypeScript
**SOLID** is a mnemonic acronym that represents five fundamental principles of object-oriented programming (OOP), aimed at making software designs more understandable, flexible, and maintainable.

These principles were introduced by **Robert C. Martin** in his 2000 paper, *"Design Principles and Design Patterns"*, and are widely adopted to help developers create code that is easier to understand, maintain, and scale over time.

The five **SOLID principles** are:
1. [**[S] - Single Responsibility (SRP)**](#1-single-responsibility-principle-srp)
2. [**[O] - Open/Closed Principle (OCP)**](#2-openclosed-principle-ocp)
3. [**[L] - Liskov Substitution Principle (LSP)**](#3-liskov-substitution-principle-lsp)
4. [**[I] - Interface Segregation Principle (ISP)**](#4-interface-segregation-principle-isp)
5. [**[D] - Dependency Inversion Principle (DIP)**](#5-dependency-inversion-principle-dip)

## 1. Single Responsibility Principle (SRP)
A class should have only one reason to change. This means each class or module should have a single, well-defined responsibility.

Let's explore **Single Responsibility Principle (SRP)** principle by examples:

### ❌ Violation Example: `Car` class has multiple responsibilities
In this example `Car` class would need to change if:
- Engine logic changes
- Logging logic changes
- Car lifecycle flow changes  

This violates **Single Responsibility Principle (SRP)** - `Car` has multiple responsibilities.

```ts
class Car {
  startEngine() {
    console.log('Starting engine...');
    // engine logic
  }

  stopEngine() {
    console.log('Stopping engine...');
    // engine logic
  }

  logCarDetails() {
    console.log('Logging car details...');
    // logging logic
  }

  drive() {
    this.startEngine();
    this.logCarDetails();
    console.log('Car is now driving...');
  }

  stop() {
    this.stopEngine();
    console.log('Car has stopped.');
  }
}
```

### ✅ Valid Example: Separate concerns across focused classes
Let's break down `Car` class into separate classes where each has its own single responsibility:
- `Engine`: Manages engine logic
- `CarLogger`: Handles logging
- `Car`: Coordinates behavior 

This makes the code more maintainable, testable, and modular, following the **Single Responsibility Principle (SRP)**.

```ts
class Engine {
  start() {
    console.log('Engine started');
  }

  stop() {
    console.log('Engine stopped');
  }
}

class CarLogger {
  logDetails() {
    console.log('Logging car details...');
  }
}

class Car {
  private engine: Engine;
  private logger: CarLogger;

  constructor(engine: Engine, logger: CarLogger) {
    this.engine = engine;
    this.logger = logger;
  }

  drive() {
    this.engine.start();
    this.logger.logDetails();
    console.log('Car is now driving...');
  }

  stop() {
    this.engine.stop();
    console.log('Car has stopped.');
  }
}

```

## 2. Open/Closed Principle (OCP)
Software entities (`classes`, `modules`, `functions`, etc.) should be open for extension but closed for modification. This means you should be able to add new functionality without altering existing code.
This can be achieved through [**polymorphism**](/oop/principles-oop.md#polymorphism) and [**abstraction**](/oop/principles-oop.md#abstraction).

Let's explore the **Open/Closed Principle (OCP)** with examples.    
Suppose we have a system that calculates discounts for different types of users (e.g., regular users, premium users, and new users).

### ❌ Violation Example: Modify the function to support new user type
Problems in this approach:
- Every time we need to support a new user type, we must modify the function.
- This violates **Open/Closed Principle (OCP)** because adding a new user type like `enterprise` requires editing this function.

```ts
type UserType = 'regular' | 'premium' | 'new';

function calculateDiscount(userType: UserType): number {
  if (userType === 'regular') {
    return 0.05;
  } else if (userType === 'premium') {
    return 0.2;
  } else if (userType === 'new') {
    return 0.1;
  }

  return 0;
}
```
### ✅ Valid Example: Follows OCP using polymorphism + abstraction
Instead of changing the logic, we extend it with new classes.  

Benefits of this approach:   
- No need to touch existing logic when adding new types
- Extensible and testable
- Keeps each concern isolated

```ts
/* Extend the Logic with Classes */
// Base abstraction
interface DiscountStrategy {
  getDiscount(): number;
}

// Concrete implementations
class RegularUserDiscount implements DiscountStrategy {
  getDiscount(): number {
    return 0.05;
  }
}

class PremiumUserDiscount implements DiscountStrategy {
  getDiscount(): number {
    return 0.2;
  }
}

class NewUserDiscount implements DiscountStrategy {
  getDiscount(): number {
    return 0.1;
  }
}

// Usage (Open for extension, closed for modification)
function applyDiscount(strategy: DiscountStrategy): number {
  return strategy.getDiscount();
}
```

Now you can easily add a new strategy without modifying existing logic:
```ts
/* Add a new strategy without modifying existing logic */
class EnterpriseUserDiscount implements DiscountStrategy {
  getDiscount(): number {
    return 0.3;
  }
}

const discount = applyDiscount(new EnterpriseUserDiscount());
console.log(discount); // 0.3
```

We can spot two **OOP principles** here:
- **Polymorphism**   
  In our example, this is polymorphism:

   ```ts
   function applyDiscount(strategy: DiscountStrategy): number {
     return strategy.getDiscount();
   }
   ```
  
  Here’s what’s happening:
    - `applyDiscount()` accepts any object that implements the `DiscountStrategy` interface.
    - At runtime, it could be a `RegularUserDiscount`, `PremiumUserDiscount`, `EnterpriseUserDiscount`, etc.
    - Each of those implements `getDiscount()` differently.
    - But they are interchangeable, because they all satisfy the same abstraction (`DiscountStrategy`).  
  
  That is **polymorphism in action** - even though we used interfaces, not class inheritance. <br><br>

- **Abstraction**   
  In our example, this part is the abstraction:

  ```ts
  interface DiscountStrategy {
    getDiscount(): number;
  }
  ```
  
  Here's what's happening:
    - `DiscountStrategy` defines a contract (or "what" each class should do), but not how.
    - It doesn't contain any actual logic - just a method signature: `getDiscount()`: number.
    - This allows you to build multiple interchangeable implementations that follow this contract.

## 3. Liskov Substitution Principle (LSP)
Subtypes must be substitutable for their base types without altering the correctness of the program. 
- Essentially, derived classes should be usable in place of their base classes without causing issues.   
- This principle ensures that subclasses don’t break the contracts or expected behavior of their base classes.

Let's explore **Liskov Substitution Principle (LSP)** by examples:

### ❌ Violation Example: Square inheriting from Rectangle
Problems in this approach:
- `Square` breaks the `Rectangle` contract (independent width/height).
- This violates the **Liskov Substitution Principle (LSP)** because substituting `Square` where a `Rectangle` is expected produces incorrect results.

   ```ts
   class Rectangle {
      constructor(public width: number, public height: number) {}
   
      setWidth(w: number) {
         this.width = w;
      }
   
      setHeight(h: number) {
         this.height = h;
      }
   
      getArea(): number {
         return this.width * this.height;
      }
   }
   
   class Square extends Rectangle {
      setWidth(w: number) {
         this.width = this.height = w;
      }
   
      setHeight(h: number) {
         this.width = this.height = h;
      }
   }
   
   const shape: Rectangle = new Square(5, 5);
   shape.setWidth(4);
   shape.setHeight(6);
   
   console.log(shape.getArea()); // ❌ Expected 24 (4×6), got 36
   ```

### ✅ To avoid LSP violations, we can favor composition over inheritance
In object-oriented programming, both inheritance and composition are used to create relationships between classes, but they achieve this in different ways.    
- **Inheritance** models an **"is-a"** relationship, where a new class (subclass) inherits properties and behaviors from an existing class (superclass).    
- **Composition**, on the other hand, models a **"has-a"** relationship, where a class contains instances of other classes as members.

In this example:
- `Square` doesn’t extend `Rectangle`.
- We model it according to its own rules.
- This avoids all misuse and misrepresentation.

**Composition** keeps responsibilities isolated and behavior predictable.

   ```ts
   class Square {
     private size: number;
   
     constructor(size: number) {
       this.size = size;
     }
   
     getArea(): number {
       return this.size * this.size;
     }
   }
   ```

### ✅ Another Example of Composition
In this example:   
- `Car` has an `Engine` (composition)
- `Engine` is provided to `Car` (dependency injection)

```ts
class Engine {
   start() { console.log("Engine started"); }
}

class Car {
   constructor(private engine: Engine) {} // DI via constructor

   start() {
      this.engine.start();
      console.log("Car is moving");
   }
}

// Elsewhere, composing objects and injecting dependencies
const engine = new Engine();
const car = new Car(engine); // DI and Composition happen here
```

### ✅ Use Interfaces for Polymorphism
Instead of inheritance, define a contract with an interface.

Benefits of this approach:  
- Promotes polymorphism and maintains ***Liskov Substitution Principle (LSP).***
- Each class implements its own logic while respecting the shared contract.

```ts
interface Shape {
  draw(): void;
}

class Circle implements Shape {
  draw() {
    console.log('Drawing a circle');
  }
}

class Rectangle implements Shape {
  draw() {
    console.log('Drawing a rectangle');
  }
}
```

### ✅ Valid Example: Polymorphism with logging
In this example:
- The `draw()` method still performs its expected purpose.
- This is safe polymorphism: `Circle` can be used where `Shape` is expected.
- Logging is allowed and does not violate **Liskov Substitution Principle (LSP).**

   ```ts
   class Shape {
     draw(): void {
       console.log('Drawing a shape...');
     }
   }
   
   class Circle extends Shape {
     draw(): void {
       console.log('Logging: Drawing a circle');
       // Still fulfills the draw contract
       super.draw();
     }
   }
   
   const shape: Shape = new Circle();
   shape.draw(); // Outputs: Logging: Drawing a circle
   ```
  
### Summary of **Liskov Substitution Principle (LSP)** Rule in Practice:
- Don’t inherit just to reuse code.
- Use inheritance only for true **“is-a”** relationships.
- Otherwise, prefer **composition** and **interfaces**.

## 4. Interface Segregation Principle (ISP)
Clients should not be forced to depend on interfaces they do not use. This means you should create smaller, more focused interfaces rather than large, all-encompassing ones.

Let's explore **Interface Segregation Principle (ISP)** by examples:

### ❌ Violation Example: All vehicles are forced to implement flying behavior, even if they don't need it
Problems in this approach:  
- The `Car` class is forced to implement `fly()` even though it doesn't fly - violating **Interface Segregation Principle (ISP)**.
- Even if we can mark `fly()` with `?` like `fly?()` making it optional, it is still a good practice to separate interfaces into smaller ones because it becomes unclear which methods are relevant for which clients.

```ts
// Bad: One large interface
interface Vehicle {
  drive(): void;
  fly(): void;
}

class Car implements Vehicle {
  drive() {
    console.log('Driving on the road');
  }

  fly() {
    throw new Error('Car cannot fly!');
  }
}

class Airplane implements Vehicle {
  drive() {
    console.log('Taxiing on the runway');
  }

  fly() {
    console.log('Flying in the sky');
  }
}
```

### ✅ Valid Example: Split the large interface into smaller, focused ones:
Benefits of this example:
- Car only implements what it needs - `drive()`.
- Airplane can use both `drive()` and `fly()` via composition of small interfaces.
- Each class stays focused and clean, following the **Interface Segregation Principle (ISP)**.

```ts
// Smaller, focused interfaces
interface Drivable {
  drive(): void;
}

interface Flyable {
  fly(): void;
}

class Car implements Drivable {
  drive() {
    console.log('Driving on the road');
  }
}

class Airplane implements Drivable, Flyable {
  drive() {
    console.log('Taxiing on the runway');
  }

  fly() {
    console.log('Flying in the sky');
  }
}
```

## 5. Dependency Inversion Principle (DIP)
High-level modules should not depend on low-level modules. Both should depend on abstractions. This promotes loose coupling and makes it easier to change lower-level components without affecting higher-level ones.

Let's explore **Dependency Inversion Principle (DIP)** through examples:

### ❌ Violation Example: We cant easily switch to other engine without modifying the Car class.
Problems in this approach:
- `Car` directly depends on `PetrolEngine`.
- We cannot easily switch to `ElectricEngine` without modifying the `Car` class.
- This violates **Dependency Inversion Principle (DIP)** and makes our system hard to scale and test.

```ts
class PetrolEngine {
  start() {
    console.log("Petrol engine starting...");
  }
}

class Car {
  private engine: PetrolEngine;

  constructor() {
    this.engine = new PetrolEngine(); // tightly coupled to PetrolEngine
  }

  drive() {
    this.engine.start();
    console.log("Car is moving");
  }
}
```

### ✅ Valid Example: Using abstraction
Benefits of this approach:
- `Car` depends only on the `Engine` abstraction, not on a specific engine type.
- We can easily swap implementations (e.g. test mocks, upgrades).
- This promotes **flexibility**, **testability**, and **scalability**.

```ts
// Abstraction
interface Engine {
  start(): void;
}

// Low-level module
class PetrolEngine implements Engine {
  start() {
    console.log("Petrol engine starting...");
  }
}

// Another low-level module
class ElectricEngine implements Engine {
  start() {
    console.log("Electric engine starting silently...");
  }
}

// High-level module depends on abstraction
class Car {
  constructor(private engine: Engine) {}

  drive() {
    this.engine.start();
    console.log("Car is moving");
  }
}

// Usage
const petrolCar = new Car(new PetrolEngine());
petrolCar.drive(); // Outputs: Petrol engine starting... Car is moving

const electricCar = new Car(new ElectricEngine());
electricCar.drive(); // Outputs: Electric engine starting silently... Car is moving
```

## Benefits of Each Principle

While the **SOLID principles** collectively help create maintainable, testable, and scalable code, let's summarize the benefits of each principle:

| SOLID Principle                  | Short Description                                                                 | Advantage                                                                                                                                      |
|----------------------------------|-----------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------|
| **S - Single Responsibility**    | A class should have only one reason to change.                                   | Increases modularity and simplifies debugging and testing.                                                                                     |
| **O - Open/Closed**              | Software entities should be open for extension but closed for modification.      | Enables safer feature additions without modifying existing code.                                                                               |
| **L - Liskov Substitution**      | Subtypes must be substitutable for their base types.                             | Enhances code reusability, improves testability, and reduces the risk of introducing bugs when adding new features or modifying existing ones. |
| **I - Interface Segregation**    | Clients should not be forced to depend on methods they don't use.                | Leads to smaller, more focused, and reusable interfaces, promoting better readability and separation of concerns.                             |
| **D - Dependency Inversion**     | High-level modules should depend on abstractions, not concrete implementations.  | Promotes loose coupling, scalability, and improved testability.                                                                                |


## Documentation and References
[**Robert C. Martin**](https://www.linkedin.com/in/robert-martin-7395b0/) also known as **"Uncle Bob,"** is a prominent figure in software development, particularly known for his work on Agile methodologies and the **SOLID principles** of object-oriented design.
These principles were introduced by **Robert C. Martin** in his 2000 paper, [**"Design Principles and Design Patterns"**](https://objectmentor.com/resources/articles/Principles_and_Patterns.pdf)

### Trusted resources on **SOLID Principles** including **Robert C. Martin's books**:

| Resource Title                                                                          | Type     | What You’ll Learn                                                                                   | Link                                                                                                     |
|-----------------------------------------------------------------------------------------|----------|-----------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------|
| **Clean Architecture** by Robert C. Martin                                              | Book     | In-depth explanations of SOLID principles, how they apply to architecture, and real-world examples. | [Link](https://www.amazon.com/Clean-Architecture-Craftsmans-Software-Structure/dp/0134494164)            |
| **Agile Software Development: Principles, Patterns, and Practices** by Robert C. Martin | Book     | Original source of SOLID principles, packed with code-level insights and exercises.                 | [Link](https://www.amazon.com/Agile-Software-Development-Principles-Patterns/dp/0135974445)              |
| **SOLID Principles in JavaScript** by Max Stoiber (freeCodeCamp)                        | Article  | A simple article that translates the core ideas of SOLID into JavaScript code examples.             | [Link](https://www.freecodecamp.org/news/solid-principles-explained-in-plain-english/)                   |
| **SOLID Principles in Programming: Understand With Real Life Examples** (GeeksForGeeks) | Article  | Detailed but beginner-friendly explanation of each principle with C++ examples.                     | [Link](https://www.geeksforgeeks.org/solid-principles-in-java/)                                          |

### Additional helper resources about **OOP**, **Clean Architecture** and **Clean Code Principles**
- [OOP Principles](./../oop/principles-oop.md)
- [Clean Code Principles](./clean-code-principles.md)
- [Clean Architecture](./clean-architecture.md)
