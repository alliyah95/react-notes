# Handling User Inputs From Forms

### Handling Single User Input
- To handle user input from forms, we basically listen to **all changes** that happen to `input`.
- This is done by using the `onChange` attribute of `input`
- In the code below, we want to get the user input for `email`
``` jsx
  <div className="form-group">
    <label htmlFor="email">Email</label>
    <input type="text" id="email"/>
  </div>
```
- So, we add the `onChange` attribute which points to a function `emailChangeHandler`. Basically, whenever changes are detected in `email`, `emailChangeHandler` gets called.
``` jsx
  <div className="form-group">
    <label htmlFor="email">Email</label>
    <input type="text" id="email" onChange={emailChangeHandler} />
  </div>
```
- The function `emailChangeHandler` looks like this:
``` jsx
    const [email, setEmail] = useState();
    const emailChangeHandler = (evt) => {
        setEmail(evt.target.value);
    };
```
- We basically make use of `useState` still. The parameter `evt` is automatically passed to the function whenever changes are made in `input`.
- `evt` contains a lot of things, including the inputted email in the field which can be accessed by `evt.target.value`
- We then call `setEmail` and pass the said value to the function. The passed value gets stored to `email`. The final value is always stored there.

### Handling Multiple User Inputs
- To handle multiple user inputs, we can just simply repate the above process `n` times.
- However, an alternative to this is calling `useState` only once and passing an object to it that contains the user inputs to which we want to listen to.
- For example, the code below is shown. We basically want to listen to the user inputs for both `name` and `email`.
``` jsx
        <form className="w-4/5 mx-auto rounded-lg" onSubmit={formSubmitHandler}>
            <h2 className="font-bold font-serif text-4xl text-center text-dark-blue">
                Sign up for our newsletter!
            </h2>
            <div className="form-group">
                <label htmlFor="name">Name</label>
                <input type="text" id="name" onChange={nameChangeHandler} />
            </div>
            <div className="form-group">
                <label htmlFor="email">Email</label>
                <input type="text" id="email" onChange={emailChangeHandler} />
            </div>
            <button className="bg-emerald-500 text-white px-6 py-2 rounded-lg mt-5">
                Submit
            </button>
        </form>
```
- To do so, we do the code below. The passed object basically contains keys for the user inputs to which we want to listen to.
``` jsx
    const [userInput, setUserInput] = useState({
        name: "",
        email: "",
    });
```
- Then, we still create individual change handlers for the 2 inputs.
``` jsx
    const nameChangeHandler = (evt) => {
        setUserInput((prevState) => {
            return { ...prevState, name: evt.target.value };
        });
    };

    const emailChangeHandler = (evt) => {
        setUserInput((prevState) => {
            return { ...prevState, email: evt.target.value };
        });
    };
```
- As seen above, we do not simply pass a value. Instead, we pass a callback function which has a parameter `prevState` which basically contains the previous state of the passed object.
- The callback function then returns the previous state while overriding the indicated key.
- When the form is submitted, `name` and `email` can be assed from `userInput` by using the dot notation
``` jsx
    const formSubmitHandler = (evt) => {
        evt.preventDefault();
        alert("Form submitted!");
        
        //Accessing the inputted name and email
        const data = {
            enteredName: userInput.name,
            enteredEmail: userInput.email,
        };
        
        console.log(data);
    };
```





