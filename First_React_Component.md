https://jscomplete.com/playground

REPL: run, eval, print, loop that you can use to test quick JavaScript expressions.
To show more things in the display, you can use the HTML element with the ID of mountNode. You can grab a reference to this element using document.getElementById and 
specify mountNode as the ID. This is a DOM API call to select the display element.

https://jscomplete.com/playground/rgs1.1

We have a simple React function component named Hello. It returns a div. This component has no input. It's also a peer component, no state here. To display a React component
in a browser, we need to instruct the ReactDOM library on how to do that. The function designed to do that is ReactDOM.render, which takes in two arguments. The first is 
the component to render, in our case it is the Hello component. Look how I used it here as if it was just another DOM element with a self closing tag. The second argument
to the ReactDOM.render function is the DOM element in the browser where we wish the React component to show up. In this playground, we're using the mountNode display element.
If we were to do this in a regular React environment, this element has to exist in the already rendered HTML before this code. You can think of this element as the entry point
for React. We're telling React to take over this element and render all of the content within it.

How are we writing HTML inside a JavaScript function? And why is this working and not throwing an error? This is not valid JavaScript. If you copy this code and try to execute
it anywhere JavaScript can be executed, it will throw on error for sure. However, in the playground, the code works fine because the playground is equipped with a special 
JavaScript extension named JSX. That should be the gist of your answer. This line is not HTML, it is JSX. It will not be executed by the browser. It will be executed by the
JSX extension and compiled to something else, something the browser can understand. This absolutely means that what this browser is currently executing is not what you see
on the screen. The playground is using a special compiler named Babel to convert JSX into React API calls. You can see exactly what Babel is doing to our JSX, if you go to 
the Babel REPL here under try it out. Make sure this React preset is selected, and paste in here the JSX value that we're testing in the playground. Babel compiles that into
a call to the createElement function in the React top level API. That's it. That's the magic of JSX. You write what looks like HTML and Babel converts into React API calls. 
So in the good example we have here, the browser is not really executing this. Instead, it's executing the following, React.createElement, and this takes many arguments. 
The first argument is the element to be created, in this case, a div. The second argument is any attributes this element will have, the div element has no attributes. 
And the third argument is the child of that div element, in our case, it's just the string Hello React!

React has some rules here. A component name has to start with an uppercase letter, because if you don't do that, React will think you meant an HTML element. For example,
if we named our React component lowercase b button and tried to render that here, React will just render an empty button element here, and it will really not use this function
up here at all. This is a beginner mistake. Always name your components with an uppercase first letter. This rendered button here is not interactive yet. To make it so,
we'll need to introduce some state to this component. We'll use the simple and powerful React hooks to do that

JSX compiler (Babel) : https://babeljs.io/

