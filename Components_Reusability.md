https://jscomplete.com/playground/rgs1.6

One of the selling points about components is reusability, making a component generic enough so that we can reuse it in different cases. Let's do that. Let's make the Button
component more generic. Let's assume that we can pass in an increment value here, and the Button component will use that value instead of the hard coded one. So we'll use the 
more generic Button component to create a +1 button, a +5 button, and so on. We need to upgrade this +1 here to something dynamic. It will be a property of the component, the 
amount to increment, and we'll pass it down from the parent. Let's name this new attributes increment, and the value we need to pass here is a number. Since the value here is 
not a string, we'll need to use a set of curly braces here as well. So, for example, we can pass in 5. One quick note about this syntax here. We could pass the number like this,
but the Button component in this case will see and work with that value as a string. So don't do that. Keep it this way so the Button component receives it as a numeric value, 
not a string. To use this new increment prop, we can just access it here as props.increment. There we go. We've got a +5. So let me go ahead and add a few more buttons here and
use increment values of 1, 5, 10, and 100. Let's initialize this back to 0. And there we go. The UI rendered four buttons now with different labels, but they're not going to work
yet. In fact, all of them would still increment with a +1 at this point because we did not change their handlers. So the challenge now is to make each button increment the 
globally displayed counter by its increment value, not just 1. Do you think you can do that on your own? Give it a try. I saved the code as of now for you under 1.5 here. 
Here's how I'd solve this challenge. This incrementCounter function here will now need to receive an increment value, and we can use its argument to do that. So receive 
incrementValue in here, and instead of using +1 we'll use the new incrementValue. Now we can invoke the incrementCounter function with different values. The incrementCounter
function is aliased as onClickFunction for the button. So the Button component needs to invoke the onClick function with an argument now, which is its own increment value, and
that can be accessed using props.increment. But we can't just pass the argument here like this, because remember, we need a function reference for the onClickEvent handler, and 
what I have on the screen right now is not a reference. It's an invocation of a function. This will not work. But we can simply wrap this invocation in an inline function to make
it into a reference, and through the magic of JavaScript closures, this will work just fine. But again, it's a bit cleaner to do this logic inside the handleClick local function
here. So let me go back to handleClick and put this new logic inside handleClick, just like that. Make sure this is still working, and all is good. This is the final code of this
example, and I saved it here under 1.6 for you. Through this example, we've touched on the many basic React concepts, but this is still a relatively simple example. Let's build
something a bit more useful next. But first, I need you to absolutely understand the value you're getting from using React's tree reconciliation under the hood That's the next
video.
