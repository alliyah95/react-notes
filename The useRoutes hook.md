### Using `useRoutes`

-   Aside from using the `Routes` and `Route` components, we can also use a hook called `useRoutes` to setup our routes.

```jsx
function App() {
    let element = useRoutes([
        {
            path: "/",
            element: <Home />,
        },
        {
            path: "*",
            element: <NotFound />,
        },
        {
            path: "/books",
            element: </Books/>
        },
    ]);
    return (
        <Fragment>
            <nav>
                <ul>
                    <li>
                        <Link to="/">Home</Link>
                    </li>
                    <li>
                        <Link to="/books">Books</Link>
                    </li>
                </ul>
            </nav>
            {element} //notice this one here
        </Fragment>
    );
}
```
