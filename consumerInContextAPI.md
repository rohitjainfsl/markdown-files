<!-- In the React Context API, a consumer is a component that subscribes to changes in a particular context. It receives the current value of the context and will automatically re-render whenever the context value changes. Consumers are a powerful tool for passing data between components without having to explicitly pass props down the component tree. -->

<!-- Here's a simple example:

Let's say you have a component hierarchy where a child component needs to access some data from a parent component that is several levels up in the hierarchy. Instead of passing the data down through multiple props, you can use the Context API to create a context that holds the data and provide it to the child component using a consumer.

Here's some code to illustrate this: -->

import React, { createContext } from "react";

const MyContext = createContext();

function ParentComponent() {
  const data = "Hello, world!";

  return (
    <MyContext.Provider value={data}>
      <ChildComponent />
    </MyContext.Provider>
  );
}

function ChildComponent() {
  return (
    <MyContext.Consumer>
      {(data) => <p>{data}</p>}
    </MyContext.Consumer>
  );
}

<!-- In this example, ParentComponent creates a context with a value of "Hello, world!" and provides it to ChildComponent using the MyContext.Provider. ChildComponent then uses the MyContext.Consumer component to access the value of the context and render it to the screen.

Here's a more complex example: -->

<!-- Let's say you have an e-commerce application that allows users to browse and purchase products. You want to be able to share the user's cart data across different parts of the application, such as the product detail page, the cart page, and the checkout page. You can use the Context API to create a context for the user's cart data and provide it to different components using consumers.

Here's some code to illustrate this: -->

import React, { createContext, useState } from "react";

const CartContext = createContext();

function App() {
  const [cartItems, setCartItems] = useState([]);

  function addToCart(item) {
    setCartItems([...cartItems, item]);
  }

  return (
    <CartContext.Provider value={{ cartItems, addToCart }}>
      <ProductDetail />
      <Cart />
      <Checkout />
    </CartContext.Provider>
  );
}

function ProductDetail() {
  return (
    <CartContext.Consumer>
      {({ addToCart }) => (
        <button onClick={() => addToCart({ id: 1, name: "Product 1" })}>
          Add to cart
        </button>
      )}
    </CartContext.Consumer>
  );
}

function Cart() {
  return (
    <CartContext.Consumer>
      {({ cartItems }) => (
        <ul>
          {cartItems.map((item) => (
            <li key={item.id}>{item.name}</li>
          ))}
        </ul>
      )}
    </CartContext.Consumer>
  );
}

function Checkout() {
  return (
    <CartContext.Consumer>
      {({ cartItems }) => (
        <div>
          <h2>Checkout</h2>
          <p>Total items: {cartItems.length}</p>
        </div>
      )}
    </CartContext.Consumer>
  );
}

<!-- In this example, the App component creates a context for the user's cart data and provides it to three child components: ProductDetail, Cart, and Checkout. ProductDetail uses the CartContext.Consumer component to access the addToCart function from the context and add an item to the user's cart when the "Add to cart" button is clicked. `Cart -->


<!-- The use of 'useContext' hook makes the code more concise and easier to read, as we don't need to wrap our JSX in a Consumer component.
However, it's worth noting that the Consumer component can be useful in certain cases, such as when you need to render different components based on the value of the context. The Consumer component allows you to write logic inside the JSX to conditionally render different components based on the context value. -->

<!-- One example is when you want to conditionally render components based on the context value. In this case, the Consumer component allows you to write conditional logic directly inside the JSX.

Here's an example: -->

import React, { createContext } from "react";

const MyContext = createContext("default");

function ParentComponent() {
  const data = "Hello, world!";

  return (
    <MyContext.Provider value={data}>
      <ChildComponent />
    </MyContext.Provider>
  );
}

function ChildComponent() {
  return (
    <MyContext.Consumer>
      {(data) => {
        if (data === "Hello, world!") {
          return <p>{data}</p>;
        } else {
          return <p>Unknown data</p>;
        }
      }}
    </MyContext.Consumer>
  );
}


<!-- Another example where the Consumer component can be useful is when you want to pass props down to child components that use the context. The Consumer component allows you to pass props to the child components as part of the render function.

Here's an example: -->

import React, { createContext } from "react";

const MyContext = createContext("default");

function ParentComponent() {
  const data = "Hello, world!";

  return (
    <MyContext.Provider value={data}>
      <ChildComponent />
    </MyContext.Provider>
  );
}

function ChildComponent() {
  return (
    <MyContext.Consumer>
      {(data) => <GrandChildComponent data={data} />}
    </MyContext.Consumer>
  );
}

function GrandChildComponent(props) {
  return <p>{props.data}</p>;
}
