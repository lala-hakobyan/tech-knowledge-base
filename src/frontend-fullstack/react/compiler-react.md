# React Compiler
- React Compiler is a new compiler that is open sourced to get feedback from the community. It is a build-time only tool that automatically optimizes your React app. It works with plain JavaScript, and understands the Rules of React, so you don’t need to rewrite any code to use it.
- The compiler is currently released as rc, and is available to try out on React 17+ apps and libraries.
- The compiler is designed to compile functional components and hooks that follow the [Rules of React](https://react.dev/reference/rules).

## What does the Compiler Do?
- In order to optimize applications, React Compiler automatically memoizes your code.   
You may be familiar today with memoization through APIs such as `useMemo`, `useCallback`, and `React.memo`. 
With these APIs you can tell React that certain parts of your application don’t need to recompute if their inputs haven’t changed, reducing work on updates.   
While powerful, it’s easy to forget to apply memoization or apply them incorrectly. This can lead to inefficient updates as React has to check parts of your UI that don’t have any meaningful changes.
- The compiler uses its knowledge of JavaScript and React’s rules to automatically memoize values or groups of values within your components and hooks. 
If it detects breakages of the rules, it will automatically skip over just those components or hooks, and continue safely compiling other code.
- You can use [React Compiler Playground](https://react.dev/learn/react-compiler) in order to check how the code is compiled.

## Getting started

### Installing Compiler
- The compiler is currently released as rc, and is available to try out on React 17+ apps and libraries. To install the RC:  
`npm install -D babel-plugin-react-compiler@rc eslint-plugin-react-hooks@^6.0.0-rc.1`
  - React Compiler works best with React 19 RC. If you are unable to upgrade, you can install the extra react-compiler-runtime package which will allow the compiled code to run on versions prior to 19. However, note that the minimum supported version is 17.
  `npm install react-compiler-runtime@rc`
  - You should also add the correct target to your compiler config, where target is the major version of React you are targeting:  
    ```js
    // babel.config.js
    const ReactCompilerConfig = {
      target: '18' // '17' | '18' | '19'
    };
  
    module.exports = function () {
      return {
        plugins: [
          ['babel-plugin-react-compiler', ReactCompilerConfig],
        ],
      };
    };
    ```

### Installing eslint-plugin-react-hooks
React Compiler also powers an ESLint plugin. The ESLint plugin will display any violations of the rules of React in your editor. 
When it does this, it means that the compiler has skipped over optimizing that component or hook. 
This is perfectly okay, and the compiler can recover and continue optimizing other components in your codebase.  
You can try it out by installing `eslint-plugin-react-hooks@^6.0.0-rc.1`.  
`npm install -D eslint-plugin-react-hooks@^6.0.0-rc.1`  
See [official editor setup](https://react.dev/learn/editor-setup#linting) guide for more details.

## Documentation
- [React Compiler Official Documentation](https://react.dev/learn/react-compiler)
- [React Compiler Playground](https://playground.react.dev/#N4Igzg9grgTgxgUxALhAgHgBwjALgAgBMEAzAQygBsCSoA7OXASwjvwFkBPAQU0wAoAlPmAAdNvhgJcsNgB5CTAG4A+ABIJKlCPgDqOSoTkB6RaoDc4gL7iQVoA)
- [React Compiler Working Group](https://github.com/reactwg/react-compiler)
- [React Eslint guide](https://react.dev/learn/editor-setup#linting)
