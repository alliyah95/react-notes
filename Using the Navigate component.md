### Using the `Navigate` component

-   This component is used to **navigate** users to a certain page.
-   In the code below, whenever `NotFound` is rendered, the user will be redirected to `/home`

```jsx
import React from "react";
import { Navigate } from "react-router-dom";

const NotFound = () => {
    return <Navigate to="/home"></Navigate>;
};

export default NotFound;
```
