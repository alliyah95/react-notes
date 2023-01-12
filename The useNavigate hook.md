### The `useNavigate` hook

-   This hook is used to display some content from a component for a specific period of time, then redirect them to another page or path
-   In the code below, once the component `NotFound` is rendered, `<div>NotFound</div>` will be initially shown. After `1000ms` or basically 1 second, the effect inside `useEffect` will execute.
-   Using the `navigate` function returned by `useNavigate`, the user will be redirected to the specified path, which in this case is `/home`
-   Tip: passing in `-1` to navigate will basically simulate hitting the back button in your browser.

```jsx
import React, { useEffect } from "react";
import { useNavigate } from "react-router-dom";

const NotFound = () => {
    const navigate = useNavigate();

    useEffect(() => {
        setTimeout(() => {
            navigate("/home");
        }, 1000);
    }, []);

    return <div>NotFound</div>;
};

export default NotFound;
```
