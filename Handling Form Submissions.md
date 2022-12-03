# Handling Form Submissions

### Adding event listener to `form`
- When handling form submissions, we put the event listener on the `form` element, not on the `button`.
- In the code below, we put an `onSubmit` listener to the form which references to the function `submitHandler`.
``` jsx
        <form onSubmit={submitHandler}>
            ...
            <div className="new-expense__actions">
                <button type="submit">Add Expense</button>
            </div>
        </form>
```
- When a form is submitted, the browser, by default, refreshes the pages. To prevent this, we use `preventDefault` in `submitHandler()`.
``` jsx
    const submitHandler = (evt) => {
        evt.preventDefault();

        const expenseData = {
            title: enteredTitle,
            amount: enteredAmount,
            date: new Date(enteredDate),
        };

        console.log(expenseData);
    };
```
- The values from the object come for the first values of the arrays created from calling `useState` individually.
``` jsx
    const [enteredTitle, setEnteredTitle] = useState("");
    const [enteredAmount, setEnteredAmount] = useState("");
    const [enteredDate, setEnteredDate] = useState("");
```

<br>

### Two-way binding to clear inputs after form submission
- To clear inputs after submitting a form, we basically just use the `set` methods for each field.
- In the code below, we pass an empty string to the `set` methods.
``` jsx
    const submitHandler = (evt) => {
        evt.preventDefault();

        const expenseData = {
            title: enteredTitle,
            amount: enteredAmount,
            date: new Date(enteredDate),
        };

        console.log(expenseData);
        setEnteredTitle("");
        setEnteredAmount("");
        setEnteredDate("");
    };
```
- However, in the form code, we also have to set the value of the `value` property to the `entered` values to make sure that the updated values, which is an empty string, reflect in the user interface.
``` jsx
        <form onSubmit={submitHandler}>
            <div className="new-expense__controls">
                <div className="new-expense__control">
                    <label>Title</label>
                    <input
                        type="text"
                        value={enteredTitle}
                        onChange={titleChangeHandler}
                    />
                </div>
                <div className="new-expense__control">
                    <label>Amount</label>
                    <input
                        type="number"
                        min="0.01"
                        step="0.01"
                        value={enteredAmount}
                        onChange={amountChangeHandler}
                    />
                </div>
                <div className="new-expense__control">
                    <label>Date</label>
                    <input
                        type="date"
                        min="2019-01-01"
                        max="2022-12-31"
                        value={enteredDate}
                        onChange={dateChangeHandler}
                    />
                </div>
            </div>
            <div className="new-expense__actions">
                <button type="submit">Add Expense</button>
            </div>
        </form>
```
- We basically added `value=enteredValue` in the code above
``` jsx
  <input
    type="text"
    value={enteredTitle}
    onChange={titleChangeHandler}
  />
```


