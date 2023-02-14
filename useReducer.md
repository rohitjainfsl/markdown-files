<!-- The useReducer hook is a way to manage state in React, just like the useState hook. The main difference between the two is that useReducer provides a more powerful and flexible way to manage state, especially when you have complex state transitions that involve multiple state values.

useState works good when working with isolated(individual) properties, and when properties do not depend on each other.
useState is not a great choice when working with complex state properties like objects with multiple properties.
Also, useState is not a good choice when one property in that object is dependant on some other property as useState does not support multiple dependant state transitions.

The role of reducer is to take an action and apply it to a state and to return a new and updated state.

Flow: 
1. Our view dispatches an action(an instruction to do something). Action optionally can have a payload, i.e. data to be added to the state
2. The reducer function updates the current state with the action and returns the updated state.
3. Since the state is updated, the component in which it is used is re-rendered.

The useReducer hook takes two arguments: the first is a reducer function, and the second is an initial state. The reducer function is a pure function that takes the current state and an action as arguments, and returns the next state. The initial state is the initial value of the state.

Here's a simple example of how you might use the useReducer hook: -->

const initialState = { count: 0 };

function reducer(state, action) {
switch (action.type) {
case 'increment':
return { count: state.count + 1 };
case 'decrement':
return { count: state.count - 1 };
default:
return state;
}
}

function Counter() {
const [state, dispatch] = useReducer(reducer, initialState);

return (

<div>
<p>Count: {state.count}</p>
<button onClick={() => dispatch({ type: 'increment' })}>+</button>
<button onClick={() => dispatch({ type: 'decrement' })}>-</button>
</div>
);
}

<!-- In this example, the reducer function handles two types of actions: increment and decrement. When the increment action is dispatched, the reducer updates the count state value by adding 1. When the decrement action is dispatched, the reducer updates the count state value by subtracting 1.

The useReducer hook returns an array with two values: the current state and a dispatch function. You can use the dispatch function to dispatch actions to the reducer. In the example, the dispatch function is called in response to the click events on the buttons, passing the appropriate action type.

In summary, the useReducer hook is a powerful tool for managing complex state in React, and provides a way to handle state transitions in a clean and organized manner. -->

const initialState = {
firstName: '',
lastName: '',
email: '',
password: '',
isSubmitting: false,
error: null
};

function reducer(state, action) {
switch (action.type) {
case 'updateField':
return { ...state, [action.field]: action.value };
case 'submitForm':
return { ...state, isSubmitting: true, error: null };
case 'submitFormSuccess':
return { ...state, isSubmitting: false };
case 'submitFormError':
return { ...state, isSubmitting: false, error: action.error };
default:
return state;
}
}

function SignUpForm() {
const [state, dispatch] = useReducer(reducer, initialState);

const handleChange = (e) => {
dispatch({
type: 'updateField',
field: e.target.name,
value: e.target.value
});
};

const handleSubmit = (e) => {
e.preventDefault();
dispatch({ type: 'submitForm' });

<!-- simulate a server request -->

setTimeout(() => {
const random = Math.random();
if (random < 0.5) {
dispatch({ type: 'submitFormSuccess' });
} else {
dispatch({
type: 'submitFormError',
error: 'An error occurred while submitting the form'
});
}
}, 1000);

};

return (

<form onSubmit={handleSubmit}>
<input
        type="text"
        name="firstName"
        value={state.firstName}
        onChange={handleChange}
        placeholder="First name"
      />
<input
        type="text"
        name="lastName"
        value={state.lastName}
        onChange={handleChange}
        placeholder="Last name"
      />
<input
        type="email"
        name="email"
        value={state.email}
        onChange={handleChange}
        placeholder="Email"
      />
<input
        type="password"
        name="password"
        value={state.password}
        onChange={handleChange}
        placeholder="Password"
      />
<button type="submit">Sign Up</button>
{state.isSubmitting && <p>Submitting...</p>}
{state.error && <p style={{ color: 'red' }}>{state.error}</p>}
</form>
);
}
