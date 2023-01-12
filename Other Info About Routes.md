### Other info about Routes

-   You cant declare multiple `Route` components for the same route. This will not cause make the app crash. Instead, it will render all the specified components in `element`

```jsx
function App() {
    return (
        <Fragment>
            <Routes>
                <Route path="/" element={<h1>Extra content</h1>} />
            </Routes>
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

-   In the code above, notice that there are two routes for the path `/`. Both `Home` and `<h1>Extra content</h1>` will then be rendered.
