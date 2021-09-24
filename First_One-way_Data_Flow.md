https://jscomplete.com/playground/rgs1.3

https://jscomplete.com/playground/rgs1.4

https://jscomplete.com/playground/rgs1.5

In the previous video, we made a simple stateful Button component that renders an HTML button element and increments its numeric label when that button element is clicked. 
We introduced the useState React hook to manage a counter state. Let's improve this component. First, don't use long lines like this. They're hard to read. So let me format 
this return value to make it more readable. There we go. Note how I used parentheses here, not curly braces. We're not returning an object here. We're returning a function call, 
remember, a React.createElement function call. Second Improvement. Instead of an inline function here, let's create an official click handler function. This new function has to 
be defined inside the Button component because it needs access to the counter and setCounter variables. You can use any name here, but it's commonly named handleClick. We can 
just paste the code we had inline before here as the body of this function. And in the onClick attribute here, we pass a reference to handleClick. Make sure this is all good and
the button is still incriminating. So far, we've only worked with one component. Let's add more. Let's split our one Button component into two. We'll keep the Button component to
be just the incrementer, and let's add a new Display component, which is going to just display the value of the counter. This new Display component is going to be a pure 
presentational one. It will not have a state of its own. That's normal. Not every React component has to have a stateful hook. So to create a new component, we define a function
named Display, and we'll make it return some HTML element. For now, let me just put a placeholder div in here and execute. Notice that this new Display component did not show up
because I have not included it in the rendered element yet. I just defined it. Let's include it. So remember to include a component, we need to use it like that. However, 
you can't just add it here as an adjacent sibling to the Button element. This will not work. Question, why does that not work? And the answer is because each one of these elements
get translated into a function call. You have few options here to fix this problem. First, you can render an array of elements here and insert into that array as many React
elements as you wish. This will work. This is usually a good solution when all the elements you're rendering are coming from the same component in a dynamic way. It's not ideal
for the case we're doing here. The other option is to make these two React elements the children of another React element. For example, we can just enclose them in a div, create
a div element, then render the Button and the Display inside this div element. The React API supports this. In fact, React has a special object. If you need to enclose multiple
elements like this without introducing a new div parent, you can use React.Fragment. This will do exactly the same thing that the div did, but no new DOM parent will be introduced.
This case is so common in React that the JSX extension has a shortcut for it. Instead of typing React.Fragment, you can just have an empty tag. This empty tag, if supported in the
environment, will get compiled to the React.Fragment version. For the case that we're doing here, I think a div here is okay, so I'm going to keep that. Question, what can we do
to make this better? And the answer is we should really extract this code into its own component. This new component can have any name, but you can just use App here. Go ahead and
try to create this app component on your own. Make it return this DOM and use it in the ReactDOM.render call instead of what we have. We take the section, create a new function,
name it App, make this function return the exact DOM tree that we have down under. And then in here, instead of all that, we can just render the App component just like that.
Since we're going to display the counter's value in the new Display component, we no longer need to show the counter's value as the label of this button. Instead, I'm going to
change the label to just +1. Now we need to display the counter value as the message in the Display component. But we have a problem. We actually have two problems. The first 
problem is that the counter is currently a state element in the Button component, and we need to access it in the Display component, which is a sibling of the Button component
in the current tree. So this is not going to work. 

The state in a React component can be accessed only by that component itself and no one else. To make this counter state accessible to both sibling components, we need to lift
it one level up and put it in their parent component, which is the App component that we just introduced. We just move this useState line down to the App component right here.
I'll initialize the counter with a different value here to make sure things are working. The logic of this handleClick function will need to change. We will come back to that 
in a minute. Let's just comment it out for now. Now that we have the counter state element in the App compartment, which is the parent of the Display component, we can flow 
some data from the parent to the child. In this case, we need to flow the value of the counter state into the Display component, which brings us to the mighty props object. 
We haven't really used it yet, so let me tell you about it. To pass a prop to a component, you specify an attribute here, just like in HTML. You can name the props of the 
component anything you want. For example, I'll make the Display component to receive a prop named message, and the value of that message is the counter variable that's coming
from the useState hook. The Display component can now use its props object, which is the argument to the function here, and it's usually named props. You don't really have to
name it props, but that's the convention. All function components receive this object even when they have no attributes. So the Button component is currently receiving its 
props object, and that object so far has been empty. Because a component can receive many attributes, this props object will have a key value pair for each attribute. This
means to access the message prop and place its value within the display div, we do curly braces and use props.message. Let me test that real quick, and we have an error, 
handleClick is not defined because we've used it here and commented it out here. So let me just put an empty function here to get things working, and here we go. A counter 
value of 42 is now getting displayed. This is coming from the Display component. And what we did here is called the one‑way flow of data. Parent components can flow their data
down to children components.

Parent components can also flow down behavior to their children, which is what we need to do next. In the App component, since the counter state is here now, we need a function
on this level to handle updating this state. Let's name this function incrementCounter. The logic for this function is actually the exact same logic that we had before in the 
handleClick function in the Button component. So we can just move it in here. This new function is going to update the App component's counter state to increment the counter 
value using the previous counter value. The onClick handler in the Button component now has to change. We want it to execute the incrementCounter function that's in the App 
component, but a component can only access its own functions. So to make the Button component able to invoke the incrementCounter function in the App component, we can pass a 
reference to incrementCounter to the Button component as a prop. Yes, props can hold functions as well, not just data. Functions are just objects in JavaScript, and you can 
pass any object value as a prop. We can name this new prop anything. I'll name it onClickFunction and pass it a value of incrementCounter, which is the reference to the 
function we defined in the App component. We can use this new pass down behavior directly in the onClick value. It will be a prop on this component, so we can access it with
props.onClickFunction. Testing, all is good. Something very powerful is happening here. The onClickFunction property allowed the button to invoke the App component's 
incrementCounter function. It's like when we click that button, the Button component reaches out to the App component and says hey parent, go ahead and invoke that 
incrementCounter behavior now. In reality, the App component is the one in control here, and the Button component is just following generic rules. If you analyze the code as 
it is now, you'll realize how the Button component has no clue what happens when it gets clicked. It just follows the rules defined by the parent and invokes a generic onClick 
function. The parent controls what goes into that generic behavior. That's basically the concept of responsibility isolation. Each component here has certain responsibilities,
and they get to focus on that. Look at the Display component too. From its point of view, the message value is not a state. It's just a value that the App component is passing
to it. The Display component will always display that message. This is also a separation of responsibilities. As the designer of these components, you get to choose the level
of responsibilities. For example, if we want to, we can make the responsibility of displaying the counter value part of the App component itself and not use a new Display 
component for that, but I like it this way. This App component has the responsibility of managing the counter state. That's an important design decision that we made, and it
is one you're going to have to make a lot in a React application, where to define the state. And the answer is usually simple, down in a tree as close as possible to the 
children who need to access that value on the state.
