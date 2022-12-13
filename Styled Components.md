# Styled Components

### To install:
```
  npm i styled-components 
```

### To use:
```
  import styled from "styled-components"; 
```

### Basic usage
- Styled components basically returns the specified HTML element of your choice together with the styles that you've provided as well.

### Syntax
``` jsx
  const Button = styled.button``;
```

### Explanation
- The `styled` object returns an HTML element `button` with the specified styles inside the back ticks.

### Example
- In providing the style, make sure to get rid of any selectors, execpt for pseudo-selectors. For such selectors, you may use an ampersand `&` to represent them.
``` jsx
  const Button = styled.button`
      font: inherit;
      padding: 0.5rem 1.5rem;
      border: 1px solid #8b005d;
      color: white;
      background: #8b005d;
      box-shadow: 0 0 4px rgba(0, 0, 0, 0.26);
      cursor: pointer;

      &:focus {
          outline: none;
      }

      &:hover,
      &:active {
          background: #ac0e77;
          border-color: #ac0e77;
          box-shadow: 0 0 8px rgba(0, 0, 0, 0.26);
      }
  `;
```
- In vanila CSS, the code above would look like this:
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
