### Installation

```bash
npm i react-router-dom
```

### Types of `Router`

### `MemoryRouter`

-   does not change the actual URL

### `StaticRouter`

-   used when working with servers

### Basic Usage

1. Import a router of your choice in `index.js`. For our example, we will be using `BrowserRouter`

```bash
import { BrowserRouter } from "react-router-dom";
```

-   `BrowserRouter` is a **context**.

2. Import `Route` and `Routes` from `react-router-dom` in `App.js`

```jsx
import { Route, Routes } from "react-router-dom";
```

3. Setup your routes in `App.js`

```jsx
import "./App.css";
import { Route, Routes } from "react-router-dom";
import Home from "./pages/Home";

function App() {
    return (
        <Routes>
            // this is going to be the root route
            <Route path="/" element={<Home />} />
            <Route />
            <Route />
        </Routes>
    );
}

export default App;
```

-   In the code above, we setup a `Route` component for each page that we want a route for. These `Route` components are then nested inside a `Routes` component.
-   `path` : the URL we want a page/component
-   `element` : the component or page that we want to load when we navigate to the specified `path`. This is typically a React component (JS/JSX file)

4. To navigate between routes, we use the `Link` component, which under the hood, is just an anchor tag `a`.

```jsx
function App() {
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
            <Routes>
                <Route path="/" element={<Home />} />
                <Route path="/books" element={<BookList />} />
                <Route />
            </Routes>
        </Fragment>
    );
}
```

-   In the code above, take note that **only the components inside `Routes` are re-rendered every time a `Link` is clicked.**

5. To use custom parameters in your URL:

```jsx
<Routes>
    .... // this will render the Book element when the URL is something like
    //localhost:3000/books/123 // where 123 is ID
    <Route path="/books/:id" element={<Book />} />
</Routes>
```

6. To access the parameters in the link, we use the hook `useParams`

```jsx
import { useParams } from "react-router-dom";

const Book = () => {
    const { id } = useParams();
    return <div>Book {id}</div>;
};

export default Book;
```

-   `useParams` basically returns all the parameters you customized

6. To access your `Error 404 : PAGE NOT FOUND`:

```
<Routes>
		...
		<Route path="*" element={<NotFound />} />
</Routes>
```

-   Whenever the user navigates to a URL that does not match with any of the ones that you’ve specified, `NotFound` will be rendered.
