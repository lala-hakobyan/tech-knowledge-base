# React Architecture: Modern React 2025

## Table of Contents
- [Best Practices for Building Scalable, Maintainable and Testable React Code](#best-practices-for-building-scalable-maintainable-and-testable-react-code)
- [React Build Tools and Frameworks](#react-build-tools-and-frameworks)
- [Project Structure and Naming Conventions](#project-structure-and-naming-conventions)
- [Design Patterns](#design-patterns)
- [State Management](#state-management)
- [Form Manipulation](#form-manipulation)
- [Data Fetching and API Manipulation](#data-fetching-and-api-manipulation)
- [Styling](#styling)
- [Linting](#linting)
- [Unit Testing](#unit-testing)
- [Localization & Translation](#localization--translation)
- [Codebase Build and Management Tools](#codebase-build-and-management-tools)
- [High-Quality React GitHub Repositories (2025)](#high-quality-react-github-repositories-2025)
- [Documentation and References](#documentation-and-references)

 
## Best Practices for Building Scalable, Maintainable and Testable React Code
- Use **TypeScript** for strong type checking and better developer experience.
- Split components by responsibility to **keep code modular** and easier to manage.
- Use **consistent and meaningful folder structure** (e.g., feature-based or domain-driven) and follow naming conventions.
- **Optimize rendering** with memoization (`React.memo`, `useMemo`, `useCallback`) where appropriate or use new [React Compiler](./compiler-react.md) to do optimizations automatically.
- Use **lazy loading** of features and resources(images, videos, etc.) to achieve better performance.
- Follow **React design patterns**, since React is an unopinionated library and without patterns, code can become messy.
- Integrate **linting plugins** to enforce [Rules of React](https://react.dev/reference/rules), accessibility rules and consistent code style.
- Include **unit and component testing** to ensure reliability and catch regressions early.
- **Avoid prop drilling** - use React Context or state management libraries (e.g., Zustand, Redux) when passing props through more than two levels.
- **Choose the right tools** for state management, API handling, styling, and forms based on project needs.
- Follow [**Clean Code Principles**](../../architecture/clean-code-principles.md) to improve maintainability and scalability.   
- Consider general [**front-end security attacks**](https://www.geeksforgeeks.org/blogs/top-common-frontend-security-attacks/) and [**performance best practices**](https://www.geeksforgeeks.org/blogs/best-practices-for-enhancing-application-performance/) when building React applications.   

This documentation contains summaries and trade-offs of various tools and architectural patterns for React applications, based on **real learning**, **official documentation**, and **community best practices**.   
You can check the [Frontend Architecture](./../architecture-frontend.md) document to dive deep into core architectural concepts and the decision-making process behind choosing them.

## React Build Tools and Frameworks
There are several ways to build a project with React:

### [Vite Build Tool](https://vite.dev/guide/)
**Vite** is a build tool that aims to provide a faster and leaner development experience for modern web projects. It consists of two major parts:
- **A dev server**  
Provides rich feature enhancements over [native ES modules](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Modules), for example extremely fast [Hot Module Replacement (HMR)](https://vite.dev/guide/features#hot-module-replacement).
- **A build command**    
Bundles your code with [Rollup](https://rollupjs.org/), pre-configured to output highly optimized static assets for production.

### [Next.js Framework](https://nextjs.org/docs)
**Next.js** is a React framework for building full-stack web applications. You use React Components to build user interfaces, and Next.js for additional features and optimizations.
Below are some useful features offered by Next.js:
- Automatically configures lower-level tools like **bundlers** and **compilers**.
- **React Server Components(RSC)**
- **SSR ( Server Side Rendering )** and **Hydration** of Client Side Components rendered on server side.
- **Partial hydration** = only hydrate what’s needed, possible only with server components which use client components.
- **App Router**(The newer router that supports React Server Components) and **Page Router**(still supported and maintained)

### [Remix Framework](https://remix.run/docs/en/main/start/quickstart)
**Remix** is a full stack web framework that lets you focus on the user interface and work back through web standards to deliver a fast, slick, and resilient user experience.
Below are some useful features offered by Remix:
- **Server-side rendering (SSR)** 
- **Efficient data loading strategies** to provide **faster initial page loads** and **smoother navigation**. 
- **Nested routing** 
- **Built-in error handling**, making it easier to manage complex applications and handle errors gracefully.

### [Hono Framework](https://hono.dev/docs/)
**Hono** is a small, simple, and ultrafast web framework built on Web Standards. It works on any JavaScript runtime.
Below are key features:
- **Ultrafast**   
The router `RegExpRouter` is really fast. Not using linear loops.
- **Lightweight**   
The hono/tiny preset is under 14kB. Hono has zero dependencies and uses only the `Web Standards`.
- **Multi-runtime**   
Works on `Cloudflare Workers`, `Fastly Compute`, `Deno`, `Bun`, `AWS Lambda`, or `Node.js`. The same code runs on all platforms.
- **Batteries Included** 
Hono has built-in middleware, custom middleware, third-party middleware, and helpers. So batteries included.
- **Delightful DX**
Very well-structured APIs with excellent TypeScript support - all types are built in.

### React-Compatible Tools: Ecosystem & Usage Overview (2025)

| Tool                         | Init Command                                  | Status              | Popularity        | When to Use                                                  | Notes                                                                            |
|------------------------------|-----------------------------------------------|---------------------|-------------------|--------------------------------------------------------------|----------------------------------------------------------------------------------|
| [**Vite**](https://vite.dev/guide/)              | `npm create vite@latest`                      | Stable & mature     | Very popular      | Small to medium apps, custom setups, fast dev environments   | Lightning-fast HMR, opinionated, needs routing/SSR added manually                |
| [**Create React App**](https://create-react-app.dev/docs/getting-started/)  | `npx create-react-app my-app`                 | Deprecated          | -                 | -                                                            | Once was the officially supported way to create single-page React applications.  |
| [**Next.js**](https://nextjs.org/docs)           | `npx create-next-app@latest`                  | Enterprise-ready    | Extremely popular | Large-scale apps, SSR, SEO, hybrid rendering                 | Official React recommendation, Server Components, Routing, API routes included   |
| [**Remix**](https://remix.run/docs/en/main/start/quickstart)             | `npx create-remix@latest`                     | Actively maintained | Moderate, growing | Apps with deep routing & data loading (e.g. forms, actions)  | Built on web fundamentals, owned by Shopify, smaller but loyal community         |
| [**Hono**](https://hono.dev/docs/)              | `npm create hono@latest`                      | New & fast-growing  | Rising rapidly    | Lightweight APIs or edge-native apps with React or JSX       | Tiny, optimized for edge/serverless, integrates with React manually              |


## Project Structure and Naming Conventions

### Folder Structure
While React is a non-opinionated library and does not enforce a specific project structure, the community has developed widely accepted conventions to support scalability and maintainability.   
A recommended folder structure for modern React projects looks like this:

```
src/  
├── app/                      # App entry, layout, routes, global providers  
│   ├── App.tsx  
│   └── routes.tsx  
│
├── components/               # Reusable UI components (buttons, cards, etc.)  
│   ├── Button/  
│   │   ├── Button.tsx  
│   │   ├── Button.test.tsx  
│   │   └── index.ts  
│   └── ...
│
├── features/                 # Feature-based folders (modular business logic)
│   ├── auth/  
│   │   ├── components/  
│   │   ├── hooks/  
│   │   ├── services/  
│   │   └── authSlice.ts  
│   └── user/
│       ├── components/
│       ├── hooks/
│       ├── userPage.tsx
│       ├── userService.ts      # Feature-based local logic
│       └── userSlice.ts 
│
├── hooks/                     # Shared custom hooks across app  
│   └── useDebounce.ts  
│
├── layout/                   # App shell layout (header, footer, etc.)  
│   ├── Header.tsx  
│   ├── Footer.tsx  
│   └── MainLayout.tsx  
│
├── lib/                      # External helpers (e.g., axios instance, utils)
│   ├── apiClient.ts  
│   └── dateUtils.ts  
│
├── store/                     # Redux or Zustand store setup or global context(if used)
│   ├── authStore.ts           # Zustand or Redux logic
│   ├── themeContext.tsx       # Global Context
│   ├── globalTypes.ts
│   └── index.ts               # Optional: combine exports
│
├── api/
│   ├── user.ts               #shared GET/POST logic
│   └── auth.ts
│
├── services/
│   └── userService.ts        #shared GET/POST logic
│         
├── types/                  # Global TypeScript types
│   └── index.d.ts
│
├── styles/                 # Global styles (CSS/SCSS/Tailwind config)
│   ├── globals.css
│   └── theme.ts
│
├── assets/                 # Static assets (images, icons, fonts)
│   ├── logo.svg
│   └── ...
│
├── index.tsx               # ReactDOM.render / createRoot
└── main.tsx                # Entry point with global providers
  ```

### File Naming Conventions
[Official documentation](https://react.dev/learn/reusing-logic-with-custom-hooks) suggests the following naming conventions for React components and hooks:
- React component names must follow `PascalCase` - start with a capital letter, like `StatusBar` and `SaveButton`. React component file names should follow the same pattern: `StatusBar.jsx`, `SaveButton.jsx`.
- Hook names must follow `CamelCase` - start with use followed by a capital letter, like `useState` (built-in) or `useOnlineStatus`. React hook file names should follow the same pattern accordingly: `useOnlineStatus.js`
- The other files, like utilities, services could align with hook naming pattern to keep consistency: `CamelCase`

### Summary Table for File and Folder Naming Conventions

| Item                  | Naming Style | Example                        | Notes                                                                 |
|-----------------------|--------------|--------------------------------|-----------------------------------------------------------------------|
| **Top-level folders** | `kebab-case` | `components/`, `features/`     | Standard for directories; avoids case-sensitive issues on some OS     |
| **Component folders** | `PascalCase` | `Button/`, `UserCard/`         | Folders that directly represent components; matches their names       |
| **Component files**   | `PascalCase` | `Button.tsx`, `UserCard.tsx`   | Same as the exported component: `export const UserCard = ...`         |
| **Other files**       | `camelCase`  | `useAuth.ts`, `apiClient.ts`   | For hooks, utils, APIs, and services; follows JS conventions          |
| **Test files**        | match component | `Button.test.tsx`           | Lives next to the component it tests for discoverability              |
| **Styles/CSS modules**| match component | `Button.module.css`        | Same name, same folder as the component it styles                     |

## Design Patterns
### [Layout Components (Layout Design Pattern)](https://github.com/LinkedInLearning/react-design-patterns-6037122/tree/06_07e/layout-components/src)
**Layout components** are React components that deal primarily with arranging other components on the page.     
Layout Component Examples:
- Split Screens
- Lists and Items
- Modals   

The main idea of the layout components is the following: **our components shouldn’t need to know where they are being displayed.**

### [Container Components (Container - Presentation Pattern)](https://github.com/LinkedInLearning/react-design-patterns-6037122/tree/06_07e/container-components/src)
- **Container components** take care of loading and managing data for their child components.
- Container components host child components which are called **presentation(dumb)** components. These components are not responsible for fetching data from the server.   
Instead, they should receive data via props from container components and focus solely on displaying it.

### [Controlled vs Uncontrolled Components Pattern](https://github.com/LinkedInLearning/react-design-patterns-6037122/tree/06_07e/controlled-uncontrolled/src)
- **What are Controlled Components?**   
These are components that do not keep track of their own state - all states pass in as props.   
In case of form, [Controlled Form Components](#controlled-form-components) are the ones that keep the form data in the React component state. React controls the input’s value via `useState`.

  ```jsx
  // ControlledModal.jsx
  export const ControlledModal = ({ isOpen, onClose, children }) => {
    if (!isOpen) return null;
  
    return (
      <div className="modal">
        <button onClick={onClose}>Close</button>
        {children}
      </div>
    );
  };
  ```
  ```jsx
  // App.jsx
  function App() {
    const [showModal, setShowModal] = React.useState(false);
  
    return (
      <>
        <button onClick={() => setShowModal(true)}>Open Modal</button>
        <ControlledModal isOpen={showModal} onClose={() => setShowModal(false)}>
          <p>This is a controlled modal</p>
        </ControlledModal>
      </>
    );
  }
  ```
- **What are Uncontrolled Components?**      
These are components that keep track of their own states and release data only when some event occurs (for example, exposing the `isOpen` state via `onToggle` callback prop).   
In case of form, [Uncontrolled Form Components](#uncontrolled-form-components--refs) are those where the form data is handled by the `DOM` itself, rather than being managed by `React state`.

  ```jsx
  // UncontrolledModal.js
  export const UncontrolledModal = ({ children }) => {
    const [isOpen, setIsOpen] = React.useState(false);
  
    return (
      <>
        <button onClick={() => setIsOpen(true)}>Open Modal</button>
        {isOpen && (
          <div className="modal">
            <button onClick={() => setIsOpen(false)}>Close</button>
            {children}
          </div>
        )}
      </>
    );
  };
  ```
  ```jsx
  // App.jsx
  function App() {
    const [showModal, setShowModal] = useState(false);
  
    return (
      <>
        <button onClick={() => setShowModal(true)}>Open Modal</button>
        <ControlledModal isOpen={showModal} onClose={() => setShowModal(false)}>
          <p>This is a controlled modal</p>
        </ControlledModal>
      </>
    );
  }
  ```
- **Controlled Components or Uncontrolled Components. Which one we prefer?**   
  We generally prefer controlled components. The reasons are:
  - It makes our components more reusable
  - It makes it easier to test since we can set up a component with an exact state that we want instead of having to create the component manually.

### [Higher Order Components (HOC) Pattern](https://github.com/LinkedInLearning/react-design-patterns-6037122/tree/06_07e/higher-order-components/src)
- **Higher order components** are basically components that instead of returning JSX, they return another component.

  ```
  MyComponent -----> <h1>I'm JSX!</h1>
  HOC -----> SomeComponent -----> <h1>I'm JSX!</h1>
  ```
- **Higher level components** are just  functions that take components as arguments and new return components. They could be interpreted as sort of component factories - functions that you can call in order to create components.
- **HOCs** are used for:
  - Sharing complex behaviour between multiple components (much like with container components)
  - Adding extra functionality to existing components without modifying component itself.
  
### [Custom Hooks](https://github.com/LinkedInLearning/react-design-patterns-6037122/tree/06_07e/custom-hooks/src)
- **Custom Hooks** are special hooks that we define ourselves, and that usually combine the functionality of one or more existing React Hooks like `useState` or `useEffect`.
- **Custom hooks** have to start with a word `use` and it has to do with the work that hooks do behind the scenes.
- **Custom hooks** are used for sharing complex behaviour between multiple components, much like with higher-order components (HOCs) and container components.
- For example, if we want to load products from different components, instead of putting the same logic in each component, we could just put that logic into a `Custom Hook` and use the hook in each of our components.

### [Functional Programming](https://github.com/LinkedInLearning/react-design-patterns-6037122/tree/06_07e/functional-react/src)
Functional programming is a coding paradigm that focuses on:
- **Minimizing mutations** and **state changes**
- Keeping functions **pure** (independent of external state)
- Treating functions as **first-class citizens**, meaning they can be passed around and returned just like values such as strings or numbers

React encourages this functional style by design - unlike Angular, which leans more toward an object-oriented programming (OOP) model using classes, services, and decorators.

In React, functional programming is reflected in patterns like:
- **Controlled components** – state is passed and controlled via props
- **Function components** – components written as pure functions
- **Higher-order components (HOC)** – functions that take components as arguments and return new components
- **Recursive components** – components that render themselves conditionally
- **Partially applied components** – using closures to pre-apply props
- **Component composition** – combining small, focused components to build complex UIs

React’s functional nature leads to better **modularity**, **reusability**, and **testability** — key ingredients for scalable, maintainable apps.

#### Recursive Components
**Recursion** is a programming technique where a function calls itself to solve a problem by breaking it down into smaller, similar sub-problems.  
Key Concepts to write a recursive function:
- There should be a **base case** (stopping point) where the function returns or doesn’t display itself - otherwise, we would run into a stack overflow error due to an infinite loop.
- The function should also include a **recursive step**, where it calls itself with a smaller or simpler input, gradually working toward the base case.

#### Component Composition
Composition refers to when you have multiple pieces of functionality that are fairly small and self-contained but can also be combined to create something more complicated.
For example, separating `Card` component into `CardHeader`, `CardBody` and `CardFooter` components:
```jsx
<Card>
   <CardHeader title="Card Header" />
   <CardBody>
      <p>Just a card context text going here</p>
   </CardBody>
   <CardFooter title="Copyright Lala" />
</Card>
```

#### Partial Application
**Partial application** is when we take a certain number of arguments in a function and fix them to specific values. And that helps to create a more specific version of a more generic function.

### Business Logic Encapsulation + Dependency Injection 
This is a very useful and interesting pattern combination to use in React. This pattern allows to create testable, maintainable and scalable code.
- If there is any specific business logic, we separate it from React and UI. We can place it in domain folder following **DDD(Domain Driven Architecture)** patten.
This is a clear example of **business logic encapsulation(separation)**.   
Example:
  ```js
  // domain/Cart.js
  export class Cart {
    constructor(items = []) {
      this.items = items;
    }
    
    addItem(item) {}
    
    removeItem(index) {}
    
    static empty() {
      return new Cart();
    }
  }
  ```
- Next, we create a `CartContext` in React to globally access `Cart` state. This is a clear demonstration of **DI(Dependency Injection)** pattern which a design pattern that enables a component to receive its dependencies from external sources rather than creating them internally.
  
  ```jsx
  // src/store/context/CartContext.js
  const CartContext = createContext(null);
  
  export const CartProvider = ({ children }) => {
    const [cart, setCart] = useState(Cart.empty());
  
    return (
      <CartContext.Provider value={{ cart, setCart }}>
        {children}
      </CartContext.Provider>
    );
  };
  
  export const useCart = () => {
    const context = useContext(CartContext);
    // Error handling
    return context;
  };
  ```
- Finally, we access `Cart` component from any component. This way component doesn't know anything about internal business logic of the cart and doesn't initialize it. Instead, component accesses `Cart` state globally and can modify it without knowing internal implementation details.
  ```jsx
  function App() {
    return (
      <CartProvider>
        <CartSummary />
      </CartProvider>
    );
  }
  ```
  ```jsx
  // src/components/cart/CartSummary.js
  export const CartSummary = () => {
    const { cart, setCart } = useCart();
  
    const handleAdd = () => {
      const newItem = { id: Date.now(), name: 'Item ' + cart.items.length };
      const updatedCart = cart.addItem(newItem); // Immutable update
      setCart(updatedCart);
    };
  
    return (
      <div>
        <h3>Cart Summary</h3>
        <ul>
          {cart.items.map((item, i) => (
             <li key={item.id}>{item.name}</li>
          ))}
        </ul>
        <button onClick={handleAdd}>Add Item</button>
      </div>
    );
  };
  ```
**Summary of Related Concepts / Patterns**
 
  | Pattern/Term                       | 	Description                                                                   |
  |------------------------------------|--------------------------------------------------------------------------------|
  | **Business Logic Encapsulation**   | Moves logic out of React components into dedicated domain classes or services. | 
  | **Domain Modeling / Domain Layer** | Represents business entities (like `Cart`) as rich, behavior-driven objects.   |
  | **State Holder Pattern**           | The domain object (`Cart`) encapsulates and manages its own state internally.  | 
  | **Factory Method**                 | `Cart.empty()` is a static method that abstracts how an empty cart is created. | 
  | **Dependency Injection**           | The `Cart` instance is injected via context, not created within the component. |
  | **Inversion of Control (IoC)**     | The component depends on an external context to provide dependencies.          |

### Summary of Design Patterns
| Pattern                                | Popularity         | Notes                                                                                |
|----------------------------------------|--------------------|--------------------------------------------------------------------------------------|
| Layout Components                      | ✅ Common          | Used for composing flexible layouts (SplitView, SidebarLayout, etc.)                 |
| Container-Presentational Pattern       | ✅ Classic         | Still relevant, though custom hooks now often replace containers                     |
| Controlled vs Uncontrolled Components  | ✅ Core Concept    | Controlled preferred for testability; uncontrolled used for simpler or native forms  |
| Higher Order Components (HOC)          | ⚠️ Declining       | Replaced by hooks in most new code; still seen in some libraries (e.g. `connect`)    |
| Custom Hooks                           | ✅ Very Popular    | Go-to pattern for logic reuse in modern React                                        |
| Functional Programming Patterns        | ✅ Core Design     | Encouraged by React team; clean, reusable, and testable code                         |
| Recursive Components                   | ⚠️ Niche           | Used when rendering nested tree-like structures (e.g. menus, comments, folders)      |
| Component Composition                  | ✅ Fundamental     | The key to React’s philosophy - "Composition over Inheritance"                       |
| Partial Application (Components)       | ⚠️ Advanced        | Useful for pre-configuring component props in complex UIs                            |
| Business Logic Encapsulation           | ✅ Best Practice   | Critical for separating concerns and enabling testing and scalability                |
| Dependency Injection (via Context)     | ✅ Common          | Widely used to inject services or data (e.g., theme, auth, cart state)               |
| Factory Methods                        | ⚠️ Advanced        | Seen in domain modeling or service instantiation scenarios                           |
| Inversion of Control (IoC)             | ⚠️ Advanced        | Tied to DI; aligns with modern scalable architecture practices                       |


## State Management
### [React Redux Library](https://react-redux.js.org/introduction/getting-started)
The official React UI bindings layer for [Redux](https://redux.js.org/tutorials/essentials/part-1-overview-concepts). It lets your React components read data from a Redux store, and dispatch actions to the store to update state.

### [Zustand Library](https://zustand.docs.pmnd.rs/getting-started/introduction)
A lightweight, fast, and scalable state management library with minimal boilerplate.
- **Zustand** has a comfortable API based on hooks. 
- It isn't boilerplate or opinionated, but has enough convention to be explicit and **flux-like**.
 
### [Mobx](https://mobx.js.org/README.html)
**A signal based, battle-tested** library that makes state management simple and scalable by transparently applying functional reactive programming.   
MobX uses `makeAutoObservable` to create reactive state, and `observer`(or `useObserver`) to make React components automatically re-render when observable data changes.
- `makeAutoObservable(obj)`
  - This is a `MobX` function. 
  - It turns a plain object (or class) into something `MobX` can track reactively. 
  - Automatically marks properties as observable and functions as actions.
  ```js
    import { makeAutoObservable } from "mobx";

    class TodoStore {
      todos = [];
    
      constructor() {
        makeAutoObservable(this);
      }
    
      addTodo(todo) {
        this.todos.push(todo);
      }
    }
  ```
- `observer(Component)`
  - A `higher-order component(HOC)` from m`obx-react-lite` or `mobx-react`. 
  - It wraps your React component to make it automatically re-render when any observed `MobX` state inside changes.
  ```jsx
    import { observer } from 'mobx-react-lite';

    const TodoList = observer(({ store }) => (
      <ul>
        {store.todos.map(todo => <li key={todo}>{todo}</li>)}
      </ul>
    ));
  ```
- `useObserver(() => JSX)`
  - A React hook alternative to observer. 
  - Same purpose: reactively track observables and trigger re-renders. 
  - Less commonly used than observer, but more flexible in some dynamic render cases.
  ```jsx
    import { useObserver } from 'mobx-react-lite';

    const TodoList = ({ store }) =>
      useObserver(() => (
        <ul>
            {store.todos.map(todo => <li key={todo}>{todo}</li>)}
        </ul>
    ));
  ```
**Note:** In modern usage with functional components, `observer` is generally preferred over `useObserver`.

### [Recoil](https://recoiljs.org/docs/introduction/core-concepts) 
**Recoil** is a state management library created by **Facebook for React**. It introduces concepts like **Atoms** and **Selectors** to manage and derive state in a simple and scalable way.
- It's aimed at **solving the complexity of shared state** in React apps, while feeling **as close as possible to React itself**.
- It is React-specific state management with `atoms` and `selectors`
- Feels like a natural extension of `useState` and `useContext`

### Comparison of Different State Management Libraries 

| Library                                                                    | Command                                     | Popularity | Best For                                                  | Pros                                                                   | Cons                                                             |
|----------------------------------------------------------------------------|---------------------------------------------|------------|-----------------------------------------------------------|------------------------------------------------------------------------|------------------------------------------------------------------|
| [**Zustand**](https://zustand.docs.pmnd.rs/getting-started/introduction)   | `npm install zustand`                       | Rising     | Lightweight apps, fast prototypes, modern stacks          | Minimal boilerplate, tiny bundle, great dev experience, React-friendly | Less built-in structure, no middleware out of the box            |
| [**Redux**](https://react-redux.js.org/introduction/getting-started)       | `npm install @reduxjs/toolkit react-redux`  | Mature     | Large-scale enterprise apps, legacy codebases             | Ecosystem rich, devtools, clear architecture, time-travel debugging    | Verbose, requires boilerplate (though Redux Toolkit helps a lot) |
| [**MobX**](https://mobx.js.org/README.html)                                | `npm install mobx mobx-react-lite`          | Balanced   | Complex UI apps, reactive data flows                      | Fine-grained reactivity, intuitive, OOP-style                          | Too implicit, harder to debug at scale                           |
| [**Recoil**](https://recoiljs.org/docs/introduction/core-concepts)         | `npm install recoil`                        | Niche      | React-first apps needing derived state & Suspense support | Hooks-based, derived state with selectors, concurrent-mode friendly    | Less community adoption, limited ecosystem                       |

## Form Manipulation

### Controlled and Uncontrolled Form Components 
#### Controlled Form Components
**Controlled form components** keep the form data in the React component state. React controls the input’s value via `useState`.
```jsx
export default function ControlledForm() {
  const [name, setName] = useState('');

  const handleSubmit = (e) => {
    e.preventDefault();
    console.log("Submitted Name:", name);
  };

  return (
    <form onSubmit={handleSubmit}>
      <label>
        Name:
        <input 
          type="text" 
          value={name} 
          onChange={(e) => setName(e.target.value)} 
        />
      </label>
      <button type="submit">Submit</button>
    </form>
  );
}
```
#### Uncontrolled Form Components + Refs
**Uncontrolled form component** in React are those where the form data is handled by the DOM (Document Object Model) itself, rather than being managed by React state.
```jsx
export default function UncontrolledForm() {
  const nameRef = useRef(null);

  const handleSubmit = (e) => {
    e.preventDefault();
    console.log("Submitted Name:", nameRef.current?.value);
  };

  return (
    <form onSubmit={handleSubmit}>
      <label>
        Name:
        <input 
          type="text" 
          ref={nameRef} 
        />
      </label>
      <button type="submit">Submit</button>
    </form>
  );
}
```
#### Controlled vs Uncontrolled. Which one to choose?
Controlled form is better approach in most cases. Why to choose **controlled form**?:
- `value` is bound to React state
- It is good for **validation**, **conditional rendering**, and **predictable behavior**.

Choose **uncontrolled form** when: 
- No need to sync `value` to state
- Useful for **quick/simple forms** or when integrating with **non-React code** (e.g., third-party libs)

### [React Hook Form](https://react-hook-form.com/get-started)
**React Hook Form** is a lightweight and performant library for building and managing forms in React applications. It leverages React Hooks to simplify form handling, state management, validation, and submission, aiming to reduce boilerplate code and improve performance compared to traditional form handling methods in React.

### [Vest](https://vestjs.dev/docs/get_started)
**Vest** is a powerful and easy-to-use JavaScript validation framework that allows you to write and run validations for your code. It is designed to handle complex validation scenarios while still being simple to use.
Below are some useful concepts and features of Vest:
- **Syntax very similar to a unit testing suite** in `Jest` or `Mocha`
- **Separation of Concerns**
- **Asynchronous Validation**
- Allows **Shared Validation between Client and Server**. 
Server can specify validation rules, client can retrieve them when receiving data from API response, deserialize and use for client side validation.
- **Warning State** different from Error State 
- **Related Fields Validation**


## Data Fetching and API Manipulation
### [Drizzle](https://www.linkedin.com/advice/3/how-can-you-effectively-use-drizzle-manage-state-your#:~:text=Drizzle%20is%20a%20collection%20of,transactions%2C%20and%20generating%20contract%20events.)
  - **Drizzle** is a **collection of libraries and tools** that simplify the development of dApps using React. 
  - **Drizzle** helps you connect your React components to your **smart contracts**, and **automatically updates the state when there are changes** in the blockchain or the user actions. 
  - **Drizzle** also provides some useful features, such as **caching contract data**, **handling transactions**, and **generating contract events**.
### [React Query (TanStack Query)](https://tanstack.com/query/latest/docs/framework/react/overview) 
  A primarily a **server state management library**, focused on handling the asynchronous lifecycle of **fetching**, **caching**, **updating**, and **syncing** remote **API data**.
### [React Suspense](https://react.dev/reference/react/Suspense)   
  A built-in feature in React that allows components to **wait** for something before rendering.

## Styling
### Tailwind CSS
**Tailwind CSS** is an **atomic** (utility-first) CSS framework, which differs from traditional component-based styling approaches like Bootstrap.
Instead of pre-designed components, **Tailwind** provides **low-level utility classes** for individual CSS rules (e.g., `p-4`, `text-center`, `bg-blue-500`), allowing developers to compose complex styles directly in the `HTML` or `JSX`. 

**Pros:**    
- Highly flexible
- Reduces style duplication
- Enables smaller final CSS bundles through tree-shaking (PurgeCSS)

**Cons:**
- `HTML/JSX` markup can become verbose
- Requires familiarity with utility class naming conventions

**How to Install Tailwind CSS?**
- [Install Using Vite](https://tailwindcss.com/docs/installation/using-vite)
- [Install with Next.js](https://tailwindcss.com/docs/installation/framework-guides/nextjs)

**Examples of famous Tailwind CSS combinations:**   
- [**shadcn/ui**](https://ui.shadcn.com/) (`Tailwind` + `Radix UI`)  
  Fully functional, ready-to-use component library built with Tailwind `CSS + Typescript`. It is the most modern, flexible, Tailwind-powered library which is used in production.
- **DaisyUI**  
  Tailwind plugin that provides styled components and themes. Mostly CSS classes only, minimal JS.
  - [DaisyUI Installation](https://www.npmjs.com/package/react-daisyui)
  - [DaisyUI Styleguide](https://react.daisyui.com/?path=/docs/welcome--docs)
- [**Tailwind UI**](https://tailwindcss.com/plus/ui-blocks/documentation)  
  Official Tailwind component library with beautiful styled components. No JS included, you add your own behavior.

### [Chakra UI](https://chakra-ui.com/docs/get-started/installation)
Functional component library and design system famous for easy to use, **responsive props**, accessible by default.

### [Material UI(MUI)](https://mui.com/material-ui/getting-started/installation/)
Functional component library for enterprise-level apps, robust ecosystems.

### [Mantine](https://mantine.dev/getting-started/)
React component library that provides fully **functional**, **accessible**, and **customizable** components built with `JavaScript/TypeScript`. It is developer-friendly, modern, fast-growing.

### [Bulma](https://couds.github.io/react-bulma-components/?path=/story/welcome--page)
**CSS-only** component styling - pure CSS, no JS.

### CSS-in-JS
**CSS-in-JS** is a technique for writing CSS styles directly within JavaScript or TypeScript code, like directly in a React component.  
```jsx
import React from 'react';
import styled from 'styled-components';

const StyledButton = styled.button`
  background-color: ${props => (props.primary ? 'blue' : 'gray')};
  color: white;
  padding: 10px 20px;
  ...
`;

function MyComponent() {
  return (
    <StyledButton primary>Click Me</StyledButton>
  );
}

export default MyComponent;
```
- [**Styled Components**](https://styled-components.com/docs/basics#installation)     
  Most widely known and adopted, has large ecosystem and is great for React.      
- [**Emotion**](https://www.npmjs.com/package/@emotion/react)   
  - Similar to Styled Components, used in frameworks like **Chakra UI**.  
  - Styles are generated and injected dynamically at runtime - i.e., when your React components mount, the JS generates CSS rules on the fly and injects them into the document’s `<style>` tags.
  This adds runtime overhead every time components mount or update.
- [**Stitches**](https://stitches.dev/docs/installation)  
  Very **fast**, **modern API**, **compile-time CSS**, provides great developer experience.
- [**Vanilla Extract**](https://vanilla-extract.style/documentation/getting-started)     
  **Type-safe**, **build-time CSS generation**, **growing** in TypeScript-heavy codebases.

#### CSS-in-JS Tools Libraries Comparison

| Library                                                                            | Pros                                                                                                       | Cons                                                                     | Community Adoption | Status              |
|------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------|--------------------|---------------------|
| [**Styled Components**](https://styled-components.com/docs/basics#installation)    | Very popular and widely used, familiar syntax, great ecosystem & docs                                      | Runtime style injection, can increase bundle size and mount-time latency | Very high          | Actively maintained |
| [**Emotion**](https://www.npmjs.com/package/@emotion/react)                        | Lightweight, flexible (supports both string and object styles), good TypeScript support, used by Chakra UI | Runtime style injection, can become messy in large projects              | High               | Actively maintained |
| [**Stitches**](https://stitches.dev/docs/installation)                             | Compile-time CSS (no runtime injection), great TS support, fast & modern API                               | Smaller ecosystem, slight learning curve for variants/theming            | Growing            | Actively maintained |
| [**Vanilla Extract**](https://vanilla-extract.style/documentation/getting-started) | Fully type-safe, build-time CSS generation, excellent for monorepos                                        | Requires custom build setup, not as beginner-friendly                    | Niche/TS-heavy     | Actively maintained |


## Linting
### [React Official Editor Setup Documentation](https://react.dev/learn/editor-setup#linting)
### [Rules of React](https://react.dev/reference/rules)
### Eslint Plugins
  - [eslint-plugin-react-hooks](https://www.npmjs.com/package/eslint-plugin-react-hooks)   
  Enforces React Hook rules; built and maintained by React team.
  - [eslint-plugin-react](https://www.npmjs.com/package/eslint-plugin-react)   
    Provides React-specific linting rules; built and maintained by React team.
  - [eslint-plugin-import](https://www.npmjs.com/package/eslint-plugin-import)   
    Intends to support linting of ES2015+ (ES6+) import/export syntax, and prevent issues with misspelling of file paths and import names.
  - [eslint-plugin-jsx-a11y](https://www.npmjs.com/package/eslint-plugin-jsx-a11y)   
    Enforces accessibility rules of JSX; built and maintained by community.
  - [eslint-config-react-app](https://www.npmjs.com/package/eslint-config-react-app)   
    This package includes the shareable ESLint configuration used by Create React App. While Create React App is officially deprecated, this package seems still maintained and relevant in React community.
    It includes a bunch of packages described above: `eslint-plugin-react-hooks`, `eslint-plugin-react`, `eslint-plugin-import`, `eslint-plugin-jsx-a11y` etc.

## Unit Testing
### [Jest](https://jestjs.io/docs/tutorial-react)
**Jest** is a JavaScript testing framework developed by Meta and is commonly used for testing React applications.
### [Vitest](https://vitest.dev/guide/)
**Vitest** is a next generation testing framework powered by Vite.
### [React Testing Library](https://testing-library.com/docs/react-testing-library/intro/)
**React Testing Library** builds on top of DOM Testing Library by adding APIs for working with React components.


## Localization & Translation
| Tool                                                             | Description                                                             |
|------------------------------------------------------------------| ----------------------------------------------------------------------- |
| [**`react-i18next`**](https://react.i18next.com/getting-started) | Most popular, based on i18next, supports dynamic loading, pluralization |
| [**`react-intl`**](https://www.npmjs.com/package/react-intl)     | Part of FormatJS, supports ICU message syntax                           |
| [**`next-i18next`**](https://www.npmjs.com/package/next-i18next) | Next.js integration with i18next                                        |
| [**`Lingui`**](https://lingui.dev/installation)                  | TypeScript-friendly, great for smaller projects                         |

## Codebase Build and Management Tools
### [Nx](https://nx.dev/getting-started/intro#what-is-nx)   
A powerful, open source, technology-agnostic build platform designed to efficiently manage codebases of any scale.
### [Turborepo](https://turborepo.com/docs)
A high-performance build system for `JavaScript` and `TypeScript` codebases. It is designed for scaling monorepos and also makes workflows in [single-package workspaces](https://turborepo.com/docs/guides/single-package-workspaces) faster, too.
### [Vercel](https://vercel.com/solutions/react)
Vercel is a popular platform for deploying and hosting React applications and many other types of web projects.

## High-Quality React GitHub Repositories (2025)

### Official & Meta Repositories

| Name             | GitHub URL                                              | Description                        |
|------------------|---------------------------------------------------------|------------------------------------|
| **React**        | [facebook/react](https://github.com/facebook/react)     | **Core React** library by **Meta** |
| **React Native** | [facebook/react-native](https://github.com/facebook/react-native) | Cross-platform React for mobile    |

### Real-World Architecture & Practices

| Name                          | GitHub URL                                                                                                            | Description                                                             |
|-------------------------------|-----------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------|
| **Next.js**                   | [vercel/next.js](https://github.com/vercel/next.js)                                                                   | Fullstack React framework with **SSR**, **routing**, and **API routes** |
| **Remix Examples**            | [remix-run/remix](https://github.com/remix-run/examples)                                                              | Example apps showing **advanced routing** and **data loading**          |
| **Tremor**                    | [tremorlabs/tremor](https://github.com/tremorlabs/tremor)                                                             | Beautiful **dashboard** components with **Tailwind** and React          |
| **Bulletproof React**         | [alan2207/bulletproof-react](https://github.com/alan2207/bulletproof-react)                                           | **Scalable architecture** and best practices                            |
| **RealWorld React Redux App** | [gothinkster/react-redux-realworld-example-app](https://github.com/gothinkster/react-redux-realworld-example-app)     | Medium.com clone – full-stack app with **modern Redux** and **routing** |
| **React Admin**               | [marmelab/react-admin](https://github.com/marmelab/react-admin)                                                       | Complex **admin dashboard** with advanced data flow                     |

### UI & Component Libraries

| Name          | GitHub URL                                                   | Description                                                 |
|---------------|--------------------------------------------------------------|-------------------------------------------------------------|
| **Radix UI**  | [radix-ui/primitives](https://github.com/radix-ui/primitives)| Low-level accessible **component primitives**               |
| **ShadCN UI** | [shadcn/ui](https://github.com/shadcn-ui/ui)                 | UI system with **TailwindCSS** and modern DX                |
| **Chakra UI** | [chakra-ui/chakra-ui](https://github.com/chakra-ui/chakra-ui)| Popular UI framework with **accessibility** and **theming** |

### Cool Community Projects

| Name                              | GitHub URL                                                                             | Description                                                                 |
|-----------------------------------|----------------------------------------------------------------------------------------|-----------------------------------------------------------------------------|
| **React E-Commerce**              | [smakosh/react-ecommerce](https://github.com/smakosh/react-ecommerce)                  | Simple yet full-featured e-commerce store built with React + Stripe         |
| **TinyBase**                      | [tinyplex/tinybase](https://github.com/tinyplex/tinybase)                              | Experimental reactive state engine using React                              |
| **React Microfrontend Example**   | [imatiqul/micro-frontend-react](https://github.com/imatiqul/micro-frontend-react)      | React Microfrontend Example with Module Federation                              |

### Educational Projects

| Name                      | GitHub URL                                                                                   | Description                                                                                                                                           |
|---------------------------|----------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------|
| **React Design Patterns** | [LinkedInLearning/react-design-patterns](https://github.com/LinkedInLearning/react-design-patterns-6037122/tree/06_07e) | React: Design Patterns by [Shaun Wassell](https://www.linkedin.com/in/shaun-wassell/?trk=lil_instructor), Linkedin learning  |


## Documentation and References
### React Build Tools and Frameworks
**Build your Web Framework from Scratch** - Presentation by [Yusuke Wada](https://github.com/yusukebe) at React Summit, June 2025 
### Project Structure and Naming Conventions
- [React folder structure in 5 steps, 2025](https://www.robinwieruch.de/react-folder-structure/) by [Robin Wieruch](https://www.linkedin.com/in/robin-wieruch-971933a6/)
- [Folder Structure for React JS Project](https://www.geeksforgeeks.org/reactjs/folder-structure-for-a-react-js-project/)
### Linting
- [Rules of React](https://react.dev/reference/rules)
- [React Official Editor Setup](https://react.dev/learn/editor-setup#linting)
### Design Patterns
- [Sharing State Between Components](https://react.dev/learn/sharing-state-between-components)
- [React: Design Patterns](https://www.linkedin.com/learning/react-design-patterns-25656257) by [Shaun Wassell](https://www.linkedin.com/in/shaun-wassell), Linkedin Learning
- **Prioritizing Architecture over Framework in Web Development** - Presentation by [Alexandre Rivest](https://www.linkedin.com/in/alexandre-rivest-25a026a6/) at React Summit, June 2025
### Form Manipulation
- **Validating the Web: The Evolution of Form Validation** by [Luis Oliveira](https://www.linkedin.com/in/luis-oliveira-tech) at React Summit, June 2025.



