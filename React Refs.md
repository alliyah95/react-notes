# Refs

-   Refs are basically **references**.
-   They can be used to connect or _reference_ components.

### Using Refs to get user inputs

#### 1. Import `useRef` from the `react` library.

```js
import React, { useRef } from "react";
```

#### 2. Call the `useRef` method.

... and store the result to a variable to which you want to reference your inputs to. Basically, such variable will store the input.

```jsx
const nameInputRef = useRef();
```

#### 3. Add the `ref` attribute to `input` element

... and point to the previously created variable.

```jsx
<input id="username" type="text" ref={nameInputRef} />
```

#### 4. Retrieve the input

-   On your form submit handler function, retrieve the input by calling `current.value` on `nameInputRef` or the previously created variable.
-   We do this because `ref` actually returns the actual `input` node or object, but we only want the value.

```jsx
const enteredName = nameInputRef.current.value;
```
