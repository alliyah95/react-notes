# Splitting Components Into Multiple Components
In any programming language, we want our functions to server **only one functionality**. The same applies to React components. Whenever possible, we should try splitting our components into multiple ones for the following reasons:
- Scalablity of code
- Readability of code
- When splitted components can be used in other parts of the app

### Original Code
- In the code below, we have an `ExpenseItem` component with a date functionality. Because this date can be used in other parts of the program, we can make it a separate component.
``` js
function ExpenseItem(props) {
    const month = props.date.toLocaleString("en-US", { month: "long" });
    const day = props.date.toLocaleString("en-US", { day: "2-digit" });
    const year = props.date.getFullYear();

    return (
        <div className="expense-item">
            <div>
                <div>{month}</div>
                <div>{year}</div>
                <div>{day}</div>
            </div>
            <div className="expense-item__description">
                <h2>{props.title}</h2>
                <div className="expense-item__price">${props.amount}</div>
            </div>
        </div>
    );
}
```
### Individual Date Component
ExpenseDate.js
``` js
import "./ExpenseDate.css";

function ExpenseDate(props) {
    const month = props.date.toLocaleString("en-US", { month: "long" });
    const day = props.date.toLocaleString("en-US", { day: "2-digit" });
    const year = props.date.getFullYear();

    return (
        <div className="expense-date">
            <div className="expense-date__month">{month}</div>
            <div className="expense-date__year">{year}</div>
            <div className="expense-date__day">{day}</div>
        </div>
    );
}

export default ExpenseDate;

```
ExpenseItem.js
``` js
import "./ExpenseItem.css";
import ExpenseDate from "./ExpenseDate";

function ExpenseItem(props) {
    return (
        <div className="expense-item">
            <ExpenseDate date={props.date}></ExpenseDate>
            <div className="expense-item__description">
                <h2>{props.title}</h2>
                <div className="expense-item__price">${props.amount}</div>
            </div>
        </div>
    );
}
```
- In `ExpenseItem.js`, we then simply pass the `date` to `ExpenseDate`.


