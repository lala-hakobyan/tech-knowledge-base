# React Compiler
- **React Compiler** is a new compiler that is open sourced to get feedback from the community. It is a build-time only tool that automatically optimizes your React app. It works with plain JavaScript, and understands the Rules of React, so you don’t need to rewrite any code to use it.
- The compiler is currently released as rc, and is available to try out on React 17+ apps and libraries.
- The compiler is designed to compile functional components and hooks that follow the [Rules of React](https://react.dev/reference/rules).

## What does the Compiler Do?
- In order to optimize applications, React Compiler automatically memoizes your code.   
You may be familiar today with memoization through APIs such as `useMemo`, `useCallback`, and `React.memo`. 
With these APIs you can tell React that certain parts of your application don’t need to recompute if their inputs haven’t changed, reducing work on updates.   
While powerful, it’s easy to forget to apply memoization or apply them incorrectly. This can lead to inefficient updates as React has to check parts of your UI that don’t have any meaningful changes.
- The compiler uses its knowledge of JavaScript and React's rules to automatically memoize values or groups of values within your components and hooks. 
If it detects breakages of the rules, it will automatically skip over just those components or hooks, and continue safely compiling other code.
- You can use [React Compiler Playground](https://react.dev/learn/react-compiler) in order to check how the code is compiled.

## Getting started

### Installing Compiler
- The compiler is currently released as rc, and is available to try out on React 17+ apps and libraries. To install the RC, use:     
`npm install -D babel-plugin-react-compiler@rc eslint-plugin-react-hooks@^6.0.0-rc.1`
- React Compiler works best with React 19 RC. If you are unable to upgrade, you can install the extra `react-compiler-runtime` package which will allow the compiled code to run on versions prior to 19. However, note that the minimum supported version is 17.   
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
- React Compiler also powers an ESLint plugin. The ESLint plugin will display any violations of the rules of React in your editor. 
When it does this, it means that the compiler has skipped over optimizing that component or hook. 
This is perfectly okay, and the compiler can recover and continue optimizing other components in your codebase.  
- You can try it out by installing `eslint-plugin-react-hooks@^6.0.0-rc.1`.  
`npm install -D eslint-plugin-react-hooks@^6.0.0-rc.1`  
- See [official editor setup](https://react.dev/learn/editor-setup#linting) guide for more details.

## Compiler Configs
If you navigate to [React Compiler Playground](https://react.dev/learn/react-compiler) and open `EnvironmentConfig` section, you will see that there are plenty of options that React compiler offers.
Let's play around over some options that can help React Compiler to deliver better performance:
- `enableFunctionOutlining: true` in environment config    
  This option is set to true by default, and it is the option responsible for automatic memoization. However, it is has some limitations and is not enough to ensure memoization for all scenarios.
- Set `enableJsxOutlining: true` in environment config ensures that memoization is done even if the map callback contains variables declared outside the callback block like in this example (see variable `style`).
   ```js
   // @enableJsxOutlining
   export default function List({people}) {
     const style = useStyles();
     const items = useMemo(() =>
      people.map(({ id, name }) => (
        <li key={id}>
          <Text name={name} style={style} />
        </li>
      )), [people, style]);

      return (
        <ul>{items}</ul>
      );
  }
  ```
  `EnvironmentConfig` is not editable in React Compiler Playground, but we can use `// @enableJsxOutlining` annotation to enable the flag.
- Set `panicTresHold: none` setting in your plugin options to `critical_errors` or `all_errors` value in order to see `CannotPreserveMemoization` errors.    
  This error occurs when React Compiler cannot guarantee us that the memoization level that we had stays the same after React compiler did his job.   
  As mentioned, by default React Compiler will just skip the components that it cannot memoize and if you still want to see those components, you can use `panicTresHold` setting.
  ```js
   const parsedOptions = {target: '18'}
  
   export const defaultOptions: PluginOptions = {
     compilationMode: 'infer',
     ...,
     panicTresHold: 'critical_errors'
  }
  ```
- Set `"validatePreserveExistingMemoizationGuarantees": true` in environment config in order to see `CannotPreserveMemoization` errors mentioned above.
   ```js
   plugins: [
    [
      "babel-plugin-react-compiler",
      {
        ...config,
        envoronment: {
           validatePreserveExistingMemoizationGuarantees: true
        }
      }
    ]
  ]
  ```
  Actually this is recommended by React Compiler team.

## Documentation & References
- [React Compiler Official Documentation](https://react.dev/learn/react-compiler)
- [React Compiler Playground](https://playground.react.dev/#N4Igzg9grgTgxgUxALhAgHgBwjALgAgBMEAzAQygBsCSoA7OXASwjvwFkBPAQU0wAoAlPmAAdNvhgJcsNgB5CTAG4A+ABIJKlCPgDqOSoTkB6RaoDc4gL7iQVoA)
- [React Compiler Working Group](https://github.com/reactwg/react-compiler)
- [React Eslint guide](https://react.dev/learn/editor-setup#linting)
- [Rules of React](https://react.dev/reference/rules)
- [How to use React Compiler Tutorial](https://www.freecodecamp.org/news/react-compiler-complete-guide-react-19/)
- **React Compiler Internals** - Presentation by [Lydia Hallie](https://www.linkedin.com/in/lydia-hallie/) at React Summit, June 2025.
- **How to React Compiler** - Presentation by [Anton Nepsha](https://www.linkedin.com/in/nepshaaa/) at React Summit, June 2025.
