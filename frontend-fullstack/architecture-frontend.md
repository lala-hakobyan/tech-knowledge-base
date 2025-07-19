# Frontend Architecture
Frontend architecture refers to the **structure and organization of the user interface (UI)** and its related code in a web application.
- It encompasses the **decisions, patterns, tools, and processes** that define how UI components are built, interact with each other and with backend services, and how the codebase evolves over time.
- A well-designed frontend architecture ensures **scalability**, **maintainability**, and **performance**, while also enabling **cross-functional teams** (developers, designers, QA) to collaborate effectively through clear separation of concerns and standardized conventions.
- In essence, it provides a solid **foundation for the user-facing part** of a web application - making it **structured**, **efficient**, and **adaptable** to future requirements.

This documentation introduces **key aspects of frontend architecture** and explores **decision-making strategies** for building **scalable** and **maintainable** systems. It is based on **my own experience**, **insights from the community**, and **official best practices.**

## Key Aspects of Frontend Architecture

- **Component-based Design**  
Breaking down the UI into reusable, independent components.

- **Code Organization**  
Structuring the frontend code in a way that is logical, maintainable, and scalable.
 
- [**Design Patterns**](#design-patterns)   
Implementing established patterns for managing data flow, user interactions, and application logic.

- **Performance Optimization**    
Ensuring the application loads quickly, responds efficiently, and uses resources effectively.

- [**Rendering Models**](#rendering-models)   
Choosing the appropriate rendering model (**CSR**, **SSR**, **SSG**) based on project needs to improve performance, accessibility, and loading speed.

- [**Application Architecture Types**](#application-architecture-types)    
Selecting the right architectural approach (**Monolith**, **Micro-frontends**, **Modular**, etc.) based on application complexity and needs to support **long-term maintainability** and **scalability**.

- **State Management**   
Applying effective strategies to handle and synchronize application state across components.

- **Accessibility and SEO**   
Following accessibility standards and SEO best practices to enhance usability and visibility.

- **Technology Stack**   
Selecting suitable frameworks, libraries, and tools based on project requirements.

- **Integration with Backend**  
Managing smooth and secure communication between the frontend and backend systems.

- **Scalability and Maintainability**   
Designing the architecture to accommodate future growth and changes in requirements.

- **Testing**   
Defining strategies to test UI components and ensure application reliability.

- **UI/UX Considerations**   
Balancing functionality with user experience and visual appeal.

- **Security**   
Applying best practices to safeguard user data and prevent vulnerabilities.

- **Deployment**  
Planning how the frontend will be built, deployed, and continuously delivered.


  
## Design Patterns
Design patterns are **reusable solutions** to common problems that occur at a lower level in software design - such as **component interaction**, **state management**, **rendering logic**, and **data flow.** 
- These patterns are used within a high-level architecture to organize local implementation details, ensuring consistency, maintainability, and readability.
- They don’t define the full structure of an application (like architecture patterns do), but they shape how components, logic, and data behave and interact within that structure.
- Design patterns are broadly categorized into three groups also known as `Gang of Four (GoF) Design Patterns`: **Creational**, **Structural**, and **Behavioral**. Additionally, there is a UI design patterns category **UI design patterns** category which introduces design patterns that are more specific to front-end UI organization.

This list covers many of the fundamental design patterns (often used within architectural patterns) found in modern front-end development. The choice of pattern often depends on the project's scale, team size, performance requirements, and long-term maintainability goals.

### Creational Design Patterns
These patterns deal with **object creation mechanisms**, aiming to create objects in a manner suitable for the situation while increasing the flexibility and reuse of the code. They abstract the instantiation process, allowing the system to determine which concrete class to instantiate. In frontend development, this often relates to how components, services, or data models are instantiated or configured, providing flexibility in setting up application parts.

- **Singleton Pattern**
    - Restricts the instantiation of a class to one "single" instance and provides a global point of access to it.
    - **Use Cases:** Managing global states, routing services, or application configurations where only one instance is needed throughout the application's lifecycle.
  
### Structural Design Patterns
These patterns are concerned with **how classes and objects are composed and organized to form larger, more complex structures** within an application. They focus on simplifying the design by identifying clear relationships between entities, promoting flexibility and efficiency in building robust applications. In frontend development, this often translates to effectively composing UI components, modules, and services to create adaptable, maintainable, and manageable user interfaces.

- **Facade Pattern**
    - Provides a simplified interface to a larger, more complex subsystem, making it easier to use.
    - **Use Cases:** Wrapping complex third-party libraries or internal systems with a clean, easy-to-use API.    

- **Adapter Pattern**
    - Allows the interface of an existing class to be used as another interface, enabling incompatible interfaces to work together.
    - **Use Cases:** Integrating legacy systems with new applications, reusing existing code, or making different libraries/frameworks compatible.    

- **Dependency Injection (DI) Pattern**
    - A pattern where a component receives its dependencies from an external source rather than creating them itself, promoting Inversion of Control and decoupling.
    - While not originally part of the GoF catalog, DI is a widely adopted structural pattern in frontend frameworks
    - **Use Cases:** Essential for creating modular, testable, and maintainable code in large applications. Heavily integrated into frameworks like Angular.    

- **Strategy Pattern**
    - Involves defining a group of different algorithms and making it possible to choose and switch between them as needed while a program is running.
    - **Use Cases:** Ideal for scenarios where an object's behavior needs to be selected and switched at runtime, promoting flexible and easily extensible solutions for varying algorithms (e.g., different sorting methods, payment options, or validation rules).

### Behavioral Design Patterns
These patterns are concerned with **algorithms and the assignment of responsibilities between objects** within an application. They focus on **how objects interact and communicate** to accomplish tasks, promoting flexibility in their collaboration and how responsibilities are distributed. In frontend development, this often involves managing user interactions, state changes, and the flow of data within the user interface, making it easier to add or change behaviors without significantly altering the core UI elements.

- **Observer Pattern**
   - Defines a one-to-many dependency between objects so that when one object (the "subject") changes state, all its dependents (the "observers") are notified and updated automatically.
   - **Use Cases:** Event-driven systems, state management, and scenarios where changes in one part of the application need to trigger updates in other, independent parts.   

- **Publisher/Subscriber Pattern (Pub/Sub)**
   - Similar to Observer but with a clearer separation. Publishers send messages to a "channel" or "topic" without knowing which subscribers will receive them. Subscribers listen to specific channels.
   - **Use Cases:** Decoupled communication between components, especially in larger applications or when integrating with external services.  

### UI Design Patterns
These patterns focus on effective ways to structure and manage individual UI components, promoting reusability, testability, and clear separation of concerns at the component level.

- **Container-Presentation Pattern (Smart/Dumb Components)**
  - This pattern separates components into two main types based on their responsibilities:
      - **Container (Smart) Components:** Are concerned with *how things work*. They handle data fetching, state management, and business logic. They often do not have much UI markup themselves.
      - **Presentation (Dumb) Components:** Are concerned with *how things look*. They receive data and callbacks via props (or inputs) and simply render UI elements. They are typically stateless and reusable.
  - **Use Cases:** Widely used in modern component-based frameworks (like React, Angular, Vue) to improve component reusability, testability, and maintainability by clearly separating concerns between data logic and UI rendering. It simplifies component testing and fosters a cleaner component hierarchy.



## Rendering Models
Choosing the correct rendering model(**CSR**, **SSR**, **SSG**) based on your project needs ensures good performance, accessibility and faster loading times.

The following frontend rendering models are available today:
- **Client-Side Rendering (CSR)**  
  Means the browser renders HTML from JavaScript after downloading it.  

- **Server-Side rendering (SSR)**  
  The server generates the HTML for the page, which is then sent to the browser to render.  

- **Static Site Generation (SSG)**  
  Pages are pre-built at build time and served as static files.  

- **Partial/Incremental Hydration**  
This is an optimization technique used with SSR or SSG, where only specific, interactive parts of the pre-rendered HTML are **"hydrated"** with client-side JavaScript, rather than the entire page. 
  - It aims to **reduce the amount of JavaScript** sent to the browser and **improve interactivity** by making only necessary components interactive, and often loading other components lazily. 
  - This is commonly implemented through patterns like **"Islands Architecture"** or **"Server Components"** in modern frameworks.

### Rendering Models: Comparison and When to Choose Each

| Rendering Type                    | ✅ Pros                                                                                   | ❌ Cons                                                                                      | How it works?                                                                           | When to Choose                                                                                                            |
|-----------------------------------|-------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------|
| **Client-Side (CSR)**             | - Simple dev setup<br> - Full browser API support<br> - Lowest server cost                | - Slower performance<br> - Poor SEO<br> - JS must fully load to render                      | The server sends the initial HTML, client updates with JavaScript                       | **SPAs, Web applications, low-SEO needs, offline/PWA use cases**                                                           |
| **Server-Side (SSR)**             | - Fast initial load<br> - Great SEO<br> - Server-side data fetching                       | - Higher server cost<br> - No browser-only libs<br> - Angular runs on each request          | The server renders HTML, sends to the client for display                                | **SEO-critical sites, user-specific data on first load, content heavy websites**                                           |
| **Prerendering (SSG)**            | - Fastest page load<br> - Great SEO<br> - CDN caching<br> - Zero server load per request  | - Build-time data only<br> - Slower build time<br> - Not for dynamic or user-specific pages | The server generates static HTML, the client uses JavaScript to update                  | **Websites that require fast initial load times and dynamic updates, static content, marketing pages, blogs, docs**        |
| **Partial/Incremental Hydration** | - Improved performance<br> - Reduced JavaScript<br> - Fine-grained control                | - More complex setup<br> - Framework-dependent<br> - Still evolving as a standard           | SSR/SSG pre-renders HTML; only selected interactive components are hydrated client-side | **Sites that benefit from fast static delivery but still need interactivity (e.g., dashboards, e-commerce product pages)** |



## Application Architecture Types
Choosing the right frontend architecture depends on the specific needs and complexity of the application. 
- Factors like **team size**, **development speed**, **maintainability**, and **scalability** should be considered when selecting an architecture.

### High-Level Frontend Architecture Patterns
**High-level front-end architecture patterns** (also called **architectural styles**) define the overall **structure and organization** of a front-end application. 
- These patterns govern how the **application is divided**, how **features are grouped**, how **codebases are managed**, and how **teams collaborate**.
- Unlike design patterns (which focus on internal logic and interactions), high-level architecture patterns deal with **macro-level decisions** that **impact scalability, maintainability, performance, and team autonomy**.

High-level front-end architecture patterns answer questions like:
- Is the frontend built as one **large unit** or **split into modules**?
- How do **different parts** of the application **communicate**?
- Can **multiple teams** work **independently**?
- How is the **code deployed and maintained**?

#### 🔹 Key Characteristics of High-Level Architecture Patterns
- Influence codebase **structure** and **module boundaries**
- Determine **team ownership models** (e.g., feature teams vs platform teams)
- Affect **build** and **deployment strategies**
- Enable **scalability** and **parallel development**

#### 🔹 Breakdown of High-Level Frontend Architecture Patterns
1. **Monolithic Architecture**
   - In a monolithic architecture, the entire frontend is built as a **single, self-contained unit**.
   - This approach can be simple for smaller applications but becomes **challenging to manage and scale** as the application grows.
   - Code is often **tightly coupled**, which can make it difficult to isolate changes or introduce new features without affecting other parts of the application. This tight coupling often extends to the backend, with both frontend and backend frequently residing in the same repository.    

2. **Modular Architecture**
   - Modular architecture involves breaking down the frontend into **independent modules** or sections.
   - Each module can be **developed and maintained separately**, promoting better organization and code reuse.
   - This approach can be more scalable and maintainable than monolithic architectures.    

3. **Component-Based Architecture**
   - Component-based architecture focuses on building the frontend from **reusable UI components**.
   - Components **encapsulate their own logic and rendering**, making them **independent** and **easy to integrate** into different parts of the application.
   - Popular frameworks like **React**, **Angular**, and **Vue.js** are well-suited for component-based development.    

4. **Micro-frontend Architecture**
   - Micro-frontends extend the **concept of microservices to the frontend**, breaking it down into **independent**, **smaller** applications that can be **developed and deployed separately**.
   - In micro-frontend architecture, we typically have a hosting app (also called the **shell**) and multiple **MFE** (**micro-frontend**) apps.
   - Each micro-frontend can be built using different technologies and teams, enabling greater **flexibility** and **agility**.
   - This approach is suitable for **large**, **complex** applications with **diverse teams and technologies**.
   - In pure micro-frontend architecture, **rendering** of micro-frontends is typically handled at **runtime in the browser**. This means that once the setup is done, the shell (host) app does not need to be redeployed when a new version of any micro-frontend is deployed.    

5. **Hybrid/Mixed Architecture**
   - This approach **combines** elements from **two or more distinct architectural patterns** to leverage their individual strengths and mitigate their weaknesses for specific parts of an application.
   - For example, a **large application** might use a **micro-frontend architecture** for its core modules, but a **highly interactive dashboard section** within one of those micro-frontends might heavily employ a **component-based architecture** with **sophisticated state management**.
   - Another common hybrid might involve a foundational **monolithic structure** for stable, rarely changing parts, combined with a **modular design for more dynamic sections**, or even a gradual transition from monolithic to micro-frontends.
   - This approach is highly adaptable and practical for complex projects that don't fit perfectly into a single pattern, or for organizations gradually modernizing existing systems.


### Internal Application Architecture Patterns
**Internal Application Architecture Patterns** (sometimes referred to as **Architectural Design Patterns**) focus on the organization of code and data flow *within* a single, cohesive frontend application or a specific module/component of a larger system. They address concerns like separation of responsibilities, state management, and interaction between UI layers.

These patterns answer questions like:
- How is the **user interface** logic separated from **the data**?
- How does **data flow** through the application?
- How does the **UI update** in response to data changes or user interactions?

#### 🔹 Breakdown of Internal Application Architecture Patterns
1. **MVC (Model-View-Controller)**
    - Separates the application into three interconnected components:
        - **Model:** Manages the application's data and business logic.
        - **View:** Responsible for displaying the data to the user (the UI).
        - **Controller:** Handles user input, updates the Model, and selects the View.
    - **Use Cases**  
      A classic pattern widely used in many frameworks, particularly for traditional server-rendered applications or as a foundational concept in early client-side frameworks like **AngularJS**.    

2. **MVVM (Model-View-ViewModel)**
    - A variant of MVC that emphasizes the separation of concerns, particularly for UI development.
        - **Model:** Same as MVC, represents data and business logic.
        - **View:** The actual UI elements, purely presentational.
        - **ViewModel:** An abstraction of the View that exposes data and commands, handling the View's display logic and acting as an intermediary between the View and the Model. It often uses data binding to synchronize View and ViewModel.
    - **Use Cases**  
      Core to frameworks with strong data binding like **Angular** and **Vue.js**, used when complex data binding and UI logic are involved.   

3. **Flux Architecture**
    - Introduced by **Facebook (Meta)** for managing application state in **complex component-based applications**. It enforces a unidirectional data flow with four main components:
        - **Actions:** Payloads of data sent to the Dispatcher.
        - **Dispatcher:** Central hub that manages the flow of data to the stores. Receives actions from views and dispatches them to the appropriate stores.
        - **Stores:** Hold the application's state and logic for a particular domain.
        - **Views:** Presentable UI, usually React components, that retrieve data from stores and dispatch actions.
    - **Use Cases**  
      Ideal for applications with complex state management, aiming for predictable updates and easier debugging (e.g., **Redux** is built on Flux principles).  


### Frontend Application Types
In addition to common architecture patterns, front-end applications can also be classified by their **runtime behavior** and **delivery approach**:

- **Single Page Applications (SPAs)**    
The entire application is loaded in a **single HTML page** and **updates dynamically** in the browser **without full page reloads**, often using client-side rendering.    

- **Server-Side Rendered (SSR) Applications**  
The initial HTML for each page is **generated on the server for every request**. This provides **fast initial load times** and **good SEO**, with the client-side JavaScript then taking over to make the page interactive (**hydration**).   
  
- **Isomorphic (Universal) Applications**  
These are applications that **render on both the server and client**. This combines the benefits of **SSR** (fast initial load, SEO) with **client-side interactivity**, allowing the same codebase to run in both environments.    

- **Static Site Applications**  
Built and served as **static HTML/CSS/JS** files. These are pre-rendered at build time, resulting in **extremely fast load times and easy hosting**. They are **less dynamic** unless paired with client-side JavaScript or APIs.    

- **Jamstack Applications**  
A modern approach using **pre-rendered pages** (via **Static Site Generators** or **SSG**), **headless APIs for dynamic data**, and **CDNs for fast global delivery**. It combines the **speed and security** of static sites with **dynamic functionality** via client-side JavaScript and serverless functions.  

- **Partial Server-Side Rendering (e.g., Server Components/Islands Architecture)**  
Only specific, dynamic parts of a page are rendered on the server, while other parts remain static or client-side rendered. This allows for fine-grained control over what gets rendered on the server, **improving performance** and **reducing JavaScript bundle sizes** by sending only necessary client-side code. Often referred to as **"Server Components"** (e.g., React Server Components) or **"Islands Architecture."**    


### Frontend Repository Structures
- **Monorepo**  
A monorepo is a **single version-controlled repository** that holds the code for multiple projects, services, or components - sometimes across an entire organization.  
  - While it **increases pull request size**, makes it **easier to accidentally introduce bugs** in unrelated parts of the codebase (if rules aren’t enforced), and can **make commit history harder to read**, it also has key advantages:  
  Teams can **leverage shared code functionality** more easily since everything lives in one place.  
  - To keep things maintainable, it’s critical to define **clear ownership boundaries** between projects and establish **rules for cross-project interactions**.    

- **Polyrepo**  
A polyrepo structure uses **separate, independent repositories** for each project or service. This provides teams with **greater autonomy**, reducing the risk of interfering with each other’s code and making development workflows more isolated.  
  - However, it introduces **operational overhead** - each repository requires its own build and deployment pipelines, and **code duplication becomes more likely** if shared logic isn’t abstracted out.  
  - When using polyrepos, it’s important to invest in **shared libraries** and **centralized utilities** to maintain consistency and avoid tight coupling between independently maintained projects.

#### 🔹 Comparison: Monorepo vs Polyrepo

| Category     | **Monorepo**                                                                        | **Polyrepo**                                                                    |
|--------------|-------------------------------------------------------------------------------------|----------------------------------------------------------------------------------|
| **Pros**     | Easier **code sharing**, unified tooling, simpler refactoring across projects       | Team independence, reduced risk of cross-team bugs, smaller and focused repos   |
| **Cons**     | Larger PRs, commit noise, risk of cross-project bugs, slower CI/CD if not optimized | Higher setup overhead, possible code duplication, harder to enforce consistency |
| **Best for** | Teams/projects that require **tight integration** and **shared codebases**          | Teams needing **autonomy**, **separate release cycles**, or **distinct domains** |



### Frontend Architecture Implementation Mechanisms
There are various mechanisms for implementing frontend architecture patterns, and they can also be **combined** to achieve the desired architecture.

---

#### 🔹 Module Federation

---

**Module Federation** is a feature introduced in Webpack 5 that allows multiple independently built and deployed JavaScript applications to **share code at runtime**.

It is the foundation of modern **micro-frontend architectures**, where each app (or module) can be **developed**, **deployed**, and **updated independently**.

---

**Core Concepts**

Module Federation has three main concepts:

  - **Shell (Host)**  
  The main app that bootstraps and integrates other apps (remotes) at runtime.

  - **Remote App**  
  A self-contained micro-frontend that exposes components/modules for others to consume via `remoteEntry.js` (generated at build time).

  - **`remoteEntry.js`**  
  A self-invoking JavaScript manifest file that bootstraps a shared module system:
      - Maps module names (e.g., `./UserCard`) to actual implementations
      - Contains logic to load and resolve shared dependencies
      - Hooks into the host’s module registry dynamically
      - **Note**: It does **not** use ES6 `import/export` syntax. Instead, it uses **Webpack's** internal runtime (`__webpack_require__`) for defining modules.

---

**How Module Federation Works**

1. **Build Time**  
   - Each **Remote App** defines what it exposes (components, services, etc.) in its **Webpack config**.
   - Webpack generates a `remoteEntry.js` file:
       - A manifest that defines **what modules are available**
       - And **how they can be dynamically loaded**

2. **Runtime**  
   - The **Host App (Shell)** dynamically loads modules from the Remote Apps via URL.
   - Remote apps behave like local modules within the Shell.
   - **No full page reloads or redeployments** are required to integrate changes.

---

**Module Federation Integration Steps (Angular Example)**

1. **Remote App Configuration (`webpack.config.js`)**

    ```ts
    new ModuleFederationPlugin({
      name: "user-mfe", // This is the actual unique name of your remote application, and it should match the name specified in the shell's Webpack config under remotes.
      filename: "remoteEntry.js", // File to be loaded by shell
      exposes: {
        './UserCard': './src/app/user-card/user-card.component.ts', // Component to expose
      },
      shared: share({
        "@angular/core": { singleton: true, strictVersion: true, requiredVersion: 'auto' },
        "@angular/common": { singleton: true, strictVersion: true, requiredVersion: 'auto' },
        "@angular/router": { singleton: true, strictVersion: true, requiredVersion: 'auto' }
      })
    })
    ```

2. **Shell App Configuration (webpack.config.js)**
    ```ts
    new ModuleFederationPlugin({
      remotes: {
        'user-mfe': 'user-mfe@http://localhost:4201/remoteEntry.js', // Explicit remote entry, name must match with remote application *unique name*
      },
      shared: share({
        "@angular/core": { singleton: true, strictVersion: true, requiredVersion: 'auto' },
        "@angular/common": { singleton: true, strictVersion: true, requiredVersion: 'auto' },
        "@angular/router": { singleton: true, strictVersion: true, requiredVersion: 'auto' }
      })
    });
    ```

3. **Load Remote Component in Shell (Runtime)**   
    Depending on the technology (`Angular`, `React`, etc.), the Shell app loads the remote component during runtime. In Angular, this is typically done when the corresponding lazy-loaded route is accessed.  
    
    **Example in Angular:** Load Angular Remote Component in `app.routes.ts` as the `user-card` route is reached
    ```ts
    export const routes: Routes = [
        {
            path: 'user-card',
            loadChildren: () =>
                loadRemoteModule({
                    type: 'module',
                    remoteEntry: 'http://localhost:4201/remoteEntry.js',
                    exposedModule: './UserCard'
                }).then(m => m.UserCardModule)
        }
    ];
    ```

    **Example in Angular (if not web component):** Load Angular Remote Component in app component and convert it to the Angular component
    ```ts
    // app.component.ts
    
    @Component({
      selector: 'app-root',
      templateUrl: './app.component.html',
      styleUrls: ['./app.component.scss'],
    })
    export class AppComponent implements OnInit, OnDestroy {
      title = 'shell-app';
    
      // Get a reference to the <ng-container> element in the template
      @ViewChild('userCardContainer', { read: ViewContainerRef, static: true })
      userCardContainer!: ViewContainerRef;
    
      private userCardComponentRef: ComponentRef<any> | null = null; // To hold reference to the loaded component
    
      constructor() {}
    
      ngOnInit(): void {
        this.loadUserCard();
      }
    
      async loadUserCard(): Promise<void> {
        // Clear any previously loaded component if you want to load fresh
        if (this.userCardComponentRef) {
          this.userCardComponentRef.destroy();
          this.userCardContainer.clear();
        }
    
        try {
          // Dynamically load the remote module
          const module = await loadRemoteModule({
            type: 'module',
            remoteEntry: 'http://localhost:4201/remoteEntry.js', // URL of the remoteEntry.js
            exposedModule: './UserCard', // The name of the exposed module as defined in remote's webpack.config.js
            remoteName: 'user-mfe', // The name of the remote as defined in shell's webpack.config.js
          });
    
          // Get the component class from the loaded module
          const UserCardComponent = module.UserCardComponent;
    
          // Create an instance of the remote component inside our container
          this.userCardComponentRef = this.userCardContainer.createComponent(UserCardComponent);
    
          // You can now interact with the component instance if needed
          // For example, setting an input property: this.userCardComponentRef.instance.userId = '123';
    
        } catch (error) {
          console.error('Failed to load remote UserCardComponent:', error);
          // Handle error, e.g., display a fallback message
          this.userCardContainer.clear();
          this.userCardContainer.element.nativeElement.innerText = 'Failed to load user card.';
        }
      }
    
      ngOnDestroy(): void {
        // Clean up the dynamically created component when the host component is destroyed
        if (this.userCardComponentRef) {
          this.userCardComponentRef.destroy();
        }
      }
    }
    ```

    ```html
    <h1>Shell Application Dashboard</h1>
    
    <div class="main-content">
        <div class="local-widgets">
            <h2>Local Widgets</h2>
            <p>This is a local component or static content.</p>
            <app-some-local-widget></app-some-local-widget>
        </div>
    
        <div class="remote-component-container">
            <h2>Remote User Card</h2>
            <ng-container #userCardContainer></ng-container>
        </div>
    </div>
    ```

    ⚠️ **Important:**  
      - If you expose components this way, the Shell and all MFEs must use the same framework (e.g., Angular).
      - To make micro-frontends framework-agnostic, expose components as Web Components instead.
      - In that case we would be able to load `remoteentry.js` and just use the component in html like this:
         ```html
            <user-card userId="currentId"></user-card>
         ```

---

**Benefits of Module Federation**
- **Runtime Integration**  
  Module Federation enables the **dynamic loading of remote modules at runtime**. This means that parts of your application can be **deployed** and **updated independently** without requiring a full redeployment of the entire application.
- **Code Sharing**  
  It allows for the **sharing of common dependencies and libraries** between the **host application** and **remote modules**, reducing bundle size and improving performance by avoiding duplicate downloads.
- **Independent Development and Deployment**  
  Teams can work on different micro frontends simultaneously and **deploy them independently** without causing any conflicts, which leads to **faster development cycles** and **easier maintenance**.
- **Scalability**  
  Module Federation promotes scalability by allowing you to **scale individual parts of your application** based on demand.

---

**Pitfalls with Module Federation**
- **Increased Complexity**  
  Setting up and managing Module Federation, especially with shared dependencies and versioning, can introduce **complexity** and a **steeper learning curve**.
- **Debugging Challenges**  
  Debugging issues related to runtime module loading and shared dependencies can be **more difficult** than in monolithic applications.
- **Potential for Version Mismatches**  
  Careful management of shared dependencies and their versions is crucial to avoid runtime errors and **ensure compatibility between federated modules**.
- **Overhead for Initial Configuration**  
  The **initial setup and configuration** of Webpack Module Federation may involve **significant upfront effort**.
- **Limited Tree-Shaking for Shared Dependencies**  
  Webpack's **tree-shaking capabilities** for shared dependencies across federated modules might be less effective than within a single application, potentially leading to **larger bundle sizes** if not managed carefully.

---

#### 🔹 Nx Monorepo

---

A monorepo is a **single git repository** that holds the source code for multiple applications and libraries, along with the tooling for them.

A **naive implementation of a monorepo** is code collocation where code is just shared within teams without any rules, and where combining all the code from multiple repositories into the same repo can lead to problems:

- **Running Unnecessary Tests**  
  **All tests** in the entire repository **run to ensure nothing breaks** from a given change, even in projects that are **unrelated to the actual change**.
- **No Code Boundaries**  
  Bugs and inconsistencies are introduced when developers from other teams change or modify code in your project that was not meant to be modified.
- **Inconsistent Tooling**  
  Each project uses its **own set of commands** for running tests, building, serving, linting, deploying, etc. Inconsistency creates **mental overhead** remembering which commands to use from project to project.

Nx provides tools to give you the benefits of a monorepo without the drawbacks of simple code collocation:

- **Consistent Command Execution**  
  Executors allow for **consistent commands** to test, serve, build, and lint each project, using various tools.
- **Consistent Code Generation**  
  Generators allow you to **customize and standardize organizational conventions and structure**, removing the need to perform the same manual setup tasks repeatedly.
- **Affected Commands**  
  Nx's affected commands analyze your source code and the context of the changes, and **only run tasks on affected projects**.
- **Remote Caching**  
  Nx provides **local caching** and **support for remote caching of command execution**. With remote caching, when someone on your team runs a command, others can reuse those artifacts to speed up their command executions, reducing times from minutes to seconds. Nx helps you **scale development** for large applications and libraries through distributed task execution and incremental builds.

---

**Benefits of Nx Monorepo**

1. **Code Sharing, Collaboration & Ownership**
    - Share code across apps using well-defined, **reusable libraries**.
    - Visibility into all projects promotes **team collaboration** and **faster onboarding**.
    - **Ownership is enforced** using `CODEOWNERS`, limiting who can approve changes per project.
    - Libraries expose **constrained public APIs** and follow defined **dependency rules**.

2. **Tooling, Consistency & Developer Experience**
    - Nx extends Angular CLI with **monorepo-focused tools**.
    - **Unified command execution** (build, test, lint, serve) via executors.
    - Custom scaffolding via generators to **automate and standardize** project structure.
    - Integration with **modern tools**: `Jest`, `Cypress`, `Storybook`, etc.

3. **Performance: Build, Test & Deploy at Scale**
    - Affected commands detect what changed and **only rebuild/test relevant projects**.
    - **Caching** (local + remote) **speeds up repeated command execution** across teams.
    - Incremental builds and distributed task execution support **large-scale applications**.

4. **Architecture & Maintainability**
    - Architectural boundaries enforce **maintainability** as the monorepo grows.
    - Generates real-time, **accurate project dependency diagrams**.
    - **Scalable structure** for organizing apps and libraries under `apps/` and `libs/`.

---

**Pitfalls with Nx Monorepo**

1. **Repository Size & Complexity**
    - Working on a single project still requires **cloning the full repository**.
    - Larger monorepos can **slow down Git operations** (e.g. `git status`, `git log`).
    - **Requires tooling** (like Nx) to keep builds and tests efficient at scale.

2. **Potential for Accidental Coupling**
    - Without enforced boundaries, teams might unintentionally **create tight dependencies** across projects.
    - **Missing or misconfigured lint rules** can lead to architecture violations.
    - Code reuse without clear APIs can introduce **hidden dependencies**.

3. **Commit History & Ownership Traceability**
    - Single Git history across many teams makes it **harder to trace the origin of specific changes**.
    - Contributions from many teams can cause **noise in logs and pull requests**.
    - **Code reviews may become less focused** unless CODEOWNERS and scopes are enforced.

4. **Tooling & Learning Curve**
    - Developers must understand **Nx-specific tooling and configuration**.
    - Advanced setup (like distributed caching or custom generators) requires **upfront effort**.
    - **Onboarding** new team members may take **longer** compared to isolated projects.

---

#### 🔹 Hybrid: Monorepo + Polyrepos (npm packages)

---

In this approach:

- The **shell**, which hosts the micro-frontends, is organized as a **monorepo**.
- Each **micro-frontend** is developed in a **separate Git repository** and deployed as an **npm package** (library).
- The shell includes a **wrapper** for each micro-frontend that **lazy loads** the corresponding module.
- A **bundler** (e.g., Webpack) in the shell assembles all the logic into a single JS bundle at **build time**, including lazy-loaded micro-frontend modules.
- This is **not a pure micro-frontend architecture**, because the loading of micro-frontends happens at **build time**, not **runtime**.
- As a result, if a new version of a micro-frontend is released, the **shell must update the package version and be redeployed**.
- Despite this limitation, this approach is still **widely used**, especially in **Angular** ecosystems.
- It allows for **team independence**, **code isolation**, and **conflict avoidance**, while maintaining **strong control** over dependencies and integration.

---

**Summary Table** 

| Advantages                                                                 | Pitfalls                                                                                   |
|----------------------------------------------------------------------------|--------------------------------------------------------------------------------------------|
| ✅ Simple integration using npm packages                                   | ❌ Requires shell redeployment after each micro-frontend update                            |
| ✅ Encourages code isolation and team independence                         | ❌ Not true runtime micro-frontend loading                                                 |
| ✅ Strong compatibility with Angular and TypeScript-based projects         | ❌ All micro-frontends must use the same framework (typically Angular)                    |
| ✅ Easier to manage with CI/CD pipelines using standard versioning         | ❌ Tight coupling between shell and micro-frontends compared to runtime-based approaches   |


---

#### 🔹 Web Components

---

**What are Web Components?**  
Web Components are a suite of **web platform APIs** that allow developers to create **reusable, custom HTML elements**.
They are built on three core technologies:
1. **Custom Elements**  
   These allow you to define your own HTML tags with specific behavior and functionality. For example, you could create a `<user-card>` element that has its own styling and click behavior.
2. **Shadow DOM**  
   This provides a way to **encapsulate the styling and markup of a component**, preventing it from interfering with or being affected by the rest of the page. This means you can use the same `CSS` class names in different components without worrying about conflicts.
3. **HTML Templates**  
   These define **reusable chunks of HTML** that serve as **blueprints** for custom elements.

---

**Core Concepts of Web Components in MFE Architecture**
In **Micro-Frontend (MFE) architecture**, Web Components are a powerful tool for building **reusable, encapsulated UI elements** that can be **shared across different applications and frameworks**. They provide a modular and maintainable approach to UI development, making them an ideal fit for micro frontend architectures.

Below are core concepts of web components which play key role in MFE Architecture: 
- **Reusability**  
   Web Components enable the creation of **reusable UI components** that can be shared across different micro-frontends. This **reduces code duplication** and makes it easier to maintain consistency across the application.
- **Encapsulation**  
   The `Shadow DOM` provides strong encapsulation, ensuring that each **component's styles and scripts are isolated** from the rest of the application. This prevents conflicts and makes it easier to develop and maintain individual micro frontends.
- **Framework Agnostic**  
   Web Components are a **browser-native technology**, meaning they can be used with **any JavaScript framework** or **even without a framework**. This allows teams to choose the best framework for their needs without worrying about compatibility issues with other parts of the application.
- **Independent Development and Deployment**  
   Each micro frontend can be developed and deployed independently, and Web Components play a key role in enabling this independence by providing a consistent way to share UI elements.

---

**Web Components Example** 
While in each front-end framework which supports creating web components, may have it's own functions to work with web components, below is a general way of creating web component in `Javascript`:
```typescript
class UserCard extends HTMLElement {
    private _userId: string;

    static get observedAttributes() {
        return ['user-id'];
    }

    attributeChangedCallback(name: string, oldValue: string, newValue: string) {
        if (name === 'user-id') {
            this._userId = newValue;
            console.log('userId set to:', this._userId);
        }
    }

    set userId(value: string) {
        this._userId = value;
        this.setAttribute('user-id', value);
    }

    get userId(): string {
        return this._userId;
    }
}

customElements.define('user-card', UserCard);

```

In a similar way, we can export any component from a framework that supports conversion to Web Components as a web component and after importing it's javascript on host side, we can use this custom HTML element in HTML template with defined attributes:
```html
<user-card user-id="123"></user-card>
```
And this approach is framework-agnostic, meaning we can export web component(s) from Angular or React frameworks and render them together in separate vue.js application.
This is because web component is a web standard and is not tight to any framework, it can be reused anywhere since it incorporates the whole logic under the hood.

---

**Benefits of using Web Components in MFEs**  
- **Reduced Development Time:** Reusable components mean less code to write and maintain.
- **Improved Code Maintainability:** Encapsulation makes it easier to understand and modify individual components.
- **Increased Team Autonomy:** Teams can work on different parts of the application independently.
- **Technology Agnostic:** Web Components can be used with any framework or no framework at all.
- **Better Scalability:** MFEs built with Web Components can be **scaled more easily** as they are independent and reusable.

---

**Pitfalls with using Web Components in MFEs**  
- **SEO Issues with Shadow DOM:**
Content within the Shadow DOM might not be indexed by search engines, potentially impacting SEO. Workarounds like using slot elements or server-side rendering can mitigate this.
- **Performance Overhead:**
**Excessive use of Shadow DOM** can cause **performance bottlenecks**, especially when polyfills are needed for older browsers.  
Additionally, if core or helper libraries aren't shared across Web Components, the same library may be loaded multiple times on the page, further impacting performance.  
To avoid this, it's important to consider **dependency sharing strategies**, such as those enabled by **Module Federation**.
- **Styling Limitations:**
Global styles don't automatically apply within the Shadow DOM, requiring specific strategies like scoped CSS or custom properties.
- **Lack of Built-in State Management:**
Unlike frameworks, Web Components don't offer built-in state management, requiring developers to implement their own solutions or rely on external libraries.
- **Event Handling Complexity:**
Inter-component communication between Web Components and other frameworks can be more complex, relying on custom events and propagation techniques.
- **Form Handling Issues:**
  Web Components **don't automatically integrate with native form elements**, such as input collection and validation. Additional handling, such as syncing values to hidden inputs or using the `ElementInternals API`, is required to integrate them fully with native forms.

---

#### 🔹 Strategic Design Concept in DDD

---

**Strategic design** in **Domain-Driven Design (DDD)** is the initial phase focused on **understanding** and **structuring** a **complex business domain** before diving into detailed implementation.
- It involves identifying **core business aspects**, dividing the domain into **manageable subdomains**, and establishing **clear boundaries (bounded contexts)** with a **shared language (ubiquitous language)**.
- This approach ensures that the software solution aligns with the **business needs** and effectively **addresses its complexities**.

---

**Key Goals of Strategic Design**  
- **Domain Understanding**   
  Building a shared understanding of the business domain, its core concepts, entities, and relationships among them, among technical and non-technical stakeholders.
- **Bounded Contexts**  
  Dividing the overall domain into smaller, more manageable **bounded contexts**. Each context represents a specific area of the business with its own unique model and language.
- **Ubiquitous Language**   
  Establishing a **common vocabulary** used by everyone involved in the project, including domain experts and developers, to ensure clear communication and reduce ambiguity.
- **Context Mapping**  
  Defining the **relationships between different bounded contexts**, such as **upstream/downstream dependencies**, **shared kernels**, or **anti-corruption layers**, to manage interactions and dependencies between them.

---

**Why is Strategic Design Important?**  
- **Complexity Management**  
  DDD acknowledges that real-world business domains can be highly complex. Strategic design helps **break down this complexity into smaller, more manageable parts**, making the **development process more efficient** and **less error-prone**.
- **Alignment with Business Needs**  
  By focusing on understanding the domain first, strategic design ensures that the **software solution accurately reflects the business requirements and goals**, leading to a **more effective and valuable product**.
- **Maintainability and Scalability**  
  Well-defined bounded contexts and clear relationships between them contribute to a **more maintainable and scalable software architecture**. Changes within one context are less likely to impact other parts of the system.
- **Improved Collaboration**   
  The shared language and clear boundaries established through strategic design foster **better collaboration between domain experts and developers**, leading to **more accurate and efficient software development**.   
  In essence, strategic design in DDD is about answering the question of **"what" needs to be built** before figuring out **"how" to build it**. It's a crucial foundation for building **robust and maintainable software** that truly addresses the needs of the business.

---

**Benefits of Strategic DDD in Front-End Projects**
- **Scalable Team Collaboration**  
  Strategic DDD helps teams define ownership boundaries, enabling multiple front-end teams to work independently and cohesively, especially in large-scale or microfrontend architectures.

- **Modular and Maintainable UI Architecture**  
  By aligning UI modules with business subdomains, teams can better isolate changes, leading to more maintainable and resilient code over time.

- **Better Domain Alignment in UI**  
  When front-end developers share the same language and understanding as domain experts, the resulting UI aligns more closely with business logic and user needs.

- **Fits Shell-Level and Shared Applications**  
  Strategic DDD is particularly valuable in shell-level applications that serve as containers for features from different domains. It ensures structured integration of shared components, routes, and models.

- **Supports Evolving Business Needs**  
  DDD’s emphasis on the core domain makes it easier to adapt the front-end to frequent changes in business rules or priorities, keeping the product relevant and agile.


**Pitfalls of Applying Strategic DDD in Front-End Projects**
- **Overhead for Simple Applications**  
  Strategic DDD introduces complexity that may be unnecessary for small or short-lived applications. If the domain logic is simple, the modeling and context mapping effort may slow down development without significant benefits.

- **Misalignment Without Strong Domain Collaboration**  
  DDD is not just a front-end or technical decision—it requires continuous collaboration with domain experts. Applying strategic design without this alignment can result in disconnected models and over-engineering.

- **Not a One-Team Initiative**  
  Strategic design is most effective when applied across multiple teams or domains. Trying to adopt it in isolation within a single front-end team, without backend or product alignment, may lead to inconsistent architecture and duplicated logic.

- **Learning Curve and Communication Overhead**  
  Establishing bounded contexts and ubiquitous language adds up-front complexity and requires clear documentation and strong communication practices, which may overwhelm smaller teams.

---

### Frontend Architecture Implementations

Using the mechanisms described above, we can create powerful frontend architecture implementations. Below are some examples:

- **Module Federation + Nx Monorepo**  
  This combination enables a **micro-frontend architecture within a monorepo**:
    - The code for MFEs lives alongside the host app in the same Nx monorepo.
    - Each MFE can have its own working rules, boundaries, and owners thanks to Nx's support for modular project organization.
    - Micro-frontends are deployed independently, while the host app loads them at runtime via Module Federation integration within the monorepo.    

- **Web Components + Module Federation + Polyrepo**  
  This combination results in a **framework-agnostic micro-frontend architecture**:
    - Each MFE lives in a separate Git repository and is maintained and deployed independently.
    - Each MFE exposes a custom Web Component and the corresponding JavaScript module using Module Federation.
    - The shell application resides in its own Git repository and hosts MFEs based on the Module Federation configuration.
    - This setup allows runtime loading of micro-frontends, meaning the shell does not require redeployment when a new version of an MFE is released.


### Frontend Architecture Comparison Table
It's important to consider **team size**, **project complexity**, and the **long-term roadmap** when deciding on a frontend architecture.  
Adopt what fits your **current needs** and **scale gradually** as the project evolves.

| Architecture                                | Use Case                                                                                   | Pros                                                                                                                                       | Cons                                                                                                                                                                  |
|--------------------------------------------|--------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Web Components + Module Federation + Polyrepo** | For framework-agnostic micro-frontend (MFE) architectures where MFEs can use different frontend frameworks | - Total independence of MFE maintenance  <br> - Framework agnostic <br> - Libraries can be shared across MFEs                            | - Tree-shaking limitations may affect performance <br> - Higher setup cost (Git + pipeline per MFE) <br> - Requires shared libraries to avoid duplication             |
| **Module Federation + Nx Monorepo**        | When you need isolated MFEs but want to share common code within the same repository       | - Independent MFE deployment <br> - Clear separation of ownership and rules <br> - Easy code sharing <br> - Simplified Git and CI setup    | - Large repo size <br> - Slow Git commands <br> - Possible bugs from shared codebase if boundaries are not respected                                                 |
| **Hybrid (Monorepo + Polyrepo via NPM packages)** | When MFEs use the same tech stack and independent workflows are desired, but shell can be redeployed | - Independent development and deployment of MFEs                                                   | - Not framework agnostic <br> - Shell redeployment needed for every MFE update <br> - Each MFE requires its own setup and pipeline integration                        |
| **Monolith**                               | Best for small projects with a single team maintaining the entire codebase                  | - No overhead for repo and pipeline setup <br> - Easy code sharing                                                                       | - Difficult to scale <br> - Harder to hand off parts to other teams <br> - Risk of maintainability issues as project grows                                            |
| **Web Components (standalone)**            | When a component built in one framework needs to be reused in another framework or vanilla JS project | - Framework-agnostic component reuse <br> - Built, maintained, and deployed individually                                                 | - Shell must update and redeploy when component version changes <br> - Managing inter-component communication can be tricky <br> - Risk of code duplication (Shadow DOM) |



## Resources and References
- ["Design Patterns: Elements of Reusable Object-Oriented Software,"](https://www.amazon.com/Design-Patterns-Elements-Reusable-Object-Oriented/dp/0201633612) book authored by Erich Gamma, Richard Helm, Ralph Johnson, and John Vlissides  
Introduces The Gang of Four (GoF) Design Patterns - set of solutions to common problems we encounter in software design and development.
- [Gang of Four (GOF) Design Patterns](https://www.geeksforgeeks.org/system-design/gang-of-four-gof-design-patterns/)
- [Webpack Module Federation](https://webpack.js.org/concepts/module-federation/)
- [Nx Monorepo](https://nx.dev/getting-started/installation)
- www.angulararchitects.io   
This is the official site of the **Angular Architects** team. It is led by [Manfred Steyer](https://www.angulararchitects.io/en/team/manfred-steyer/), who is a core maintainer of the [Angular Module Federation plugin](https://www.npmjs.com/package/@angular-architects/module-federation), a recognized expert in Angular architecture, and a Google Developer Expert.   
It’s an excellent place to learn and explore **micro-frontend architecture**. Some highly recommended reads include:
  - [Combining Native Federation and Module Federation](https://www.angulararchitects.io/blog/combining-native-federation-and-module-federation/)
  - [Dynamic Module Federation with Angular](https://www.angulararchitects.io/blog/dynamic-module-federation-with-angular/)
  - [Implementing your Strategic Design with Angular and Nx](https://www.angulararchitects.io/blog/sustainable-angular-architectures-2/)