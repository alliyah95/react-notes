# Using `useReducer`

-   This hook is used for handling multiple states.

### Syntax

```jsx
const [state, dispatch] = useReducer(reducer, { count: 0 });
```

-   `reducer` is a function wherein we define what we want to happen to a state.
-   ` { count: 0}` is the initial value for our state. We normally want to pass an object instead of just a value, that is `0` only.
-   `state` contains `count` and all other initialized values. They can be accessed using dot notation (e.g. `state.count`)
-   `dispatch`, similar to the second array value returned by `useState`, is also a function. Whenever it is called, `reducer` is consequently called.

### Sample App

-   The app below is just a simple counter app that utilizes `useReducer` for updating the state of the current count.
-   In the `reducer` function, we don't pass in anything to `state` because by default, it has this parameter. Similar to set updating functions whenever
    we use `useState`, the current state is always stored at `state`.
-   What we pass in to `action` should be an object. Then, when accessing our arguments inside the `reducer` function, we use dot notation.
-   **Reminder:** `reducer` is called by calling `dispatch`!

```jsx
import React, { useReducer } from "react";
const ACTIONS = {
    INCREMENT: "increment",
    DECREMENT: "decrement",
};
function reducer(state, action) {
    switch (action.type) {
        case ACTIONS.INCREMENT:
            return { count: state.count + 1 };
        case ACTIONS.DECREMENT:
            return { count: state.count - 1 };
        default:
            return state;
    }
}

function App() {
    const [state, dispatch] = useReducer(reducer, { count: 0 });

    function increment() {
        dispatch({ type: ACTIONS.INCREMENT });
    }

    function decrement() {
        dispatch({ type: ACTIONS.DECREMENT });
    }

    return (
        <div className="App">
            <>
                <button onClick={decrement}>-</button>
                <span>{state.count}</span>
                <button onClick={increment}>+</button>
            </>
        </div>
    );
}

export default App;
```

### Another app

-   If want to pass in data to `reducer`, we can add another property to the passed object named `payload`. The value of payload is then another object.
    App.js

```jsx
import React, { useState, useReducer } from "react";
import Todo from "./Todo";

export const ACTIONS = {
    ADD_TODO: "add-todo",
    TOGGLE_TODO: "toggle-todo",
    DELETE_TODO: "delete-todo",
};
function reducer(todos, action) {
    switch (action.type) {
        case ACTIONS.ADD_TODO:
            return [...todos, newTodo(action.payload.name)];
        case ACTIONS.TOGGLE_TODO:
            return todos.map((todo) => {
                if (todo.id === action.payload.id) {
                    return { ...todo, complete: !todo.complete };
                }
                return todo;
            });
        case ACTIONS.DELETE_TODO:
            return todos.filter((todo) => todo.id !== action.payload.id);
    }
}

function newTodo(name) {
    return { id: Date.now(), name: name, complete: false };
}

function App() {
    const [todos, dispatch] = useReducer(reducer, []);
    const [name, setName] = useState("");

    const handleSubmit = (e) => {
        e.preventDefault();
        dispatch({ type: ACTIONS.ADD_TODO, payload: { name: name } });
        setName("");
    };

    return (
        <React.Fragment>
            <form onSubmit={handleSubmit}>
                <input
                    type="text"
                    value={name}
                    onChange={(e) => setName(e.target.value)}
                />
            </form>
            {todos.map((todo) => {
                return <Todo key={todo.id} todo={todo} dispatch={dispatch} />;
            })}
        </React.Fragment>
    );
}

export default App;
```

Todo.js

```jsx
import React from "react";
import { ACTIONS } from "./App";
const Todo = ({ todo, dispatch }) => {
    return (
        <div>
            <span style={{ color: todo.complete ? "#AAA" : "#000" }}>
                {todo.name}
            </span>
            <button
                onClick={() =>
                    dispatch({
                        type: ACTIONS.TOGGLE_TODO,
                        payload: { id: todo.id },
                    })
                }
            >
                Toggle
            </button>
            <button
                onClick={() =>
                    dispatch({
                        type: ACTIONS.DELETE_TODO,
                        payload: { id: todo.id },
                    })
                }
            >
                Delete
            </button>
        </div>
    );
};

export default Todo;
```

### Code is from [Web Dev Simplified](https://www.youtube.com/watch?v=kK_Wqx3RnHk)
