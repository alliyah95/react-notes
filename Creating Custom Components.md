# Creating Custom Components

## Essentials
- Create a `components` folder inside of `src`
- Use `PascalCase` naming convention when creating component files.

<br>

## Main Takeaways
### Component -> Function
- A component in react is essentially just a function. In the code below `App` is a component.
``` js
function App() {
  return (
    <div>
      <h2 className="text-5xl bg-emerald-500">Let's get started!</h2>
      <p>This is also visible</p>
    </div>
  );
}

export default App;
```
### There should only be one root element in the `return` statement of a component
- The code below will produce an error because it seems like there are 3 root elements, that is the 3 `div`.
``` js
function ExpenseItem() {
  return (
      <div>Date</div>
      <div>Title</div>
      <div>Amount</div>
  );
}
```
- To solde the problem above, the elements can be wrapped in a single `div`.
``` js
function ExpenseItem() {
  return (
    <div>
      <div>Date</div>
      <div>Title</div>
      <div>Amount</div>
    </div>
  );
}

```

<br>

## Creating a sample React component
1. In the `components` folder, create an `ExpenseItem.js` file
2. Write the code below:
``` js
function ExpenseItem() {
    return(
        <h2>I am an ExpenseItem component!</h2>
    )
}

export default ExpenseItem;
```
3. To be able to use the component, import it to `App.js`
4. To use the component, treat it like you would treat an HTML elements such as a `div`, `h1`, `p`, etc.
``` js
import ExpenseItem from "./components/ExpenseItem";

function App() {
  return (
    <div>
      <h2 className="text-5xl bg-emerald-500">Let's get started!</h2>
      <p>This is also visible</p>
      <ExpenseItem></ExpenseItem>
    </div>
  );
}

export default App;
```

<br>

## Outputting Dynamic Data Part 1
- You basically make use of curly braces `{}`
``` js
function ExpenseItem() {
    const expenseDate = new Date(2021, 2, 28);
    const expenseTitle = "Car Insurance";
    const expenseAmount = 294.67;

    return (
        <div className="expense-item">
            <div>{expenseDate.toISOString()}</div>
            <div className="expense-item__description">
                <h2>{expenseTitle}</h2>
                <div className="expense-item__price">${expenseAmount}</div>
            </div>
        </div>
    );
}
```

<br>

## Outputting Dynamic Data Part 2
- To share data between React components, make use of the `props` concept.
- In React, there is always one parameter for every function / component. Inside this paramater, passed objects or information are stored.
- To pass data from `App.js` to `ExpenseItem.js`:
<br>
App.js

``` js
function App() {
    const expenses = [
        {
            id: "e1",
            title: "Toilet Paper",
            amount: 94.12,
            date: new Date(2020, 7, 14),
        },
        {
            id: "e2",
            title: "New TV",
            amount: 799.49,
            date: new Date(2021, 2, 12),
        }
    ];

    return (
        <div>
            <h2 className="text-5xl bg-emerald-500">Let's get started!</h2>
            <ExpenseItem
                title={expenses[0].title}
                amount={expenses[0].amount}
                date={expenses[0].date}
            ></ExpenseItem>
            <ExpenseItem
                title={expenses[1].title}
                amount={expenses[1].amount}
                date={expenses[1].date}
            ></ExpenseItem>
        </div>
    );
}
```
<br> ExpenseItem.js
``` js
function ExpenseItem(props) {
    return (
        <div className="expense-item">
            <div>{props.date.toISOString()}</div>
            <div className="expense-item__description">
                <h2>{props.title}</h2>
                <div className="expense-item__price">${props.amount}</div>
            </div>
        </div>
    );
}
```
- Basically, the syntax would be like this:
``` js
<MyComponent property1={value1} property2={value2} ... propertyN={valueN}></MyComponent>
```
- To access the passed data in the component file:
``` js
 function MyComponent(props){
    return (
      <div>
          <p> {props.property1} </p>
          <p> {props.property2} </p>
          ...
          <p> {props.propertyN} </p>
      </div>
    );
}
```
- Basically, all passed key-value pairs are stored in `props`. We access the values in the component file then by accessing the keys.
