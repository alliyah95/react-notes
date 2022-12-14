# React Portals

Portals are used when you want to place an HTML element on a certain place in the DOM or the rendered code in the browser. For example, say you have a `Modal`, you would want it to be at the top of everything because that is how modals work.

Ideal:

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <title>Sample Title</title>
    </head>
    <body>
        <div id="overlay-root"></div>
        <div id="root"></div>
    </body>
</html>
```

### How to use Portals

#### 1. Import `ReactDOM` from `react-dom`

```jsx
import ReactDOM from "react-dom";
```

#### 2. Use the method `ReactDOM.createPortal`

-   This method accepts two arguments, the element/component to portal or position, and the HTML node on where it will be positioned.

```js
{
    ReactDOM.createPortal(
        <ElementOrComponent onConfirm={props.somePropsToPass} />,
        document.getElementById("backdrop-root")
    );
}
```

-   In the code below, we are telling React to position `ModalOverlay` inside `overlay-root` which is basically a `div` positioned before `root` as seen on the code above.

```js
{
    ReactDOM.createPortal(
        <ModalOverlay title={props.title} message={props.message} />,
        document.getElementById("overlay-root")
    );
}
```

### Code context

```js
const ErrorModal = (props) => {
    return (
        <React.Fragment>
            {ReactDOM.createPortal(
                <Backdrop onConfirm={props.onConfirm} />,
                document.getElementById("backdrop-root")
            )}
            {ReactDOM.createPortal(
                <ModalOverlay title={props.title} message={props.message} />,
                document.getElementById("overlay-root")
            )}
        </React.Fragment>
    );
};
```

```html
...
<div id="backdrop-root"></div>
<div id="overlay-root"></div>
<div id="root"></div>
...
```
