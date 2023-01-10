### Nested Routes

-   We literally just nest routes.

```jsx
function App() {
    return (
        <Fragment>
            ....
            <Routes>
                <Route path="/" element={<Home />} />
                <Route path="/books">
                    <Route index element={<BookList />} /> //this component will
                    load when /books is opened
                    <Route path=":id" element={<Book />} /> //this means /books/new
                    <Route path="new" element={<NewBook />} /> //this means
                    /books/:id
                </Route>
                <Route path="*" element={<NotFound />} />
            </Routes>
        </Fragment>
    );
}
```

### Taking Advantage of Nested Routes

```jsx
function App() {
    return (
        <Fragment>
            ....
            <Routes>
                <Route path="/" element={<Home />} />
                <Route path="/books" element={<BookLayout />}>
                    <Route index element={<BookList />} />
                    <Route path=":id" element={<Book />} />
                    <Route path="new" element={<NewBook />} />
                </Route>
                <Route path="*" element={<NotFound />} />
            </Routes>
        </Fragment>
    );
}
```

-   In the code above, notice the line `<Route path="/books" element={<BookLayout />}>`
-   This basically means that whenever `/books` and its nested routes are navigated to, the component `BookLayout` will be rendered. In other words, its like `BookList`, `Book`, and `NewBook` are wrapped around `BookLayout`

### The `Outlet` Component

-   In the code above, although routes are nested, the content of `BookList`, `Book` and `NewBook` will not be rendered. To fix this, we have to define the `Outlet` component in `BookLayout`

```jsx
const BookLayout = () => {
    return (
        <div>
            <Link to="/books/1">Book 1</Link>
            <Link to="/books/2">Book 2</Link>
            <Link to="/books/3">Book 3</Link>
            <br />
            <Link to="/books/new">Create a new book</Link>
            <Outlet />
        </div>
    );
};
```

-   `Outlet` basically renders what nested routes should render.
-   We can also pass in context to `Outlet`. All components in the nested routes will then have access to `context`

```jsx
const BookLayout = () => {
    return (
        <div>
            <Link to="/books/1">Book 1</Link>
            <Link to="/books/2">Book 2</Link>
            <Link to="/books/3">Book 3</Link>
            <br />
            <Link to="/books/new">Create a new book</Link>
            <Outlet context={{ hello: "World" }} />
        </div>
    );
};
```

-   To access the `context` values, we use a hook called `useOutletContext`

```jsx
const obj = useOutletContext();
```
