# React Context

-   This is useful when dealing with an application-wide information or state.
-   You should utilize this when you find yourself passing data from one component to another, only to pass such data again to another component.

### How to use

1. Create a new folder `store` on the same root of `components` folder.
2. Inside the folder, create a file. Do not use CamelCase as we are not creating a component.

_auth-context.js_

```jsx
import React from "react";

const AuthContext = React.createContext({
    isLoggedIn: false,
});

export default AuthContext;
```

-   To create a React context, we call the method `createContext` from the React library.
-   The argument is an object which contains the information or state that we want to share accross our entire application.
-   When `createContext` is called, it returns a component which we can then use in our other components.

3. Import `AuthContext` in your component files.
4. We can then use `AuthContext` as a wrapper to our components. Everything that is wrapped around it will have access to the shared information or state. In other words, they will be _**part of the context**_.
5. Wrapping components is called **Providing**. `AuthContext` contains several comopnent in it. One of them is `Provider`.

```jsx
...
        <AuthContext.Provider value={{ isLoggedIn: false }}>
            <MainHeader isAuthenticated={isLoggedIn} onLogout={logoutHandler} />
            <main>
                {!isLoggedIn && <Login onLogin={loginHandler} />}
                {isLoggedIn && <Home onLogout={logoutHandler} />}
            </main>
        </AuthContext.Provider>
...
```

-   Remember that if you use `Provider`, you have to use its prop `value` as well. However, as opposed to the example above, the value should be dynamic and not hard coded.

6. To get access to the shared information, we **listen**. This can be done by using `useContext` or `Consume`. The former is more used than the latter, so we will be utilizing it.

### Using `useContext`

1. Perform the steps above.
2. Make sure that `AuthContext` is imported in the files where you want to use the shared state.
3. In the files where you will be using the shared information or stat, call `useContext` and pass in `AuthContext` as an argument.
4. Store the result in a variable.

```jsx
const context = useContext(AuthContext);
```

5. `context` will contain the key-value pairs that we previously specified in the `value` prop of `AuthContext.Provider` (see Step 5 above).
6. So if we want to access `isLoggedIn`, we do it by: `context.isLoggedIn`.

### Tips

7. We can also reference or point to a function in the `value` prop of `AuthContext.Provider`.

```jsx
const logoutHandler = () => {
    localStorage.removeItem("isLoggedIn");
    setIsLoggedIn(false);
};

<AuthContext.Provider
    value={{ isLoggedIn: isLoggedIn, onLogout: logoutHandler }}
>
    ...
</AuthContext.Provider>;
```

8. In `AuthContext` then, it would be a nice practice to add `onLogout` in the object of initial values (the values to be shared accross the app`.
9. Then, we just point to a dummy function. This is just to let VSCode suggest `onLogout` when using, say `context`.

```jsx
const AuthContext = React.createContext({
    isLoggedIn: false,
    onLogout: () => {},
});
```
