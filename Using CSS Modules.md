# Using CSS Modules

### How to
1. Your `.css` files should be renamed as `<ComponentName>.module.css`. For example, `Button.css` should be renamed to `Button.module.css`.
2. On your `JSX` or `JS` file, import the `module.css` file using the syntax below. **Take note of the word `styles`**.
``` js
  import styles from "./Button.module.css";
```
3. To use your classes, you basically just have to pass in `styles` to `className`. However, we have to be more specific. Since we only want to apply the styles for the class `button`, we write `styles.button`.
```js
  <button type={props.type} className={styles.button} onClick={props.onClick} > </button>
```
Complete code:
``` js
  const Button = (props) => {
      return (
          <button
              type={props.type}
              className={styles.button}
              onClick={props.onClick}
          >
              {props.children}
          </button>
      );
  };
```

#### Context
Button.module.css
``` css
  .button {
    font: inherit;
    padding: 0.5rem 1.5rem;
    border: 1px solid #8b005d;
    color: white;
    background: #8b005d;
    box-shadow: 0 0 4px rgba(0, 0, 0, 0.26);
    cursor: pointer;
  }

  .button:focus {
    outline: none;
  }

  .button:hover,
  .button:active {
    background: #ac0e77;
    border-color: #ac0e77;
    box-shadow: 0 0 8px rgba(0, 0, 0, 0.26);
}
```

### Using multiple classes from your CSS modules
- Here, we use the style for `form-control`. However, we also want to apply the styles for `invalid` is `isValid` has a value of `True`.
``` js
  <div lassName={`${styles["form-control"]} ${!isValid && styles.invalid}`}>
```

#### Context
``` css
  .form-control {
      margin: 0.5rem 0;
  }

  .form-control label {
      font-weight: bold;
      display: block;
      margin-bottom: 0.5rem;
  }

  .form-control input {
      display: block;
      width: 100%;
      border: 1px solid #ccc;
      font: inherit;
      line-height: 1.5rem;
      padding: 0 0.25rem;
  }

  .form-control input:focus {
      outline: none;
      background: #fad0ec;
      border-color: #8b005d;
  }

  .form-control.invalid input {
      border-color: red;
      background: #ffd7d7;
  }

  .form-control.invalid label {
      color: red;
  }

```
