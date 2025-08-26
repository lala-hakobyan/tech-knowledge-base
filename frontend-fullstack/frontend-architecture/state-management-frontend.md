# State Management in Front-end
**Frontend state management** is the process of **handling**, **synchronizing**, and **updating the data** (or "state") that determines a web application's behavior and appearance across components. 
This can be done using built-in framework capabilities, such as **Angular Signals or RxJS**, **React Context API**, or using libraries like **Redux**, **Zustand**, and **NgRx**.

Effective state management is crucial for long-term scalability and maintainability of front-end applications. It ensures a seamless user experience by keeping the UI consistent and making state changes predictable.

## Front-End State Management Terminology
Let's explore the main terminology in front-end state management before we start exploring different tools and patterns:

- **State**: A piece of data that represents the current snapshot of your application and determines its behavior or appearance.   
  **Example:**
    ```javascript
    const [isOpen, setIsOpen] = useState(false); // whether a modal is open
    ```

- **Store**: A centralized container that holds state, provides rules for updating it, and allows components to access or react to changes.   
  **Example:**
    ```javascript
    import create from "zustand";
    
    const useStore = create(set => ({
      count: 0,
      increment: () => set(state => ({ count: state.count + 1 }))
    }));
    ```

> **Note:** A **store** contains **state** and provides mechanisms to update or access it across the application.


## Managing Complex Front-End Stores with Normalized State
Normalized state is a way of storing your front-end state like a database:
- Each entity type (posts, comments, users) has its own “table” in the store
- Each item is stored once, referenced by its ID
- Arrays of IDs are used for ordering
  In other words, there is only one source of truth for each entity.

### The Problem with Hierarchical State ❌
Imagine we have hierarchical data coming from the backend that needs to be stored on the frontend.  
We have a news feed with the following entities: **Post**, **Comment**, and **User**.  
A **Post** has many **Comments**, and both are written by a **User**:

```
const posts = [
  {
    id: "post1",
    author: { id: "user1", username: "Jane" },
    body: "...",
    comments: [
      { id: "c1", author: { id: "user2", username: "John" }, comment: "..." },
      ...
    ]
  },
  {
    id: "post2",
    author: { id: "user2", username: "John" },
    body: "...",
    comments: [
      { id: "c2", author: { id: "user1", username: "Jane" }, comment: "..." },
      ...
    ]
  },
  ...
];
```

If `Jane` changes her username, it must be updated in `post1.author`, `comment2.author`, and everywhere else she appears.

That means:
- **Duplication** - same user stored in multiple places
- **Complex updates** - deeply nested reducers
- **Performance issues** - small updates may cause big re-renders

### The Solution with Normalized State ✅
Instead of storing hierarchical data, store each entity separately.  
Use `byId` to store the objects of each entity and `allIds` to store the list of IDs.  
This gives consumers flexibility: query byId (e.g., `posts.byId.post1`) or get the full list (`posts.allIds`).

With this solution, if `Jane` updates her username, it changes in one place only: `users.byId.user1`.

Here’s how the same data looks when normalized:

```
const normalizedState = {
  posts: {
    byId: {
      post1: { id: "post1", author: "user1", body: "...", comments: ["c1", ...] },
      post2: { id: "post2", author: "user2", body: "...", comments: ["c2", ...] },
      ...
    },
    allIds: ["post1", "post2", ...]
  },
  comments: {
    byId: {
      c1: { id: "c1", author: "user2", comment: "..." },
      c2: { id: "c2", author: "user1", comment: "..." },
      ...
    },
    allIds: ["c1", "c2", ...]
  },
  users: {
    byId: {
      user1: { username: "user1", name: "Jane" },
      user2: { username: "user2", name: "John" },
      ...
    },
    allIds: ["user1", "user2", ...]
  }
};
```

### Advantages of Using Normalized State
- **Single source of truth** - no duplication
- **Simpler updates** - reducers are flatter and easier
- **Better performance** - fewer unnecessary re-renders

### When to Use Normalized State?
Use **Normalized State** only when it applies to your problem.

✅ Use it when:
- You have nested relational data  
- Entities are updated independently or frequently

❌ Avoid it when:
- Data is flat  
- Updates happen only from a single source

Normalized state can make store easier to maintain and UI more predictable.  
It is game changer when working with complex state using the **Redux pattern**, **React Redux**, **NgRx**, or any other similar library like **Zustand**.


## Documentation and References
- [Redux Official Docs: Normalizing State Shape](https://redux.js.org/usage/structuring-reducers/normalizing-state-shape)