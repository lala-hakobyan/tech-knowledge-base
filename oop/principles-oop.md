# Core Principles of OOP with Examples in TypeScript
**Object-Oriented Programming (OOP)** is a programming paradigm that structures software design around **data (objects)** rather than functions and logic. It models real-world entities as **objects**, each encapsulating **data (attributes)** and **behavior (methods)**. These objects interact with each other to build complex systems.

**OOP** is based on four core principles. These principles help create modular, reusable, and maintainable code by organizing it around objects and their interactions:
- [Encapsulation](#encapsulation)
- [Inheritance](#inheritance)
- [Polymorphism](#polymorphism)
- [Abstraction](#abstraction)

In this article, we will not only cover the core principles of **OOP**, but also project those concepts into **JavaScript (TypeScript)** code.

## Encapsulation
**Encapsulation** in object-oriented programming (OOP) is the practice of bundling the data (attributes) and methods (functions) that operate on that data into a single unit, typically a class. It's a key principle of OOP that promotes data hiding, abstraction, and modularity. By encapsulating data, you can control access to it, making your code more manageable, reusable, and secure.

### Core Concepts of Encapsulation
- **Bundling Data and Methods**  
Encapsulation combines data (variables) and the functions (methods) that manipulate that data into a single unit, the **class**.
- **Data Hiding**  
It restricts direct access to the internal data of an object from outside the class, protecting it from unintended modification.
- **Controlled Access**  
While hiding the internal data, encapsulation provides controlled access through methods (**getters** and **setters**) that can validate and manage data changes.
- **Abstraction**  
Encapsulation supports abstraction by exposing a **public interface (methods)** while hiding the complex implementation details.
- **Modularity**  
It promotes modularity by creating self-contained units of code (classes) that can be easily reused and maintained.

### How to Achieve Encapsulation?
The classic way to achieve **encapsulation** in object-oriented programming is by using **getters and setters** inside classes.   
Here’s what **getters and setters** allow us to do:
- **Hide Internal State**  
The actual data is kept private - it's not directly accessible from outside the class.
- **Expose a Controlled Interface**    
You define exactly how values can be read or updated.
- **Add Validation, Formatting, or Side Effects**   
You can apply logic when accessing or modifying data, without exposing the internal implementation.

**Encapsulation Example**    
What's encapsulated here?
- `_email` is a private field, meaning it's not accessible directly (`user._email` would throw an error).
- Access is only possible through `get email()` and `set email()`.
- The setter includes validation logic, preventing invalid data from being set.
- This keeps the internal state safe and under control - a perfect example of encapsulation.

```ts
class User {
  private _email: string;

  constructor(email: string) {
    this._email = email;
  }

  get email(): string {
    return this._email;
  }

  set email(newEmail: string) {
    if (!newEmail.includes('@')) {
      throw new Error('Invalid email');
    }
    this._email = newEmail;
  }
}

// ✅ Client-side usage
const user = new User('lala@example.com');

// Accessing the email using the getter
console.log(user.email); // Output: lala@example.com

// Updating the email using the setter
user.email = 'newmail@example.com';
console.log(user.email); // Output: newmail@example.com

// ❌ Attempting to set an invalid email
try {
    user.email = 'invalid-email'; // Throws: Error: Invalid email
} catch (err) {
    console.error(err.message); // Output: Invalid email
}

// ❌ Direct access is not allowed
// console.log(user._email); // Error: Property '_email' is private
```

### Benefits of Encapsulation
- **Data Protection**    
Prevents direct modification of data, ensuring data integrity and consistency.
- **Increased Security**    
Limits access to sensitive data, reducing the risk of unauthorized access or modification.
- **Improved Code Organization**    
Makes code more structured and easier to understand by bundling related data and methods.
- **Reduced Complexity**  
Hiding internal details simplifies the use of objects, making the system easier to manage.
- **Increased Flexibility**  
Allows for changes to the internal implementation of a class without affecting the code that uses it, as long as the public interface remains the same.

## Inheritance
In object-oriented programming (OOP), **inheritance** is a mechanism where a new class (subclass or derived class) can inherit properties and methods from an existing class (superclass or base class). This allows for code reuse and the creation of a hierarchical structure of classes.

### Core Concepts of Inheritance:
- **Base Class (Parent/Superclass)**    
The class that provides the inherited members (attributes and methods).
- **Derived Class (Child/Subclass)**     
The class that inherits the members from the base class.
- **Inheritance Relationship**     
Represents the **"is-a"** relationship between classes. For example, a `Dog` class **"is-a"** `Animal` class.
- **Code Reusability**     
Inheritance promotes code reuse by allowing the derived class to utilize the functionality of the base class without rewriting it.
- **Extensibility**     
Inheritance allows you to extend the functionality of a base class by adding new attributes and methods in the derived class.
Example:
Imagine a `Vehicle` class with methods like `startEngine()` and `accelerate()`. A `Car` class can inherit from `Vehicle` and also have its own unique methods like `openSunroof()`. This way, a `Car` object can perform all the actions of a generic vehicle, plus car-specific actions.

### Types of Inheritance
- **Single Inheritance**     
A class inherits from only one base class.
    ```ts
    class User {
      constructor(public name: string) {}
      greet() {
        console.log(`Hello, I’m ${this.name}`);
      }
    }
    
    class AdminUser extends User {
      constructor(name: string, public role: string) {
        super(name);
      }
    
      manage() {
        console.log(`${this.name} manages with role ${this.role}`);
      }
    }
    
    const admin = new AdminUser('Alice', 'Moderator');
    admin.greet(); // Hello, I’m Alice
    admin.manage(); // Alice manages with role Moderator
    ```

- **Multiple Inheritance**      
A class inherits from multiple base classes (this is not supported in all languages like Javascript, Java and C#, but is available in languages like Python).

- **Multi-level Inheritance**    
A class inherits from a derived class, which in turn inherits from another base class.
    ```ts
    class Engine {
      start() {
        console.log('Engine started');
      }
    }
    
    class CarEngine extends Engine {
      accelerate() {
        console.log('Accelerating...');
      }
    }
    
    class SportsCar extends CarEngine {
      boost() {
        console.log('Boost mode ON!');
      }
    }
    
    const ferrari = new SportsCar();
    ferrari.start();      // Engine started
    ferrari.accelerate(); // Accelerating...
    ferrari.boost();      // Boost mode ON!
    ```

- **Hierarchical Inheritance**  
Multiple classes inherit from a single parent class.
    ```ts
    class Animal {
      eat() {
        console.log('Eating...');
      }
    }
    
    class Dog extends Animal {
      bark() {
        console.log('Woof!');
      }
    }
    
    class Cat extends Animal {
      meow() {
        console.log('Meow!');
      }
    }
    
    const dog = new Dog();
    dog.eat(); // Eating...
    dog.bark(); // Woof!
    
    const cat = new Cat();
    cat.eat(); // Eating...
    cat.meow(); // Meow!
    ```

- **Hybrid Inheritance**  
This is a combination of two or more of the above inheritance types.
    ```ts
    // Base class
    class Vehicle {
      start() {
        console.log('Vehicle started');
      }
    }
    
    // First level of inheritance (Multi-level begins)
    class Car extends Vehicle {
      drive() {
        console.log('Car is driving');
      }
    }
    
    // Second level of inheritance (Multi-level)
    class SportsCar extends Car {
      turboBoost() {
        console.log('Turbo boost activated');
      }
    }
    
    // Another branch from the base (Hierarchical)
    class Motorcycle extends Vehicle {
      wheelie() {
        console.log('Motorcycle doing a wheelie');
      }
    }
    
    // Demo usage
    const lambo = new SportsCar();
    lambo.start();         // inherited from Vehicle
    lambo.drive();         // inherited from Car
    lambo.turboBoost();    // from SportsCar
    
    const bike = new Motorcycle();
    bike.start();          // inherited from Vehicle
    bike.wheelie();        // from Motorcycle
    ```

### Inheritance vs. Composition:
While inheritance allows for **"is-a"** relationships, composition allows for **"has-a"** relationships. For example, a `Car` **"has-a"** `Engine`, which is a composition relationship. Choosing between inheritance and composition depends on the specific relationship you want to model in your code.
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

### Benefits of Inheritance:
- **Code Reusability**   
Avoids redundant code by inheriting from existing classes.
- **Extensibility**   
Easily add new features to existing classes.
- **Code Organization**  
Creates a hierarchical structure of classes, making code easier to understand and maintain.
- **Polymorphism Support**   
**Inheritance** is a foundation for **polymorphism**, enabling objects of different classes to respond to the same method call in their own way.

## Polymorphism
**Polymorphism** is one of the fundamental concepts of **Object-Oriented Programming (OOP)**. The term itself means **“many forms”**, derived from the Greek words **“poly” (many)** and **“morph” (form)**.   
**Polymorphism** in **OOP** refers to the ability of different objects to respond to the same method call in their own unique way. It allows a single variable, function, or object to take on multiple forms or behaviors. This enables **code reusability**, **flexibility**, and **easier maintenance** of complex systems.

### Key Aspects of Polymorphism
- #### Method Overriding
  Derived classes can redefine methods inherited from their parent class, providing specialized behavior. 
  - Method overriding is also an example of **Dynamic Binding (Subtype Polymorphism)**.   
  - **Dynamic Binding** is a mechanism where the method that gets executed is determined at **runtime**, based on the actual type of the object - not the reference type.   
  - This enables **Subtype Polymorphism**, where a subclass instance can be treated as an instance of its superclass, and the correct overridden method will still be called.<br><br>

  Let's explore Method Overriding (Dynamic Binding) Example:
  - In this example, `AdminUser` extends `User` and overrides the `login()` method.
  - We then create a `user` object and assign it to an `AdminUser` instance. When we call `user.login()` (where `user` is actually an instance of `AdminUser`), the overridden `AdminUser.login()` method will execute - not the base one.
  - This behavior is known as **dynamic binding**, and it’s what enables **subtype polymorphism** to work.
  - Also, since `AdminUser` inherits from `User` and does not break or alter any of `User`’s public methods, it can safely be used anywhere a `User` is expected.  
  This aligns with the **Liskov Substitution Principle (LSP)** from the **SOLID principles**, which states that derived types must be substitutable for their base types without affecting program correctness.

    ```ts
    class User {
     login() {
     console.log('User logged in');
     }
    }
    
    class AdminUser extends User {
     login() {
     console.log('Admin logged in with elevated permissions');
     }
    }
    
    let user: User = new User();
    const admin = new AdminUser();
    
    user = admin;          // ✅ Works: AdminUser has all methods of User
    user.login();          // Output: "Admin logged in with elevated permissions" - runtime binding
    
    // admin = user;       ❌ Error: User may not have AdminUser-specific methods
    ```
- #### Method Overloading
    Having multiple methods with the same name but different parameters (number or types) within the same class.
    ```ts
    class Car {
      start(): void;
      start(mode: string): void;
      start(mode?: string): void {
        if (mode) {
          console.log(`Car started in ${mode} mode`);
        } else {
          console.log('Car started');
        }
      }
    }
    
    const myCar = new Car();
    myCar.start();         // Output: "Car started"
    myCar.start('sport');  // Output: "Car started in sport mode"
    ```

- #### Interface-Based Polymorphism
    Classes can implement the same interface, allowing them to be treated as a common type even though they have different underlying implementations.
    ```ts
    interface AuthService {
      login(): void;
    }
    
    class GoogleAuth implements AuthService {
      login() {
        console.log('Logged in with Google');
      }
    }
    
    class FacebookAuth implements AuthService {
      login() {
        console.log('Logged in with Facebook');
      }
    }
    
    function performLogin(auth: AuthService) {
      auth.login();
    }
    
    performLogin(new GoogleAuth());   // Output: "Logged in with Google"
    performLogin(new FacebookAuth()); // Output: "Logged in with Facebook"
    ```

### Types of Polymorphism
- **Compile-time (Static) Polymorphism**  
Resolved during compilation, like method overloading.
- **Runtime (Dynamic) Polymorphism**  
Resolved during program execution, typically through inheritance and method overriding. Also, referred as **Dynamic Binding (Subtype Polymorphism)**.

### Benefits of Polymorphism
- **Code Reusability**   
Reduces code duplication by allowing different objects to share the same interface or methods.
- **Flexibility and Adaptability**   
Easier to add new classes or modify existing ones without impacting other parts of the code.
- **Maintainability**   
Code becomes more modular, readable, and easier to understand, leading to simpler maintenance and debugging.
- **Extensibility**   
Allows for easy addition of new functionalities and behaviors without significant code changes.

## Abstraction
Abstraction in **Object-Oriented Programming (OOP)** is the concept of hiding complex implementation details and showing only the essential features of an object to the user. It allows users to interact with objects at a higher level of abstraction, without needing to understand the intricate inner workings.      
For example, a car's engine or a microwave's internal workings are good examples of abstraction, where users interact with simplified controls without needing to know the underlying mechanisms.

### Core Concepts of Abstraction
- **Hiding Complexity**  
Abstraction simplifies interaction by hiding the complexities of an object's implementation.
- **Essential Features**  
It focuses on presenting only the necessary information and functionalities to the user.

### How to Achieve Abstraction?
- #### Abstract Classes and Interfaces
  **Abstract classes** are used to define a **blueprint** for objects - they specify the methods that must be implemented, but not the implementation details themselves.
  - An **abstract class** is a class that **cannot be instantiated directly**. It can contain both fully implemented methods and abstract methods.
  - Abstract methods are declared using the `abstract` keyword and **must be overridden** in derived classes.
  - The `abstract` keyword is used in TypeScript to mark a class or method as abstract. <br><br>

  An **interface** in TypeScript defines a contract that a class must follow.  
  - It only describes **what** should be done - not **how**. 
  - Interfaces do **not contain any implementation**, only method and property signatures.
  - Interfaces promote **loose coupling** and support **polymorphism**, allowing different classes to implement the same interface in their own way. <br><br>

  **Example (Car abstraction via abstract class):**
  ```ts
  abstract class Car {
    // Abstract methods must be implemented by subclasses
    abstract startEngine(): void;
    abstract stopEngine(): void;
    
    // Concrete method with default behavior
    drive(): void {
      console.log('Driving...');
    }
  }
    
  class ElectricCar extends Car {
    startEngine(): void {
      console.log('Electric engine started silently.');
    }
    
    stopEngine(): void {
      console.log('Electric engine stopped.');
    }
  }
    
  const myCar = new ElectricCar();
  myCar.startEngine(); // Output: Electric engine started silently.
  myCar.drive();       // Output: Driving...
  ```
  **Example (User abstraction via interface):**
  ```ts
    interface IUser {
      login(): void;
      logout(): void;
    }
    
    class Admin implements IUser {
      login() {
        console.log('Admin logged in.');
      }
    
      logout() {
        console.log('Admin logged out.');
      }
    }
    
    const user: IUser = new Admin();
    user.login(); // Output: Admin logged in.
  ```
  
- #### Access Modifiers
  **Access Modifiers** (`public`, `private`, `protected`) are used to control visibility of class members.
  This helps hide internal implementation details while exposing only what's necessary through a controlled interface.
  In this example:
  - The `_password` is hidden using the private modifier.
  - Access is allowed only through public methods like `checkPassword()` - enforcing abstraction and safety.
  
  ```ts
  class User {
    private _password: string;
    
    constructor(private username: string, password: string) {
      this._password = password;
    }
    
    getUsername(): string {
      return this.username;
    }
    
    checkPassword(password: string): boolean {
      return this._password === password;
    }
  }
    
  const user = new User('lala', 'secure123');
  console.log(user.getUsername());        // Output: lala
  console.log(user.checkPassword('123')); // Output: false
  ```

### Benefits of Abstraction:
- **Simplified Usage**    
Makes it easier for users to interact with complex objects by providing a simplified interface.
- **Reduced Complexity**    
By hiding implementation details, abstraction makes the code easier to understand, maintain, and modify.
- **Improved Reusability**    
Abstraction promotes code reusability by allowing different parts of the program to interact with objects through a common interface.

## Documentation and References
- [Introduction of Object Oriented Programming](https://www.geeksforgeeks.org/dsa/introduction-of-object-oriented-programming/)
- [Object-Oriented Programming : Polymorphism](https://medium.com/@hasan_denli/object-oriented-programming-polymorphism-fc6c7782f93b)