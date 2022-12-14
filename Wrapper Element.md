# Wrapper Element
- To avoid the **`<div>` soup** problem on React apps, you can simply create a `Wrapper` component whose function is to only return `props.children`.
- `Wrapper` does not basically render any HTML element.

Wrapper.js
``` js
  const Wrapper = (props) => {
      return props.children;
  };

  export default Wrapper;
```

### How to use the wrapper element
- We basically use `Wrapper` to wrap around the code we return from our other components
``` js
  return <Wrapper>
            <h1>Hi</h1> <h2>Hola</h2>
          </Wrapper>
```
