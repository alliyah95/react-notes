# Using `useEffect`

-   By using `useEffect`, you are telling React that your components needs to do something after the initial render.
-   The callback function we pass is basically the "effect", thet is, the changes that we want to happen to a component.

### Syntax

#### Using `useEffect` without any dependency

-   The code below runs for every render of the functional component in which its included.

```jsx
useEffect(callbackFn);
```

#### Using `useEffect` with an empty dependency array

-   The effect is executed only for the the initial render of the the functional component. And then it will not run in the further renders of the same functional Component..

```jsx
useEffect(callbackFn, []);
```

#### Using `useEffect` with a dependency array that is not empty

-   The effect will run for the initial render as well as when the render happen due to change in dependencies mentioned in the dependency array

```jsx
useEffect(callbackFn, [dependency1, dependency2, ...dependencyN]);
```

### Notes!

-   Never add state updating functions (`set` functions) as dependencies
-   Never add variables that are out of scope of the component as dependencies

### View Practice File

[Click Here](https://github.com/alliyah95/react-practice-files) _Note: The practice project for `useEffect` is the main branch because I was so dumb I accidentally forgot to create a new branch for it._
