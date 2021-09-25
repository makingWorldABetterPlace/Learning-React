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

Object Literals

You can create a JavaScript object in a few different ways, but the most common way is to use an object literal. Here's an example of that. This is a lot easier than doing something like new object, which you can do if you want to. Literal initiation is very common in JavaScript. We use it for objects, arrays, strings, numbers, and even things like regular expressions. The object literal syntax supports a few modern goodies. Here's a simple example where this object defined two regular properties. If you need to define a property that holds a function, you can use this short syntax with object liberals. Of course, if you need an arrow function, you can still use this regular property syntax. Modern object literals also support dynamic properties using this syntax. It looks like an array literal, but don't confuse it with that. JavaScript will evaluate what's within the square brackets and make the result of that the new property name. So, assuming we have a variable named mystery defined before this X object, here's a JavaScript interview question. What is the value of obj.mystery? It's undefined because this mystery property was defined with a dynamic property syntax. This means JavaScript will evaluate the mystery expression first, and whatever that expression evaluates to will become the object's property. For this case, the object will have a property named answer with the value of 42. Another widely popular feature about object liberals is available to you when you need to define an object with property names to map values that exist in the current scope with the exact same name. Here's an example. If we have a variable named InverseOfPI, we would like obj here to have a property named InverseOfPI holding the same value as the variable InverseOfPI. Instead of typing that name twice, you can use the shorter syntax by removing the second part. This shorter syntax is equivalent to what I had before. Objects are very popular in JavaScript. They are used to manage and communicate data, and using these features will make the code a bit shorter and easier to read.

https://jscomplete.com/playground/destructuring

Destructuring and Rest/Spread

The destructuring syntax is really simple, but I've seen it confuse many people before. Let me make sure that does not happen to you. Destructuring works for both arrays and objects. Here's an example for objects using the built‑in Math object in JavaScript. When you have an object like Math, and you want to extract values out of this object into the enclosing scope, for example, instead of using Math.PI, you'd like to have a constant named PI to hold the value of Math.PI, which is easy because you can have a line like this for PI and another one for E if you need the same for E and so on. With the destructuring syntax, these three lines are equivalent to this single line. It destructures the three properties out of its right‑hand object and into the current scope. This is useful when you need to use a few properties out of a bigger object. For example, here's a line to destructure Component, Fragment, and useState out of the React API. After this line, I can use the useState method directly like this. If I don't use destructuring here, I'll have to type a lot more characters and lines. Destructuring also works inside function arguments. If the argument passed to a function is an object, instead of using the name of the object every time you want to access its properties, you can use the destructuring syntax within the function parentheses to destructure just the properties that you're interested in and make them local to that function. This generally improves the readability of functions, and you'll see it used a lot for the props argument in React function components. So here we have a circleArea function, which expects an object as its argument, and it expects that object to have a radius property. We're destructuring the radius property out of that object and using it locally in the function. If we call this circleArea function with an object like circle here, it will use its radius property inside of its calculation. Let's go ahead and test that. You'll see the circleArea calculation working as expected. Destructured arguments can also be defined with defaults, like regular arguments. Say I'd like to use a default value of 2 for a precision property here. Let's define a second options argument for this circleArea function here, and lets destructure our precisions out of that argument to use it in the function's body. If I'd like to use a default value of 2 for the precision property, I can just use the equal sign here after destructuring precision, and that means the default for precision, if not specified, will be 2. I can also make this whole second argument optional using an equal sign after the destructuring syntax. The same call here will use an empty object for the second argument of the function, and then it will use a default value of 2 for the precision property that is now used in the function. Of course, if we invoke the circleArea function with a second argument that has the precision property, that value will be used inside the function. As you can see, this destructuring feature offers a good alternative to using named arguments in functions, which is much better than relying on positional arguments. Destructuring, whether you do it in function arguments or directly with variables, also works for arrays. If you have an array of values and you want to extract these values into local variables, you can use the item's positions to destructure their values into local variables just like this. Note how I used double commas here to skip destructuring the third item in the array. The destructured variable fourth here will hold the value of 40. In React, the useState function returns an array of two items. We use array destructuring with useState to capture these two items into local variables. Array destructuring is useful when combined with the rest operator, which has an example here. By using these three dots, we are asking JavaScript to destructure only one item out of this array and then create a new array under the name restOfItems to hold the rest of the items after removing the first one. Let's test that. So first, here will be 10, and rest of items will be an array of 20, 30, and 40. This is powerful for splitting the array, and it's also even more powerful when working with objects to filter out certain properties from an object. Here's an example of that. Say that we have this data object that has a few temp properties, and we'd like to create a new object that has the same data except for temp1 and temp2. We can destructure temp1 and temp2 and then use the rest operator to get the remaining properties into a new object called person. Just like the three dots of rest, you can use the three dots to spread one array or object into a new array or object. This is useful for copying arrays and objects. You can spread the items in an array into a new array, like in this example. NewArray here will be a copy of the restOfItems array that we destructured above. Similarly, you can also spread the key‑value pairs of an object into a new object, like this example. The newObject here will be a copy of the person object. Note that these copies are shallow copies. Any nested objects or arrays will be shared between these copies. Don't forget that.

https://jscomplete.com/playground/template-strings

Template Strings

Template strings are one of my favorite new features that were introduced to the JavaScript language a few years ago. Let me tell you about them. You can define strings in JavaScript using either single quotes or double quotes. These two ways to define string literals in JavaScript are equivalent. Modern JavaScript has a third way to define strings, and that's using the backtick character. Strings defined with the backtick character are called template strings because they can be used as a template with dynamic values. They support what we call interpolation. You can inject any dynamic expression in JavaScript within these dollar sign curly braces holders. For example, we can use Math.random here, and the final string will have the value of the expression included exactly where it was injected in the string. With template strings, you can also have multiple lines in the string, something that was not possible with the regular quoted strings. Backticks look very similar to single quotes, so make sure to train your eyes to spot template strings when they are used in examples.

https://jscomplete.com/playground/classes

Classes

JavaScript offers many programming paradigms, and object‑oriented programming is one of them. Everything in JavaScript is an object, including functions. Modern JavaScript also added support for the class syntax. A class is a template or blueprint for you to define shared structure and behavior between similar objects. You can define new classes, make them extend other classes, and instantiate objects out of them using the new keyword, You can customize the construction of every object and define shared functions between these objects. Here's a standard class example that demonstrate all these features. We have a Person class and a Student class that extends the Person class. Every student is also a person. Both classes define a constructor function. The constructor function is a special one that gets called every time we instantiate an object out of the class, which we do using the new keyword, as you can see here. We are instantiating one object from the Person class and two other objects from the Student class. The arguments we pass here when we instantiate these objects are accessible in the constructor function of the class. The Person class expects a name argument, and it stores that value on the instance using the this keyword here. The Student class expects a name argument and the level argument. It stores the level value on its instance, and since it extends the Person class, it will call the super method with the name argument, which will invoke the Person class constructor function and store the name as well. Both classes defined a greet function that uses the values they store on each instance. In the third object, which we instantiated from the Student class here, I also defined a greet function directly on the object. When we test this script, o1 will ease the greet method from its class, the Person class, o2 will use the great method from the Student class, and o3 will use its own directly defined greet method. 

https://jscomplete.com/playground/promises

Promises and Async/Await

When you need to work with asynchronous operations, usually have to deal with promise objects. A promise is an object that might deliver data at a later point in the program. An example of an async function that returns a promise is the web fetch API that's natively available in some browsers. Here we're fetching information from the top‑level GitHub API. Since fetch returns a promise, to consume that promise, we do at .then call on the result of fetch and supply a callback function in here. This callback function will receive the data from the API. The fetch API has a raw response. If you need to parse the data as JSON, you need to call the json method on the response object, and that json method is also on asynchronous one, so it returns a promise as well. To get the data, we need another .then call on the result of the json method, and in the callback of that, we can access the data. As you can see, this syntax might get complicated with more nesting of asynchronous operations or when we need to combine this with any looping logic. You can simplify the nesting here by making each promise callback return the promise object, but the whole .then syntax is a bit less readable than the modern way to consume promises in JavaScript, which is using async await. Let me show you that. You just await on the asynchronous call that returns a promise, and that will give you back the response object. Then you can await on the json method to access the JSON data, just like this. And to make these await calls, you need to label the function as async, and this will work exactly the same. The async await syntax is just a way for us to consume promises without having to nest .then calls. It's a bit simpler to read, but keep in mind that once you await on anything in a function like fetchData here, this function itself becomes asynchronous, and it will return a promise object.

https://jscomplete.com/learn/lab-functions-scopes

https://jscomplete.com/learn/lab-functions-args

https://jscomplete.com/learn/lab-hofs

https://jscomplete.com/learn/lab-closures




































