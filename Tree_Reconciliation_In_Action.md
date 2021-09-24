https://jscomplete.com/playground/rgs1.7

https://jscomplete.com/playground/rgs1.8

You know the basics of React, and you've probably formed your initial impression about it. My initial impression was why go for all this trouble? Why use JavaScript to generate
HTML? What exactly is the value I am getting from doing all that? Let me show you that value in action. In this example, which starts at 1.7 here, we have two simple DOM nodes,
one being controlled with the native DOM web API directly using innerHTML and another being controlled with the React API, which in turn uses the DOM API. The only major 
difference between the ways we are building these two nodes in the browser is that in the HTML version, we used a string to represent the content, while in the React version,
we used pure JavaScript calls and represented the content with an object instead of a string. There's no JSX, and I will also use a regular JavaScript interval timer here to 
create some UI state so that we can do a stateful change for both versions. No matter how complicated the HTML user interface is going to get, when using React, every HTML 
element will be represented with a JavaScript object using a React.createElement call. Let's now add some more features to this simple UI. Let's add an input box that we can
type into. To nest elements in our HTML template, it is straightforward in the HTML version. We can just add an input element like this, and it will render. We can do the same
in React by adding more arguments after the third argument for React.createElement. To match what we did in the native HTML node, we can add a fourth argument here that is another
React.createElement call that renders an input element. This input element has no attributes and no children. There we go. Okay, not too bad so far. Let's add another node to both
trees. This time, let's render the current time. I have a JavaScript line here that you can use to display the current time. Just include this in both versions. Since the first
version is a template string here, if you notice these are backticks and not single quotes, so this makes the innerHTML a template string, and I can use a dollar sign syntax here
and include the JavaScript line to render the time. Let me put this value inside a pre tag just to give it some monospaced font. Test that. The time is showing up. To add the
timestamp in the React version, we add a fifth element to the top‑level div element. This new fifth element is another React.createElement call. This time it's a pre tag as we 
used in the HTML version, no attributes as well, and the new date String for content. Both the HTML and React versions are still rendering the exact same HTML in the browser. 
But as you can see, the React way is a lot more complicated than the native DOM way. So let me ask you the question again. Why go for all this trouble? What is it that React
does so well that is worth giving up the familiar HTML and having to learn a new API to write what can be simply written in HTML? The answer is not about rendering the first HTML
view. It's about what we need to do to update any existing views in the DOM. So let's do an update operation on the DOM that we have so far. Let's simply make the timestamp tick
every second. We can easily repeat a JavaScript call in the browser using the set interval web timer API. So let's put all of our DOM manipulations for both the HTML and the 
React versions into a function. I'm going to name this function render. This can be a simple arrow function just like that. And I'll copy all of this code and put it inside the
render function. We can then use this setInterval call to invoke the render function every second. So this should work now. When we refresh the display area, the timestamp string
should be ticking every second in both versions. We are now updating our user interface in the DOM, and this is the moment when React will potentially blow your mind. If you try
to type something in the text box of the HTML version, you will not be able to. This is very much expected because we are basically throwing away the whole DOM node on every tick
and regenerating it. However, if you try to type something in the text box that is rendered with React, you can certainly do that. Although the whole React rendering code is 
within our ticking timer, React is changing only the timestamp text and not the whole DOM node. This is why the text input was not regenerated and we were able to type in it.
You can see the different ways we are updating the DOM visually if you inspect the two DOM nodes in the Chrome DevTools elements panel. The Chrome DevTools highlight any DOM 
elements that get updated. You will see how we are regenerating the entire first mountNode element with every tick, while React is smartly only regenerating the content of the 
pre element in the second mountNode. This is React's smart diffing algorithm in action. It only regenerates in its DOM node what actually needs to be regenerated, while it keeps 
everything else the same. This diffing process is possible because of React's virtual DOM and the fact that we have a representation of our user interface in memory because we 
wrote it in JavaScript. For every tick in this example, React keeps the last UI version in memory, and when it has a new one to take to the browser, that new UI version 
will also be in memory. So React can compute the difference between the new and the old versions. In this example, the difference was the content of the pre element. React
will then instruct the browser to update only the computed diff and not the whole DOM node. No matter how many times we regenerate our interface, React will take to the
browser only the new partial updates. Note that the HTML version can be easily changed with a few more lines to make it update only the content of the pre element as well
instead of the whole thing. But that requires some imperative programming. We'll first have to find the element that needs changing in the DOM tree and add some more imperative
logic to change its content. We are not doing that in React. We're being declarative in React. We just told React that we'd like a pre element with the date string. No 
imperative logic is here, and yet we're still getting the efficiency of a tuned‑up imperative alternative. This is the subtle power here. The React way is not only a lot more
efficient, but it also removes a big layer of complexity about the way we think about updating user interfaces. Having React do all the computations about whether we should or
should not update the DOM enables us to focus on thinking about our data and state and the way to model that state. We then only manage the updates that's needed on the state 
without worrying about the steps needed to reflect these updates in the actual user interface in the browser because we know React will do exactly that for us, and it will do
it in an efficient way.

Wrap Up

A React application is a set of reusable components. Components are just like functions. They take input and they output a description of a user interface in the form of a React
element. The ReactDOM library enables us to render those React elements in the browser, and it will rerender them for us automatically when their in‑memory state changes. 
To accomplish this, we write the component's markup using the React JavaScript API. Writing HTML in JavaScript is a lot different than what we're used to. But luckily, 
React has a way to write the virtual DOM in a syntax very close to the HTML syntax we're used to. This special React syntax is called JSX. Once we have the virtual DOM 
description in JSX, we can pre‑transform it to valid React API calls before shipping it to the browser. Browsers do not have to deal with JSX. The input for a component is a 
set of properties you can access inside the component with its first argument object, which is usually named props, and also a set of state elements that a component can hook 
into with the special useState function. A component state can be changed inside that component, and every time a component changes its state, React rerenders it. The props of
a component cannot be changed by the component, but the whole component can be rerendered with different props by the component's parent. The syntax to mount a React component
in the browser is ReactDOM.render, and that takes two arguments, the component to render and the HTML element to hold the React‑rendered markup. React also comes with normalized
events that work across all browsers in a standard way. We've seen the onClickEvent handler in this course module, and there are other onSomething events like onChange and 
onSubmit, and many others. React actually has two types of components, function and class components. We've only seen function components, but I'll be covering class components 
in future videos as well. However, before we start another application on React, let's get you comfortable with all the modern JavaScript syntax that's usually used in the React
ecosystem. That's our next course module.
