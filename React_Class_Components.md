https://jscomplete.com/playground/rgs2.1

https://jscomplete.com/playground/rgs2.2

The first decision you need to make in a React application is the component structure. You need to decide how many components to use and what each component should describe. 
This is often easy if you have the full picture of the application you're building, but practically you don't. I usually start with what makes sense for me at the beginning and
keep an open mind about it while making progress. I rename components a lot, and sometimes I remove them if I find no reason for them to stick around. There isn't a right or wrong
answer here, but there are good and better answers, and you'll only get better with experience. So just start with something, and see where that takes you. Our application will 
eventually be a list of GitHub cards. That's your first clue that you need a component to represent a single card and another component to represent the list itself. You can start
coding either one of these components. I like to start from the bottom up or from the deepest point in the tree, but it's sometimes useful to start with a top to bottom approach, 
especially when you know most of the components in the tree. Before we introduce new components, let's learn how to use the class syntax for components. Let's start by converting
this App function component into a class one. This is simple. Instead of a function component, you define a class with the same name and make it extend a special class in React, 
the React.Component class. Uppercase component here. This extending of React.Component makes your App JavaScript class an official React component. And just like function
components, class components also map data to view. They do that using a few concepts related to class components. We're going to learn about two main concepts in this example, 
the concept of the constructor and the concept of the this keyword in classes. I'll explain them as we need them, but for now, you need to know that each React component must 
have a render function. A class can have as many functions as needed, but the render function in a React component is the only function that's required. You make the render 
function return the virtual DOM description of your component. This is the same as what the original function component returned, so we can return it here as is. However, instead
of receiving props as arguments, in class components, both the props and the state are managed on an instance of the class. Now that we're using a class, we are creating instances
of them, and each instance gets its props and state. So this title prop here needs to become this.props.title, and this will just work. Let me do some cleanups, and now we have an
App class component.

 Let's now create the card component, so class Card extends React.Component, render function, and a return, and let's make it return a div placeholder. I'm going to give it a
 class of github‑profile. Let me put it on multi lines and put a placeholder. And to render this card component, we need to include it in the App component that gets rendered in
 the DOM. So do the same here, multi line, top‑level div container. I'll put the header that we had before, and we'll render a Card component. Using a class component is exactly
 the same as using a function component. There's no difference here. There we go. The Card component is showing up on the screen. I've prepared some markup for this Card, so we're
 just going to use it. This uses an img placeholder and simple div for information that contains the name and the company. Note how I've given many elements class names here. 
 These class names, for me personally, make the code a little bit more readable. But it's also handy for us to quickly reference them in CSS style sheets and give them some styles.
 And this is exactly what I did here in the CSS style sheet. I've added some styling using the class names that I used in the markup. I saved the code we have so far here under 
 rgs2.2.
 
 https://jscomplete.com/playground/react-style
 
 https://github.com/MicheleBertoli/css-in-js
 
 Styling React Components
 
Before we get into working with data, let me tell you a bit about an alternative way to style your React components without using a global CSS style sheet. Let me actually 
scratch the global CSS sheet and lose all the styling for what we have so far. Now with this alternatively to style React components, you don't really need to have a className
in here, so you can actually get rid of all these classNames if you want to. Instead, you pass a style property. Now, this is a special React property. It is not like the HTML
style property that's usually frowned upon. Just like events, instead of passing a string, we pass this special React property, a JavaScript object. So we use curly braces for
a dynamic value, and then we use another set of curly braces to start an object literal. This is not a special double curly brace syntax. This is just an object literal inside
the normal JSX dynamic expression syntax that we do with curly braces. Inside the style object we can specify any styles we want this element to have using the JavaScript API 
for styles. For example, if I want to give this GitHub profile card some margin, I can use margin and put the value in here in a string. So this would be 1rem, for example. 
Similarly, here is an example style to give the info class a display of inline‑block and a marginLeft of 10 pixels. Let's also give the name here a bigger fontSize and test all
that. Note the syntax here. It's all JavaScript. It's camel case for property names and it's strings for values. It is not the same as what you use in the regular CSS. Now, 
there is a lot of debate around this method. It feels like using inline styles, and some people call it that, but it's quite different, the difference being this is JavaScript,
not strings. We can generate it and reuse it, and we have the complete power of JavaScript to do that. We can use conditional styles here without having to deal with conditional
class names, which is usually a better deal. But this method also has its disadvantages. I often use a mix of JavaScript styles and global styles in my projects. JavaScript 
styles are excellent for conditional styling. Instead of using different class names based on a certain condition, with JavaScript styles, you can just output different objects,
which, I think it's a bit cleaner. Here is a non‑related example about that specific use case. This component will output its text in either green or red colors randomly about 
half the time. The logic for that is right here in the component. I like that. This is easier to work with than conditionally using a class name and then go track what that 
class name is doing in the global CSS style sheet. I'm pretty sure we're going to need to use this in some styles in the upcoming examples, so keep this in mind. The styling
methods we talked about here are really the most basic ones. They sure have a lot of limits and challenges. To mention one example, it would be a big challenge to implement 
media queries with JavaScript style objects. The good news is there are a lot more solutions that offer more powerful ways. You can see a good list of the available options in
this GitHub repository here. Some of these options are deprecated, so don't let this long list scare you. You can find the popular options here, judging by the number of stars,
but you should really take a look at CSS modules, which has a few options here. But this babel‑plugin‑css‑in‑js one is probably a good starting point. There's also React Native
for Web, which would make sense if you're planning to use React Native as well.

https://jscomplete.com/playground/rgs2.3

https://api.github.com/users/makingWorldABetterPlace

https://jscomplete.com/playground/rgs2.4

Working with Data

Under the rgs2.3 link here, I added a temporary testData array for us to work with. This data was copied from the GitHub API so that once we're done testing our app with this
fake test data, it will just work with the real API data. The URL I used to copy the GitHub data is api.github.com/users , and then you put any GitHub user name, and you'll see
their data as a JSON object. Since we want to render multiple cards, we need another component to hold the different cards. We'll name this new component CardList. We can 
potentially manage the state of the application in this CardList component, but until we make that decision, we'll keep this component simple. I am going to actually write this
component as a function component, just for you to be comfortable mixing these two components styles together. Not all components in the same React application have to be one 
type or the other. The CardList function component will receive the standard props argument and let's make it return a div that will hold our list of cards. So inside this div 
we'll render a Card component, just like that, and we'll need to change the app component to render the CardList instead of the Card. Make sure things are still working. Now 
let's put some real data in the Card component. We'll use the testData array for that. So we need to uncomment this part to make the test data available in the scope. And inside
the render function for the Card component, I'm going to create a local variable here, call it profile, and grab the first element of the test data array. Now we need to change 
the place holder data here with dynamic values from the profile variable. So we need curly braces, and for the image we're going to use profile.avatar_url. For the name, we need
profile.name. And for the company name, we need profile.company. Let's test that. There we go. Dan's profile information is ready. Now that we have an idea how a card is going 
to look like, let's make it reusable. If we want to render multiple cards right now, they will all render Dan's information because we are fetching the same profile in the Card 
component itself. So instead of doing this, we'll make the Card component receive its data through its props. So, for example, it will receive name property, like this, and a 
company property, and so on. One way of doing that is to take the object that holds the props and spread it inside the Card component element, like this. When we use the spread
operator with an object like this in the React component, all the properties of that object will become props for this component. So let me spread two objects here to test, 
we'll spread 0 and 1. And to make this work in the Card component, the profile variable becomes this.props. Capture all the props coming for the Card component as a profile 
object, and we're already using that for data. Let's test. There we go, progress. The this keyword in here refers to an instance of the Card component. That's something that 
you need to understand. A beginner question here might be, what exactly is an instance? I mean, you probably know that objects can be instantiated from classes, and we call 
every object an instance. But what is an instance in a React application? Well, every time we use a class component, like we're doing here twice, React internally creates an 
instance from the component and uses it to render the element. That instance is something that React keeps in memory for each rendered element. It's not really in the browser. 
What's in the browser is the result of the DOM operation React came up with using that instance render method, which came from the component. Don't worry if you don't completely
understand that. What you need to keep in mind for now is that each time we use a component, we get a different instance to work with. So the this keyword in the first card is
different from the this keyword in the second card. And that's why React places the different props for each card on their different instance. And by using generic props in the
Card component, we made it reusable. This means we can now use it to render any card, but we're still hard coding values in the CardList component. So let's fix that. And what 
we need here is to take an array of objects, as in the testData array in here, and map it into an array of card elements. So in here, instead of the hard coded cards, we can 
start with testData. This testData is an array, so we can map it into another array. This gives us access to a single profile object in the array of profiles. We can map that 
into a Card element just like this. And as props for this mapped Card element, we can spread the profile variable that was exposed from the map, and we don't need the hard 
coded values, and this should work. This line here is a mix of JavaScript and React. This map function here is a JavaScript function that you can invoke on arrays. It takes a 
function as an argument, and then it uses this function to convert one array into another array, using the return values in the function. So this map line is converting the 
testData object into something like this, an array of Cards elements because it's returning the Card element inside its function. And an array of Card elements is just an array
of React.create element calls, and React is okay with that, React understands arrays. It will just join the array of Card components on automatically render them all. Now that 
we have a tested card, we can build the form for the user to type in a GitHub user name, query the GitHub API for that user name's data, and append it in the array of data that
this app is using. We'll do that next.

https://jscomplete.com/playground/rgs2.5

Initializing and Reading the State Object

To eventually take input from the user, we can use a simple HTML form with an input and a button. Let's create a new React component. I'm going to call it Form, and this needs
to extend React.Component. It needs a render function, and it needs to return some kind of DOM. I'll make it return a form HTML element. And in there, let's use an input 
element, give it a placeholder, something like GitHub username. And we'll render a button to Add new card. Very simple. To make this component show up in the browser, we need
to include it somewhere in what we're rendering, and it can be included in many places. For example, I can put it inside the CardList component, render the Form component, and
it will show up. But that would be completely wrong to do. This Form component is not part of a card listing logic. Every component has its own separate responsibility. 
The CardList component renders a list of cards, and the Form component renders an input form. So we should not mix them together. It would be so much better to render the Form
component in the top‑level App component as a sibling to the CardList component. The App component will handle the connection between the CardList component and the Form 
component. Testing that, both components now show up, and we did not mix their logic. The data array driving the code we have so far is still a global variable, which is not
a good thing. Your component should avoid reading global variables. This is a test data object though, so it is a temporary thing that we're going to get rid of. But instead
of reading it directly from the CardList component, let's make it part of the App component and make the CardList component receive it as a prop. I'll name this prop profiles
and initialize it from the testData. Now in the CardList component, instead of testData directly here, we need to use props.profiles because it's now a property that's coming
from the parent, and this CardList component is no longer depending on anything global. Remember, always test your changes as soon as you can. Now, since we want React to 
re‑render the CardList component every time a new record is added to this profile's array, the easiest way to trigger this re‑render is to place the profiles array on the 
special state object. After that, all we need to do is just add a new record to the array and React will react and reflect the new change in the UI. The question is which 
component should hold this new state? So far, the profiles array is only used by the CardList component. So we can manage the state of the profiles in the CardList component
itself. But remember that the Form component will need to append a record to this profiles array, and it can't do that if the owner of the array is its sibling, the CardList
component. To allow both the CardList and the Form component to access the profiles array, we should put it on the state of the top‑level App component itself. In a class 
component, the state is also managed on the in‑memory instance that React associates with every mounted component. To initialize a state object for the App component, we need
to tap into the native class constructor method, which gets called for every instantiated object. This special constructor method receives the instance props as well. It has 
to call the JavaScript super method. This is a JavaScript thing. This super method is needed to honor the link between the App class and the class that it extends from, 
React.Component. And React will complain if you don't do that. You should also pass the props object to the super method. Once inside the constructor, we have access to the
special state object that React manages for each class component. We can initialize it here by using a call to this.state = and put an object here. Unlike useState in function
components, this state instance property has to be an object in class components. It can't be a string or an integer, for example. Now we can place the profiles array directly
within this object. So this is going to start as an empty array eventually. But we're testing with our testData, so let's just place testData in here. To read this new state 
element, because the CardList component needs it, we can flow it down using this.state.profiles. State is an object on the instance, and the profiles array is a property on 
that object. Test and make sure we did not break anything. Before we move on, let me show you a simpler and shorter syntax for this extra code that we have to deal with. 
Instead of all this, we can simply use a class field like this without a constructor call. So this is definitely so much simpler than dealing with a constructor object. 
This is not yet part of the official JavaScript language, but it is going to be. The syntax works in here because the JS complete playground uses Babel to transpile things to
normal JavaScript that the browser will understand. This class field syntax also has some power when combined with arrow functions as we'll shortly see. When you configure your
own React application, you'll have to use something like Babel anyway to compile JSX into JavaScript. So it's a big, easy win to also include and use the JavaScript features 
that are well on their way to become an official part of the language. So I'm just going to keep this syntax. Let's implement the logic of the Form component next. We need to
read the value of the text box every time we click on the ad button. Simple, right? Except when we type into this text box, we're changing the state of the UI as well, and 
it is currently being changed natively, not through React.

https://jscomplete.com/playground/rgs2.6

Taking Input from the User

To take input from the user, we need to define an event handler in the React UI. We can define an onClick event here on the Add card button, but I prefer to handle this with an
onSubmit event for the HTML form element itself. By using onSubmit, you can utilize native form submission features. For example, you can make this input required, and the
onSubmit event will honor that in modern browsers. Let's define an instance function here on the form component. I'm going to use the exact same class field syntax that we used
for the state in the app component. Let's call this new function handleSubmit, and we'll make it an arrow function and wire it to be triggered onSubmit. So in here we do
this.handleSubmit. Every React event function receives an event argument. You can name this anything; it doesn't have to be event. This is just the last argument that the 
function receives. And for React events, this argument is just a wrapper around the native JavaScript event object. All the methods available on the native event object are also
available here. For example, since we want to take over the HTML submit logic, we should prevent the default form submission behavior here using event.preventDefault. This is 
important when you're working with forms because without preventing default, if you submit the form, your page is going to refresh. So just be aware of that. Now, to read the 
value that the user types in this box, we can simply use the DOM API. We can give the input here an ID attribute and use getElementById to read its value. React has a special 
property named ref that we can use to get a reference to this element. This is kind of like a fancy ID that React keeps in‑memory and associates with every rendered element. 
To use a ref, you need to instantiate an object here. You can name it anything. I'll name it userNameInput, and we do a React.createRef call in here. And to use this ref, 
since it is part of the instance now, we can just do this.userNameInput, just like that. And here it is on multiple lines. We added ref this.userNameInput, which is the result
of calling the createRef method from the React API. Now, inside the handleSubmit, let's console.log the value. The value is we grab the reference using this.userNameInput, 
and this is a ref object. The current value is stored under .current, and this .current reference is the HTML input element itself, so we can do .value on it to read the value
that the user types. Let's test. Type in something, submit, and we can read the value that I typed. So this is how we use refs. But React has another method to work with this 
input element, which is to control their values directly through React itself, rather than reading it from the DOM elements. This method is often labeled as controlled 
components, and it has some more advantages over the simple ref property. However, it does require a little bit more code, but it's still simple, so let's use it. So I'll 
remove this ref attribute. We will not be able to read it this way. We're going to have to find another way to read it. And we don't need the ref attribute on the input element
at all. Instead of all that, we introduce a state object, and in the state object, we define an element to handle the input value of the userName field, so maybe something like
userName. And we'll initialize it as an empty string. Then, we use this new state element as the value of the input element. So we do value= this.state.userName. And this 
immediately creates a controlled element. Now, we're controlling the value of the input. However, once you do that, you can't really type in this field anymore because 
React is now controlling the value. This is why you need an onChange event so that the DOM can tell React that something has changed in this input and you should reflect it in
the UI as well. And I'm going to use an inline function here for the onChange event. This function receives the event object as its argument, and it needs to do one simple 
thing. It needs to change the value of the userName state element into what was typed in the text box. To do that, in the class component we use this.setState and pass it an
object that has the new state. In this case, we need to pass it to userName is and in here grab the value that the user typed directly from the DOM. So we can do that using 
event.target.value. So this is the syntax that we need to use in order to change the state of a class component. It's a little bit different than function component hooks 
because this function is always named setState and it always receives an object, and it will merge this object with the current state of the component. So now, if we've done
everything correctly, we can access the value that the user types using this.state.userName directly, like this. Let's test that. And there we go. So basically, the onChange
event happened on every character that we typed here, and it made React aware of this element state change and React reflected the change back to the element itself because 
it's a regular React state change. So what exactly is the benefit of doing all this instead of just a simple ref? Well, you can see that clearly if you open the dev tools and
find this input element, right here it's on the form component, and observe as you type something here, you'll see how React is aware of this state change for every single 
character, while previously React was not aware of what was being typed in the input box. So this method is valuable if you need to provide some kind of feedback for the user
as the user is typing. One example of that would be a password strength indicator or the count of characters as the user is typing, as in Twitter's Tweet form. Because now that
this whole state is in React, we can add a UI description on it as well. And we don't need to read the value from the DOM, it's in React's memory. So that's simply the story of
controlling a component to force its UI state through React rather than through the native DOM, and that keeps things in sync for React. There's nothing wrong about reading form
data from the DOM if you don't need React to be aware of that data. This should just be a different tool in your box when you need it.

https://jscomplete.com/playground/rgs2.7

Working with Ajax Calls

Now that we can read the input that the user typed, we are ready to ask the GitHub API for a single profile data using this type input. We can use the native fetch call
available in browsers to do an AJAX call. But this playground also has the axios library, and axios is a simple one to use here. So in the handleSubmit function, all we need
to do is axios.get and then specify the API endpoint where the data is, and this is the API input that we need. So in here, if we're to fetch Dan's profile information again,
we just use this syntax. But because we want this to be a dynamic part, we'll go ahead and make this whole thing into a template string, note backticks in here, and inside this,
we can inject the value of the username that the user inputted in the box, which is this.state.userName. We put that in here. Okay, that's how you do an axios call. 
Now axios.get returns back a promise. So to consume this promise, we can await on it, and this will give us back a response object. To make this await call work, we need to
label this handleSubmit as async. Now we can console.log the response object, let's go ahead and test that. So in here, type any valid GitHub username, click Add card, and the
handleSubmit will go and fetch that particular username's profile data, and it will print back the response. Now this response has a data attribute that has the actual profile 
information from GitHub. So what we need here is response.data. This is just the way axios works. It returns a response object and then a data attribute on that response object
that has the JSON data parsed and ready for us. Now all we need to do next is append this data object that we get from the API to the profiles array that we have on the app 
state, and when we do that, react will re‑render the App component and show the new GitHub profile. However, this Form component can't access the profiles state elements 
directly here because react components have a one‑way flow of data, and a component can't change the state of its parent. But remember that the App component can pass properties
to its Form child component, and those properties can be simple primitive values or function references. So if the App component passes a function reference to the Form 
component, we can change the state of the App component in that function, and the Form component will be able to invoke that function because it will be part of its props
object. Let's define a new function here on the App component. I'm going to name it addNewProfile, make it an arrow function, and this function will simply receive the new 
profileData as an argument, so this will be the profileData, and it will do something with it. For now, let's just console.log this profile data to make sure things are working
in the App component. Then we pass to the Form component a new prop. Let's name this prop here onSubmit and pass it this.addNewProfile. So the addNewProfile is a function that 
we defined on the instance of this component, and in here we are making it available as a new prop on the Form component. So within this handleSubmit function, instead of 
console.log here, we can access the new prop that became part of the Form component. And to do that, we do this.props.onSubmit. This is a new prop, and it holds a function
reference. And that function reference is an alias to the addNewProfile function in the App component. And as an argument, we pass it the data attribute that's coming from
the axios response. If we test now and type in a valid GitHub username, you will see the App component console log line, and you'll see the GitHub profile data ready for us 
here. So here, instead of console.log, we need to put this new profileData on the state of the App component. We need to append this object to the array of objects that we have
stored as profiles here on the state. And to do that, we have a few options. We do need to invoke setState. Remember, this is the function that we need to change the state of a
react class component, and in here we can pass either an object or a function. The updater function syntax is the same here, so I'm going to use a function. This function will 
give you access to the previous state. And what you return here from this function becomes the new state. So I'm going to return profiles:, and in here I will spread the 
existing profiles. That is something that we can read using prevState.profiles, and then append the new profileData. This is equivalent to doing a concat operation on the 
profiles array. This is the spread operator syntax. And with that, I think we're ready to test. So starting with the testData, we can now add a fourth card. There you go. 
So now we can remove all the testData and start the profiles array as an empty one like this and remove the testData from the scope. We don't need that anymore. I have included 
the GitHub username I've been testing with here. So now you can test from an empty card and add one card at a time. Notice how the username stayed here after we added the card.
So one small improvement that we can do on this is to reset the username field after we're done adding it to the profiles array. So we can simply just have another setState
call in here and pass in a userName value of empty string, and that would reset the userName state value that react is using to track the username that gets typed into the box.
So let's test one more time. And now, after adding the card, the username here should reset. There's another important improvement that we need. When you start adding data to
this form, react will give you a warning about the key prop. This key prop is something react needs whenever you render a dynamic list of children like we're doing here in the 
CardList component. React will give you a warning that if you don't specify some kind of identity for this dynamic element, then react will just assume that the position of the
element is its identity, and that might cause problems if you start re‑ordering those elements. So to avoid issues like this, you just pass a key property here to react, and
this key property has to be unique in this particular DOM node. So the GitHub data comes with an ID that's unique, so we can just use that. We can do profile.id, and if you do
that, that warning should go away. And I think we have the GitHub cards app. You can use it to add as many cards as you need. It's all driven from a single array, and it fetches
information directly from GitHub. Now there are a lot of improvements that we can do to this code, but there is one very important thing that we did not do. We did not handle 
errors. What should the UI do if the user types in an invalid GitHub handle? What should the UI do if the request of data fails over the network? What should the UI do if the 
request is taking too long? In fact, if you were in an interview doing an exercise like this, you should voice these concerns right away. These concerns are not really beginner
level, so I'm going to keep them as an exercise for you. I cover examples of them in my book, React.js Beyond the Basics at jscomplete. There are other simple improvements you 
can make to this code. For example, here in handleSubmit, we have some logic to fetch data from an API. Then we have some application logic about what to do with that data 
that's coming from the API. This is a bad mix. A component should not have this much responsibility. Your whole app should not really depend directly on a library like axios
for example. You should have a small agent‑type module that has one responsibility to communicate with external APIs and make your code only depend on that agent module.
Another thing you could do is extract this logic about managing the state of the username input into its own component as well. And this would simplify the Form component's 
code. I think this is a good stopping point for this example. Play around with the final code, which I saved here under jsdrops.com/rgs2.7. One quick exercise you can do, 
convert all the class components into function components. So instead of state here, you use a hook, and instead of this.setState, you use the updater function from the hook.

Wrap Up

We've built a few simple React components in this module, a Card component to render information about a GitHub profile, a CardList component to convert an array of records
into an array of Card components, that form component to read input from the user, and an app component to manage the relation between all the other components. We've managed
the records array as a state element on the top level App component, which allowed us to share data between multiple components, and it allowed us to append new GitHub profiles
to the UI by simply appending the GitHub API response to that state element. In the Form component, we explored how to access an element in the DOM from React directly using 
the special ref attribute, and we've explored how to read from an input element using React's state itself, with the help of an onChange event. Components written with this 
latter method are known as controlled components. In the next module, we'll build a simple game for kids. Here's a preview of it. The player gets a random number of stars
between 1 and 9, and the set of numbers from 1 to 9. They need to select the numbers that sum up to the current random number of stars. When they pick the right sum, a new 
random number of stars will appear and they need to pick again, and keep doing that until all the numbers are used.

