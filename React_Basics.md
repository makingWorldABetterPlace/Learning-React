React's Basic Concepts

React has 3 simple and fundamental concepts:

1) Components : With React we describe UIs using components.
	- Like functions
	- Input: props, state | Output: UI
	- Reusable and composable(components can contain other components)
	- You don't really invoke a react component. You just use it in your HTML as if it were a regular HTML element <Component/>
	- Can manage a private state (unlike pure functions) to hold any data that may change over the lifecycle of the component
	
2) Reactive Updates: When the state of a react component (the input) changes, the user interface it represents (the output) changes as well. This change in the 
description of the UI has to be reflected in the device we are working with. In a browser we need to regenerate the html view in the DOM tree. With React we don't need
to worry about how to reflect these changes, or even manage when to take changes to the browser. React will simply react to the changes in a components state
and automatically updates the part of the DOM that need to be updated.

3) Virtual views in memory: To build HTML web applications with React, we don't write HTML at all, we use javascript to generate HTML. Here's why, When your web application
receives just the data from the server in the background with Ajax, you need more than HTML just to work with that data. You have two options: you can use an enhanced HTML 
template that has loops and conditionals or you can rely on the power of javascript itself to generate the HTML from the data. Both approaches have advantages and disadvantages. 
React uses the later one and eliminates the extra step needed to parse an enhanced HTML template. One big advantage of this HTML in javascript approach is how it enables 
react to keep and use a virtual representation of HTML views in memory, which is also known as virtual DOM or Tree reconciliation algorithm. React uses the virtual DOM to compare
the virtions of UI in memory before it acts on them.

React Components: 
  Two types: 1) Function Component 
             2) Class component
Both types can be stateful and have side effects, or they can be purely presentational. You should learn them both, but prefer to use function components over class components
because they're really much simpler. Class components, however, are a bit more powerful. Both types can be compared to regular functions when it comes to their contract. 
They use a set of props and state as their input, and they output what looks like HTML, but is really a special JavaScript syntax called JSX. The props input is an explicit one. 
It is similar to the list of attributes an HTML element can have. The state input is an internal one, but is really the more interesting one because of how React uses it to 
auto‑reflect changes in the browser.  These two input objects have one important difference. Within a component, the state object can be changed while the props object represents 
fixed values. Props are immutable. Components can only change their internal state, not their properties. This is a core idea to understand in React.

(Explicit describes something that is very clear and without vagueness or ambiguity. Implicit often functions as the opposite, referring to something that is understood, 
but not described clearly or directly, and often using implication or assumption.)

JSX is NOT HTML. It simply gets compiled to the pure JavaScript calls that you see here on the right. These React.createElement calls that you see on the right are what we ship to browsers. 
They are the JavaScript representation of this component's DOM, and they are what React can efficiently translate into actual DOM operations to be performed by the browser.
This is important to understand.


