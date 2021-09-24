https://jscomplete.com/playground/rgs1.2

Our component currently renders a stateless button. We now need to make the button increment a counter every time it's clicked. We need a state object. To use a state object,
react has a special function named useState. This is also globally available here in the playground. So we're going to be invoking this function. This useState function is 
going to return two items for us. The first item is a state object, and the second item is a function to change that state object. The state object can be of any time you wish
it to be. It could be a string, a number, or an array, or anything else. For this use case, we need it to be a number. I'm going to name this state object counter and name its
updater function setCounter. The syntax you need here might look a bit weird, but since JavaScript functions can only return a single value, the useState function returns an
array with exactly the two elements here. To make this work, we need a variable‑defining keyword before this syntax. I'm going to use const. This special syntax here is using 
JavaScript destructuring feature to capture these two variables in one line. It's not magic or anything; useState returns an array with two elements, and in here we're 
destructuring these two elements into variables in our Button component. The argument to useState is the initial value for the state element, counter in our case. Since we
want that counter to be a number, we'll set that to 0. To use the two new variables that we introduced, let me tell you a nice little thing about JSX. It supports displaying 
dynamic expressions if you place them within curly braces anywhere inside JSX. So if I make the button's label into curly braces, and inside these curly braces put any JavaScript
expression I want, I'll use Math.random, and execute the code, the button will have random value every time I render this component. So to use this new state element, all we have
to do is put the counter variable within curly braces and make that the label of the button element. The button will now be rendered with a label of 0. This is the same 0 that's
coming from the initial value we specified for useState. So any value initialized here will show up as the button's label, but we'll keep it as 0. Now to use the setCounter
updater function, every time we click on this button, we need to introduce an event handler. This is going to look similar to the way we can do this with the DOM API. We define an
onClick attribute on the button element. This onClick attribute is also case sensitive. It has to be camelCase like this. And unlike the DOM version of the onClick, which
receives a string, this react onClick attribute receives a function reference. So you always specify that inside curly braces as well. In here, we're going to specify a
function reference. Let me create a dummy function here, function. I'm going to name it logRandom, and we'll make this function console.log(Math.random). Very simple. To use this
function as the onClick event handler, we pass in here the functions reference, its name, just like this. To see the console.log messages, we need to bring up the browser's 
console here. And after executing this code, every time I now click on that button, the console will print a random value. Note that when we passed in the logRandom function here,
we did not invoke the function. This will not work. You just need to pass in the pointer to the function. You can also inline the function definition right here inside the curly
braces. So, basically, you paste in the function definition, and this will work as well. We can make this more concise by using the new arrow function syntax, which can fit in a
single line here, () =>, and then the body of the function directly after that. This highlighted part is an inline arrow function definition. We're not invoking the function here.
We're defining it and passing this new reference to the onClick prop. This will work as well. So now that we saw how to wire an onClick event, what we need to do to make the 
counter count is to use the setCounter updater function that we got from useState. So instead of console logging a random value here, I'm going to use setCounter, invoke that
function, and the argument to setCounter will become the new value of counter here. So if we pass in counter+1 as the argument just like this and execute this code, then every 
time the onClick event is triggered now, the counter will be incremented, and you'll see the button behaving as we wanted it to. This useState function is called a hook in the 
react world. It is similar to a mix‑in or a module, but it is a stateful one that hooks this simple component into a state. What I need you to notice here is that to reflect the
new value of the counter variable in the browser here, we did nothing. We just managed the state of the counter value. React is automatically updating the browser for us thanks 
to its reactive nature. We did not implement any transactions on this UI. We implemented the transactions on a JavaScript counter object in memory. Our UI implementation was 
basically telling React that we want the label of the button to always reflect the value of that counter object. We didn't do any DOM updates. React did. You're going to need 
a few more examples to appreciate this power.
