# Clean Code Principles
**Clean Code principles** were firstly introduced by Robert C. Martin’s book "Clean Code". By adhering to these principles, developers can create code that is more maintainable, readable, and easier to collaborate on, leading to higher quality software.
- Based on that book, **Clean Code** is code that is easy to read, understand, and maintain.    
- It prioritizes clarity, simplicity, and expressiveness over cleverness or complexity.    
- Key principles include **using meaningful names**, **writing small functions**, **avoiding duplication**, **eliminating side effects**, and **keeping code expressive**.

## Detailed Breakdown of Clean Code Principles
### 1. Meaningful Names
- Use descriptive and unambiguous names for variables, functions, and classes that clearly indicate their purpose.
- Avoid single-letter names or cryptic abbreviations.
- Choose names that are easy to pronounce and search for.
- Example: `getUserInfo()` is better than `getData()`.

### 2. Small Functions:
- Functions should ideally be short and focused on a single task. Aim for functions that are no more than 20-30 lines long, and ideally even shorter.
- Aim for functions with three or fewer parameters.
- Break down large functions into smaller, more manageable ones.
- Avoid flag arguments - use separate functions for different operations. 

### 3. Avoid Duplication (DRY - Don't Repeat Yourself):
- Identify and eliminate duplicated code by extracting it into reusable functions or modules.
- Use functions, classes, or existing libraries to avoid redundancy.

### 4. Eliminate Side Effects:
- Functions should ideally have no side effects, meaning they should only perform the task they are intended for without altering external state.
- Avoid methods that both change object state and return values: use separate methods for each.

### 6. Keep Code Expressive:
- Write code that explains itself, minimizing the need for comments.
- Use comments to explain complex logic or clarify intent, but avoid obvious or redundant comments.
- Remove commented-out code - it's better to refactor or delete it.

### 6. Consistency:
- Maintain a consistent coding style throughout the project, including naming conventions, formatting, and indentation.
- Use tools like linters and formatters to enforce consistent style.

### 7. Simplicity:
- Favor simple and straightforward solutions over complex or clever ones.
- Write code that is easy to understand and maintain.

### 8. Modularity (Separation of Concerns):
- Break down code into smaller, self-contained modules or components.
- Each module/class/function should have a single responsibility.
- This promotes reusability, encapsulation, and easier maintenance.

### 9. Testability:
- Write code that is easy to test, with clear separation of concerns.
- Use unit tests to verify the behavior of individual components.

## Documentation and References
- Book "Clean Code: A Handbook of Agile Software Craftsmanship" by Robert C. Martin
- [Tutorial: Clean code #3 - Writing better Functions](https://www.youtube.com/watch?v=mvgTQAVRpKA&t=154s)
- [Clean Code Javascript Adaptation](https://github.com/ryanmcdermott/clean-code-javascript)