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

<br>

### Handling Multiple Events in One State
- In the code below, we may want to handle all input changes for `title`, `amount`, and `date`.
``` jsx
    return (
        <form>
            <div className="new-expense__controls">
                <div className="new-expense__control">
                    <label>Title</label>
                    <input type="text" onChange={titleChangeHandler} />
                </div>
                <div className="new-expense__control">
                    <label>Amount</label>
                    <input
                        type="number"
                        min="0.01"
                        step="0.01"
                        onChange={amountChangeHandler}
                    />
                </div>
                <div className="new-expense__control">
                    <label>Date</label>
                    <input
                        type="date"
                        min="2019-01-01"
                        max="2022-12-31"
                        onChange={dateChangeHandler}
                    />
                </div>
            </div>
            <div className="new-expense__actions">
                <button type="submit">Add Expense</button>
            </div>
        </form>
    );
```
- One way to do this is by calling `useState()` multiple times like in the code below:
``` jsx
    const [enteredTitle, setEnteredTitle] = useState("");
    const [enteredAmount, setEnteredAmount] = useState("");
    const [enteredDate, setEnteredDate] = useState("");
```
- Another is by calling `useState` only once, but passing an object to it containing the user inputs to which we want to listen to for events
``` jsx
    const [userInput, setUserInput] = useState({
        enteredTitle: "",
        enteredAmount: "",
        enteredDate: "",
    });
```
- The event handler functions would then look like these:
``` jsx
    const titleChangeHandler = (evt) => {
        setUserInput((prevState) => {
            return { ...prevState, enteredTitle: evt.target.value };
        });
    };

    const amountChangeHandler = (evt) => {
        setUserInput((prevState) => {
            return { ...prevState, enteredAmount: evt.target.value };
        });
    };

    const dateChangeHandler = (evt) => {
        setUserInput((prevState) => {
            return { ...prevState, enteredDate: evt.target.value };
        });
    };
```
- We use the spread operator `...` to ensure that all other values in the object are saved.
- `prevState` stores a copy of the object, then we return it together with the overidden key-value pair. 
