# Events and States

### Adding Event Listeners to React Elements
- Basically we add a `props` key to the element to which we want to add event listeners to.
- Event listeners start with the prefix `on`.
- The value to the added `props` should be a **function**.
- In the code below, when the button is clicked, `alert("Clicked!!")` will execute.
``` js
  <button onClick={() => {alert("Clicked!!");}}>Change Title</button>
```
- If a function named `clickHandler` is to be passed:
```js
  <button onClick={clickHandler}>Change Title</button>
```
- **Do not add parentheses! We are not executing the function.**

<br>

### Working With States
- We use the `useState` function for this.
- To work with states, we have to first import `useState` from the React library.
``` js
  import React, { useState } from "react";
```
- `useState` is basically a function that returns an array with a size of `2`.
- The first value is the **updated value**, while the second one is the function we can use to update the value.
- In the code below, `props.title` is the value that we expect to be changed or updated in the user interface.
``` js
  const [title, setTitle] = useState(props.title);
```
- `setTitle` is used in the event handler. The parameter is basically the updated value for `title`.
``` js
    const clickHandler = () => {
        setTitle("Updated value!");
    };
```
- After the function above is executed, the value of `title` becomes `Updated value!`
- **IMPORTANT:** Remember to use  `title` instead of `props.title` in your JSX code then because it is the one being updated, not `props.title`, whose value never changes because this only stores the initial value.
