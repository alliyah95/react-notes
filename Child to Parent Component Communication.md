# Child to Parent Component Communication

### Scenario
- Say we have 3 components, `App`, `NewExpense`, and `ExpenseForm`.
- `App` renders `NewExpense`, while `ExpenseForm` is rendered along with `NewExpense`
- Therefore: `App` -> `NewExpense` -> `ExpenseForm`

### What needs to happen
- When `Form` is filled out, the submitted data should be passed to its parent, `NewExpense`, which also needs to pass the organized `ExpenseForm` data to `App` for rendering.
- Basically, all children components must pass data to their parent component.
- The code below shows what the files look like 
<br>

_App.js_
``` jsx
    return (
        <div>
            <NewExpense></NewExpense>
            <Expenses items={expenses} />
        </div>
    );
```
_NewExpense.js_
``` jsx
    return (
        <div className="new-expense">
            <ExpenseForm></ExpenseForm>
        </div>
    );
```
_ExpenseForm.js_
``` jsx
    return (
        <form onSubmit={submitHandler}>
            <div className="new-expense__controls">
                ...
            <div className="new-expense__actions">
                <button type="submit">Add Expense</button>
            </div>
        </form>
    );
```
<br>

### Solution
#### TLDR
- Gawa ka ng function sa parent component with a parameter representing the data na ipa-pass ng child component.
- Make this function a property of the children component kapag ica-call yung child component sa file ng parent component.
- Sa form sa child element, specically sa form submission handler function, just call the function and pass in the data as an argument.
```
    props.parentFunction()
```
#### Long explanation
- On the parent component, add a `property` that points to a `function` to the child component when it is **called**.
- Say in `NewExpense.js`, originally, `ExpenseForm`, which is its child, did not have the `onSaveExpenseData` property.
``` jsx
    return (
        <div className="new-expense">
            <ExpenseForm
                onSaveExpenseData={saveExpenseDataHandler}
            ></ExpenseForm>
        </div>
    );
```
- The function `saveExpenseDataHandler` it points to is as follows:
``` jsx
    const saveExpenseDataHandler = (enteredExpenseData) => {
        const expenseData = {
            ...enteredExpenseData,
            id: Math.random().toString(),
        };
    };
```
- In the `submitHandler` of `ExpenseForm` then, we can call `onSaveExpenseData` like a function. Then, we pass the expected data, which is `expenseData` as an argument.
- Basically, `saveExpenseDataHandler` is then called, then `expenseData` is the argument for the parameter `enteredExpenseData`. We can now access the passed data in `NewExpense.js`.
``` jsx
    const submitHandler = (evt) => {
        evt.preventDefault();

        const expenseData = {
            title: enteredTitle,
            amount: enteredAmount,
            date: new Date(enteredDate),
        };

        props.onSaveExpenseData(expenseData);
        setEnteredTitle("");
        setEnteredAmount("");
        setEnteredDate("");
    };
```
- For `App.js` to access the data in `NewExpense.js`, we do the same process.
- In`App.js` we add a property `onAddExpense` to `NewExpense`
``` jsx
    return (
        <div>
            <NewExpense onAddExpense={addExpenseHandler}></NewExpense>
            <Expenses items={expenses} />
        </div>
    );
```
- The function is points to is `addExpenseHandler` which is as follows. `expense` is the expected data coming from `NewExpense.js`
``` jsx
    const addExpenseHandler = (expense) => {
        console.log(expense);
    };
```
- To be able to pass data from `NewExpense.js` to `App.js`, we call the `onAddExpense` property and pass data as an argument
- Highlight here is `props.onAddExpense(expenseData)`.
``` jsx
    const saveExpenseDataHandler = (enteredExpenseData) => {
        const expenseData = {
            ...enteredExpenseData,
            id: Math.random().toString(),
        };
        props.onAddExpense(expenseData);
    };
```




