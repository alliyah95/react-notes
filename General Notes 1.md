# General React Notes

## The `index.js` file
- The `index.js` file in the `src` folder is always the file that runs first wheneever the development server is started.

<br>

## The `ReactDOM` on `index.js`
- The line of code below basically tells the browser to replace the contents of the element with an id `root` with the content of `<App />
``` html
ReactDOM.render(<App />, document.getElementById('root'));
```
- The `root` element can be found in `public/index.html`
``` html
 <div id="root"></div>
```

<br>

## The `App` component
- A default component in React
- The `App.js` file uses `JSX` syntax. Basically, JavaScript with HTML and CSS.

``` js
function App() {
  return (
    <div>
      <h2>Let's get started!</h2>
      <h1> Hello</h1>
    </div>
  );
}

export default App;

```

<br>

## Introducing JSX
- JSX is essentially JavaScript XML.
