https://jscomplete.com/learn/react-beyond-basics

https://jscomplete.com/learn/complete-intro-modern-javascript

https://jscomplete.com/playground/scopes

https://jscomplete.com/playground/const

https://jscomplete.com/playground/why-const

ECMAScript and TC39

React developers love modern JavaScript and use most of its new features. We'll review these features in this course module, which you can totally skip if you think you're 
comfortable with the topic. JavaScript is a very different language than it used to be just a few years ago. ECMAScript, which is the official specification that JavaScript 
conforms to, has improved a lot in the past few years after a rather long period of no updates to the language at all. Today, the ECMAScript Technical Committee, which is 
known as TC39, makes yearly releases of ECMAScript, and modern browsers shortly follow by implementing the new features introduced in each year. This has started with ECMAScript
2015, or its other commonly known name, ES6. Since then, we've had yearly releases named ES plus the current year. Some of these releases were big, and others were very small, 
but the language now has a continuous update cycle that drives more innovative features and phases out the famous problems JavaScript had over the years. In this module, we'll 
go over some of the features that are usually used in React applications. This will not be a complete coverage of all the modern ECMAScript features. If you want to expand on 
this topic, check out The Complete Introduction to Modern JavaScript in the beginner collection at jsComplete.

Variables and Block Scopes

First up, let's talk about variables and block scopes. Here's one of my favorite JavaScript trick questions. Is this a valid JavaScript line of code? Testing it in the playground
seems to work fine. There are no errors, which means it's valid. So now the question is, what did it do? These are nested block scopes. We could write code in here
like var v = 42 and then access the v variable right after, and it would work fine. JavaScript does not really care about the spacing or new lines in here. A block scope is
created with a pair of curly braces, just like this example here. This also applies to if statements and for statements as well. These also get their own block scopes.
Block scopes are a bit different than function scopes, which are created for each function. You can see one difference when using the var keyword to define variables.
Variables defined with var inside a function scope are okay. They don't leak out of that scope. If you try to access them outside of that scope, you can't. As you can see here,
we cannot access the result variable that was defined inside the sum function's scope. However, when you define variables with var in a block scope, you can totally access them 
outside that scope afterward, which is a bit problematic. And here's one practical example of that. This for loop has an index variable that ticks from 1 to 10. You can access 
that variable inside the loop normally, but you can also access the same variable outside the loop. After all the iterations are done, the value of i here will be reported as 11,
which is a bit weird. This is why the more recommended way to declare variables in modern JavaScript is by using the let keyword instead of the var keyword. When defining variables
with let, we won't have this weird out of scope access problem. If we replace this var here with let and redo the same test and try to access i after that, you'll get the error
that i is not defined. This makes sense because we're outside of the scope where it was defined, so this is much better. Block scopes, like function scopes, can also be nested,
like the trick question we started with. This is a nested block scoop. Within each level, the scope will protect the variables defined in it as long as we use the let keyword
or the const keyword, which behaves in a good way like the let keyword, We use const when the reference assigned to a variable is meant to be a constant one. References assigned
with const cannot be changed. Note how I'm saying references here and not values, because defining an object with const does not make it an immutable object. It just means 
constant reference to it. We can still change that object just like we can do within functions that receive objects as arguments. If the variable defined with const is a scaler
one, like a string or an integer, you can think of it as an immutable object. Because these scaler values in JavaScript are immutable, we can't mutate the value of a string or
an integer in JavaScript. And when we use const with these scalar values, we can't change the references either. However, placing an array or object in a const is a different
story. The const will guarantee that the variable is pointing to the same array or object, but the content of the array or object can still be mutated. So be careful here, and
keep that in mind. Variables defined with const are much better than those defined with let for scaler values and functions because you get a guarantee that the value did not
accidentally change. Looking at this code example here and assuming that between the first and last line there is a big program, on the last line, if the program runs without
any errors, we can confidently say that the answer variable still holds the 42 value. For the same example with let, we would have to parse through the code to figure out if 
the answer variable still holds the 42 value. If you need a variable to hold a changing scaler value, like a counter, for example, then using let is okay. However, for most 
other cases, it's probably much better for you to stick with using const for all your variables.

https://jscomplete.com/playground/arrow-vs-regular-functions

Arrow Functions

There are many ways to define a function in JavaScript, and the modern specification introduced a new way, arrow functions. It is a way to define a function without typing 
the keyword function, but rather by using an arrow symbol like this. This shorter syntax is preferable not only because it's shorter, but also because it behaves more
predictably with closures. Let me tell you about that. An arrow function does not care who calls it, while a regular function cares very much about that. A regular function,
like X here, always binds the value for its this keyword for its caller. If it didn't have an explicit caller, the value of the this keyword will be determined by the calling
environment. In the playground here, it's the global window object. An arrow function, on the other hand, like Y here, not caring about who called it, will close over the value
of the this keyword for its scope at the time it was defined. Let me say that one more time. An arrow function will close over the value of the this keyword for its scope at 
the time it was defined. This makes it great for delayed execution cases like events and listeners because it gives easy access to the defining environment, not the calling 
environment. This is important, so let's take a look at an example. In this playground, the top‑level this keyword is associated with a special object, which has the ID of REPL.
Now, I've prepared this tester object that defines two similar functions. In both functions, I am logging the value of the this keyword to the display. Func1 is defined with 
the regular syntax, while func2 is defined with the arrrow syntax. When func1 is called, it's this keyword will be associated with its caller, which in this case, is the tester
object itself. This is why you see the printed value for the this keyword in func1 representing the tester object itself. However, when func2 is called, it's this keyword will
be associated with the same this keyword that was available in the function's scope when it was defined. It was this playground's REPL object that we've seen on the top level.
This is a big benefit when working with listeners and event handlers, and it's why you'll see me using arrow functions often. One other cool thing about arrow functions is that
if the function only has a single line that returns something, you can make it even more concise by removing the curly braces and the return keyword altogether. You can also 
remove the parentheses around the argument if the function receives a single argument, making it really short. This syntax is usually popular for functions that get passed to 
array methods, like map, reduce, and filter, and functional programming in general.

https://jscomplete.com/playground/object-literals
















































