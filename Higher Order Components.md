Higher Order Components (1 example)

<!-- In React, a higher-order component is a function that takes a component as an argument and returns a new component with additional props.

HOCs are used to abstract and reuse logic that can be used across multiple components. They can be thought of as "enhancers" or "decorators" that wrap a component and add new functionality to it.

A common use case for HOCs is for adding logic related to authentication, data fetching, or state management. For example, you could create an HOC that adds an authenticated user to the props of a component, or one that fetches data from an API and passes it to a component as props. -->

<!--
import React from "react";

const withLoading = (WrappedComponent) => {
  return (props) => {
    return props.isLoading ? (
      <div>Loading...</div>
    ) : (
      <WrappedComponent {...props} />
    );
  };
};

export default withLoading;


export default withLoading; -->

<!-- This HOC takes a component WrappedComponent as an argument and returns a new component that wraps it. The new component checks if the isLoading prop is true and if so, displays a "Loading..." message, otherwise it renders WrappedComponent. -->

<!-- You can use this HOC by wrapping any component with it: -->

<!--
import React from "react";
import withLoading from "./withLoading";
const MyComponent = (props) => <div>{props.data}</div>;

export default withLoading(MyComponent); -->


<!-- EXAMPLE 1: -->

<!-- Here's a common use case for HOCs: adding authentication logic to a component.
Suppose you have a component that displays sensitive information, such as a user's personal profile, and you want to ensure that only authenticated users can view it. You could create an HOC that checks if a user is authenticated and if so, renders the profile component, otherwise it redirects the user to a login page. -->

<!-- import React from "react";
import { Redirect } from "react-router-dom";

const withAuth = (WrappedComponent) => {
  return (props) => {
    if (!localStorage.getItem("isAuthenticated")) {
      return <Redirect to="/login" />;
    }

    return <WrappedComponent {...props} />;
  };
};

export default withAuth; -->

<!-- To use this HOC, you would wrap your profile component with it:

import React from "react";
import withAuth from "./withAuth";

const Profile = (props) => <div>Profile information</div>;

export default withAuth(Profile); -->

<!-- Now, every time the profile component is rendered, it will first be passed through the withAuth HOC, which will add the authentication logic to it. -->


<!-- EXAMPLE 2: -->

<!-- Here's another example of a more advanced HOC that implements a custom theme for a component. -->
<!-- Suppose you have a component that displays content, and you want to give users the ability to switch between light and dark themes. You could create an HOC that takes a theme as a prop and sets the appropriate styles for the component. -->

<!-- import React from "react";

const withTheme = (WrappedComponent) => {
  return (props) => {
    const theme = {
      backgroundColor: props.theme === "light" ? "#fff" : "#000",
      color: props.theme === "light" ? "#000" : "#fff",
    };

    return (
      <div style={theme}>
        <WrappedComponent {...props} />
      </div>
    );
  };
};

export default withTheme; -->


<!-- import React from "react";
import withTheme from "./withTheme";

const Content = (props) => <div>Content goes here</div>;

export default withTheme(Content); -->
