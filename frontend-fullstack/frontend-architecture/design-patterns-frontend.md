# Front-end Design Patterns
Design patterns are **reusable solutions** to common problems that occur at a lower level in software design - such as **component interaction**, **state management**, **rendering logic**, and **data flow.**
- These patterns are used within a high-level architecture to organize local implementation details, ensuring consistency, maintainability, and readability.
- They don’t define the full structure of an application (like architecture patterns do), but they shape how components, logic, and data behave and interact within that structure.
- Design patterns are broadly categorized into three groups also known as `Gang of Four (GoF) Design Patterns`: **Creational**, **Structural**, and **Behavioral**. Additionally, there is a **UI design patterns** category which introduces design patterns that are more specific to front-end UI organization.

This list covers many of the **fundamental design patterns** commonly used within architectural patterns in **modern front-end development**. The choice of pattern typically depends on the project's scale, team size, performance requirements, and long-term maintainability goals.

## Creational Design Patterns
These patterns deal with **object creation mechanisms**, aiming to create objects in a manner suitable for the situation while increasing the flexibility and reuse of the code. They abstract the instantiation process, allowing the system to determine which concrete class to instantiate. In frontend development, this often relates to how components, services, or data models are instantiated or configured, providing flexibility in setting up application parts.

- **Singleton Pattern**
    - Restricts the instantiation of a class to one "single" instance and provides a global point of access to it.
    - **Use Cases:** Managing global states, routing services, or application configurations where only one instance is needed throughout the application's lifecycle.

## Structural Design Patterns
These patterns are concerned with **how classes and objects are composed and organized to form larger, more complex structures** within an application. They focus on simplifying the design by identifying clear relationships between entities, promoting flexibility and efficiency in building robust applications. In frontend development, this often translates to effectively composing UI components, modules, and services to create adaptable, maintainable, and manageable user interfaces.

- **Facade Pattern**
    - Provides a simplified interface to a larger, more complex subsystem, making it easier to use.
    - **Use Cases:** Wrapping complex third-party libraries or internal systems with a clean, easy-to-use API.

- **Adapter Pattern**
    - Allows the interface of an existing class to be used as another interface, enabling incompatible interfaces to work together.
    - **Use Cases:** Integrating legacy systems with new applications, reusing existing code, or making different libraries/frameworks compatible.

- **Dependency Injection (DI) Pattern**
    - A pattern where a component receives its dependencies from an external source rather than creating them itself, promoting Inversion of Control and decoupling.
    - While not originally part of the GoF catalog, DI is a widely adopted structural pattern in frontend frameworks.
    - **Use Cases:** Essential for creating modular, testable, and maintainable code in large applications. Heavily integrated into frameworks like Angular.

- **Strategy Pattern**
    - Involves defining a group of different algorithms and making it possible to choose and switch between them as needed while a program is running.
    - **Use Cases:** Ideal for scenarios where an object's behavior needs to be selected and switched at runtime, promoting flexible and easily extensible solutions for varying algorithms (e.g., different sorting methods, payment options, or validation rules).

## Behavioral Design Patterns
These patterns are concerned with **algorithms and the assignment of responsibilities between objects** within an application. They focus on **how objects interact and communicate** to accomplish tasks, promoting flexibility in their collaboration and how responsibilities are distributed. In frontend development, this often involves managing user interactions, state changes, and the flow of data within the user interface, making it easier to add or change behaviors without significantly altering the core UI elements.

- **Observer Pattern**
    - Defines a one-to-many dependency between objects so that when one object (the "subject") changes state, all its dependents (the "observers") are notified and updated automatically.
    - **Use Cases:** Event-driven systems, state management, and scenarios where changes in one part of the application need to trigger updates in other, independent parts.

- **Publisher/Subscriber Pattern (Pub/Sub)**
    - Similar to Observer but with a clearer separation. Publishers send messages to a "channel" or "topic" without knowing which subscribers will receive them. Subscribers listen to specific channels.
    - **Use Cases:** Decoupled communication between components, especially in larger applications or when integrating with external services.

## UI Design Patterns
These patterns focus on effective ways to structure and manage individual UI components, promoting reusability, testability, and clear separation of concerns at the component level.

- **Container-Presentation Pattern (Smart/Dumb Components)**
    - This pattern separates components into two main types based on their responsibilities:
        - **Container (Smart) Components:** Are concerned with **how things work**. They handle data fetching, state management, and business logic. They often do not have much UI markup themselves.
        - **Presentation (Dumb) Components:** Are concerned with **how things look**. They receive data and callbacks via props (or inputs) and simply render UI elements. They are typically stateless and reusable.
    - **Use Cases:** Widely used in modern component-based frameworks (like React, Angular, Vue) to improve component reusability, testability, and maintainability by clearly separating concerns between data logic and UI rendering. It simplifies component testing and fosters a cleaner component hierarchy.
