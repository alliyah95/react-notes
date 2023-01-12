### Using `NavLink`

-   This works the same way as `Link`, but it offers more properties that you can play around with.
-   This will change the color of `Home` to `red` when we’re currently at the path `/home`

```jsx
<NavLink
    style={({ isActive }) => {
        return isActive ? { color: "red" } : {};
    }}
    to="/home"
>
    Home
</NavLink>
```

-   By default, `NavLink` adds a class named `active` to the `NavLinks` that are currently being navigated.
