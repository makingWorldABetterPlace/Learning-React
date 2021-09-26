https://jscomplete.com/playground/rgs3.1

https://jscomplete.com/playground/rgs3.2

The Star Match Game

What We Are Building

In this course module, we're going to build an in‑browser game was React. I named it Star Match, and it's a simple math skills game for kids. This app will teach us a few very
important concepts about React function components, React hooks, and optimizing state and side effects in a React components tree. You can play the game at this URL here. 
Go ahead and explore it a little bit because that will help you understand the design decisions we will be making. The game is simple. When it starts, the player gets a random
number of stars between 1 and 9 and also the fixed set of numbers from 1 to 9. The goal is to use all nine numbers. For each random number of stars, the player needs to pick one
or more numbers that sum to the number of stars. So for 2, I can pick 2. For 4 stars, I have 2 options. I can either pick 4 or I can pick 3 plus 1. For 9, I have 2 options here
as well. I can either pick 9 directly or 4 plus 5. Now while the player is picking numbers, they get marked as candidates because it's not a complete answer. And if they pick more
than the count of stars, numbers get marked as wrong, and the player can unpick these candidates or wrong numbers to be able to pick a correct sum. And the game will always draw
a number of stars that is playable. So, for example, in this case, we only have 1, 2, and 6 available, so the only number of stars that get drawn are either 1, 2, 6 or the 
combination of them. And once we're done with the core UI of the game, we'll add a timer to make the game a little bit more interesting and harder to win. If the timer runs out
and you're not done picking all the numbers, the game is over. And you can always click Play Again to reset everything about this game and play again. Let's try to win this time.
We've got 9. We have 8, 4, 9. We could do 6 and 3, 3. We could do 2 and 1. And then we have 7 and 5. And that was a close one. Okay, enough play. Let's write some code.

Working with Static Markup

I kept the scope and logic of the game as simple as possible for you to focus on learning React concepts and not get distracted by any HTML, CSS, or even the math that we need 
for this game. In fact, in this jsdrops.com/rgs3.1 URL, I have given you all the distracting elements ready. This has a static HTML template for us to start with. It has all the
CSS that I've used in the game, and also I've included some globals here that has the theme colors I chose for the PlayNumbers, and all the math science were going to need. 
All of this is not really React, don't get distracted by it, but certainly take a look and familiarize yourself with the elements were going to work with here. The static HTML
markup here is already represented as a single React component. You should be comfortable with that by now. This is all JSX. Under the Colors object, I used four properties, 
these represent all the statuses of any PlayNumber. A number starts as available, you click it, and that click might change the number into one of the other three statuses based
on the current number of stars and the running sum of picked numbers. In the utils object, we have a few handy functions to sum an array, create an array of numbers, pick a random
number in the range, or pick a random sum in an array of numbers. I've implemented these with vanilla JavaScript to keep things simple, but you can opt to use different
implementations if you wish. You could, for example, use Lodash here. My point is, all of this logic has nothing to do with React. React can just use it. When that's the case,
it's a good abstraction to have on its own rather than mixing it with the React application logic. One quick note before we begin, don't get overwhelmed with the complexity of the
game. Pick one small increment that's easy to test and focus on that. Don't, for example, start thinking about how to track candidate clicks right now. We're not ready for that.
There are plenty of simpler things we can do. Pick one, focus 100% on it, test it, take a break maybe, then come pick another small testable increment. I think there are two 
beginner increments here. We could start extracting components and making a component tree. We need to do that. However, I think getting rid of any static lists here is the
better way to begin. Stars will be rendered from a certain value and that value will not always be nine. So we could get rid of all these static divs here and make a loop from
a predefined value. Let me actually define a stars variable right away, const stars equal, I'm going to start with 5. So the current focus is to display five stars based on 
this value. Now, we could use a for loop and manually push elements in an array for this task. But the declarative way of doing this is to start with an array of IDs and map
those IDs into an array of star divs. This makes the code shorter and easier to understand and maintain. Avoid for and while loops in React if you can. It's not a hard rule 
though. In the utils object, we have this range function that we can use to create an array from a number. We just give it the min and the max. So let's use that. So instead
of all these stars, we now need a dynamic expression. We're going to start from utils.range, create a range from 1 to the current number of stars, and map this range, because
that range is now an array from 1 to 5, we're going to map it into an array of stars. So let's give us an ID for the star, let's just call it starId. And we want to map this 
into an array of the original divs that we had in the markup. And because this is a list of dynamic children, we should pass a key attribute that is unique for this node. 
So we can just use the starId here. So test this increment on its own and we are rendering five stars, try to render a different number, and there we go. And similarly, we 
should also get rid of all these numbers, now that we know how to create a range, we can just do the same here. So let's just do that, dynamic expression, utils, the range is
always going to be from 1 to 9, in this case. And we're going to map it into a button component, right? So this gives us access to a single number, and instead of all these 
numbers, get rid of them and just take one of them here and put it in the map, and this is going to render the number itself. The number is 1 through 9. And we can also use 
the same number as a key here. So test that. We are rendering nine numbers. And we got rid of all the static lists. Now here's the thing. You should separate this step from the
extracting of components step, and I think by doing this first, you get a better idea into what components are good candidates to be extracted on their own. One other thing we 
could do here is start the number of stars with a random number each time the component renders. This is easy. We also have the random function here in utils. So instead of 6 
here, we can do utils.random and 1 through 9. And test that. So now each time the component renders, a different random number of stars should appear. Now because the number 
of stars is going to change while we're playing, and we need React to reflect this change in the UI, we should probably make the star count a state element. And that's easy 
because we can take this initial value and do a useState call and pass this initial value to the useState call, and if you remember, the useState call returns an array of two
elements, so we can have stars and we can have setStars. So this should work as well. But now the number of stars is a state element. We read it from the state and we could 
change this state element, and React is going to rerender the number of stars. Now here's the thing, in the current increment we're focusing on, we did not really need to make 
the stars variable a state element. So this is a little bit of thinking ahead. We don't have enough clues that this state element is absolutely needed. And guess what? It is not
really needed if we're to super optimize the code. But from experience, whenever you identify a data element that's used in the UI and is going to change value, you should make 
it into a state element, and only optimize the elements on the state when you have enough clues about how they fit with the other elements on the state. It is normal for the 
state elements of React components to grow and shrink as we design them. I've saved the code we have so far under the rgs3.2 link here.

https://jscomplete.com/playground/rgs3.3

Extracting Components for Reusability and Readability
Continuing from the previous progress, a good next increment is to think about what components we need in this app. Should we, for example, extract the help line into its own 
header component maybe? Or is that a not‑needed abstraction? Should we make the stars section a component? We can also implement this whole app with a single component, but that
would leave us with a really big component. We need to start thinking about splitting responsibilities. Here's the thing. Too few or too many components are both bad. You need 
a good balance here. Let me give you one important pointer to identify a good candidate for a component. Every time in the UI you have many items that share similar data or
behavior, that's a candidate for an Item component. The play numbers here will have the exact same behavior. Each click on a number will invoke logic to determine if that click
is good or bad. The numbers are going to invoke this behavior with different data, but the nature of the behavior is similar, so this is a good clue that we should extract a 
play number into a component. Let's do that. I'll take this part and get back here once I'm done designing the component. Okay, what's a good name for this component? Let's 
call it maybe Number. Each react component receives a set of props, and we'll make it return the exact same value that we had before. So now back in here, we do Number, and 
this Number will need to receive the property of which number to display. So let's just pass it here as a prop, number ={number}, and because it's now a prop in here, I can 
access it as props.number. I don't need the key here anymore. The key is needed on the immediate element in the loop, this thing in here. So let's cut this part and put it back
in here and make sure things are still working. Cool! Here's an important question now. What is wrong with what I just did? Just because what I did is working doesn't make it 
right. One part of the change I just made is fundamentally wrong, and you should be able to identify it. And I'm talking about this Number name. By naming my component Number,
I am actually overriding the native Number class that's available in JavaScript. This Number constructor is used in JavaScript to convert a string into a number. For example, 
say that these edges of the random range are received for some reason as strings. If you just use them as strings here, things will not work as expected. So one solution is to 
call the Number constructor on this to change it into a number. But guess what? This will not work now because I've named my component Number. So in here I am not using the 
Number constructor anymore. I am using the component I just made. So this is bad. Be aware of the top‑level JavaScript objects in your scope and do not override them. A good way
to avoid this conflict is to always name your components with two words instead of one. Maybe we call it PlayNumber instead of Number, which means we need to change this into 
PlayNumber. And now this Number call here is using the native JavaScript Number. Okay, now that we have a shared component to represent a single number, we can define behavior
on this number. Let's go ahead and define an onClick behavior. We need to identify when a number is clicked. So I'll inline an arrow function here and just use a console.log 
line that we have clicked on a number. So we need props.number here. And let's test this change. Click around and make sure the number values are being reported. Here's an 
important question for you. 

How exactly is this working? 

We have a function here, and this function gets invoked on each click. What is the JavaScript concept that's at play 
here that makes this click handler access the value of each number? The onClick Handler is a function within another function, the PlayNumber function. So focusing on just the 
play numbers, we created nine top functions and then nine click handler functions in them. So what is making all this work? And the answer is JavaScript closures. Each onClick 
function here closes over the scope of its owner number and gives us access to its props. We have nine onClick handlers, and they all have different closures closing over 
different scopes. This is important to understand and remember when working with stateful function components in react because they do depend on closures. And this could also be
a source of bugs later on if we forget to refresh the scope of a closure. So you just need to start identifying when closures are being used in your function components.

Okay, what other components should we extract? So the concept behind extracting a play number here is reusability. We want to make a play number reusable and define some shared 
behavior on it. The other guideline for extracting components is readability and making components smaller in general. An example of this would be here. This part here is 
displaying stars, but that information is not immediately visible. I could make this part a little bit more readable by rendering a component here. Maybe we call this one 
StarsDisplay, and StarsDisplay is a simple component that receives props and returns what we had before. But now we have a list of adjacent items here, so we need to make this
into a single element because every react component needs to render a single element. Now, if we don't want to introduce any new element nesting in the tree, we could just use
the react fragment concept and wrap this whole thing with an empty JSX tag here that represents a react.fragment. The other challenge about this change is we previously had
access to the number of stars when we were here, but now we added another level abstraction. So we need to flow down the number of stars to the StarsDisplay, and it doesn't have
to be the exact same name. I could say this is just the count of how many stars to display, and this count can be assigned to stars, and now in here instead of stars, the range 
is props.count. I still need the key here because that is the dynamic child inside the map. But with that, let's test this change, and things seem to be working. Now you can 
definitely think about extracting more components out of this StarMatch component, but just don't overdo it. Let's just run with these three components for now and focus more on
the interactions between them. So let's start thinking about the next react concept here, which is how to make the UI an exact description of all the state elements in this app.
We've already made the UI describe how to render a number of stars, but that's only one state element. We have more. We need to think about picking a number next.

https://jscomplete.com/playground/rgs3.4

View Functions: State => UI

Let's now start thinking about what will actually happen when we click on these numbers. There's some math logic that we need to come up with, and that's mostly JavaScript. 
But here's the thing, for every behavior you're trying to implement in the React application, there are two aspects to it. There's the actual logic for the behavior, and there's
the UI logic to describe what this behavior is going to be changing. So when we click on a number, we're going to have to change that number's color based on its new state. 
We're going to have to do some math computations to figure out this new state. But we also have to reflect this new state change to the UI. And it's often easier to start by 
doing the UI logic. First, however, to design your UI logic, you need to come up with what elements you need to place on the state. Because we want React to change the color of
every number we click, we will have to maintain some containers of data on the state. If you remember the number statuses, we have candidateNumbers, we have wrongNumbers, we 
have usedNumbers, and we also have the list of availableNumbers. Which of these containers should we place on the state to enable us to describe all the possible states? And the
general advice in React stateful components is that you should minimize the state. Don't place on the state anything that could be computed from the other things that you place 
on the state. For example, wrong numbers can be computed from candidate numbers because we have the count of stars and we could just sum the candidate numbers. And if the sum is
greater than the count, then we have wrong numbers, so we shouldn't really place the wrong numbers on the state. Also, the list of usedNumbers and the list of availableNumbers 
are just the inverse of each other. If the number is used, it's not available, so we could just use one or the other. We could start a usedNumbers container as an empty array,
and then every time we need to mark a number as used, push a new element that array. Or we could start the list of available numbers as all the numbers and every time we need to
mark a number as used, we remove number from the availableNumbers. I think having the availableNumbers on the state is a little bit more interesting than having the usedNumbers.
So when you design your state elements, make sure they're enough to represent all the possible states and also make sure they are the minimum to represent all the possible 
states. So let's make them official. I'll start with the availableNumbers here, we'll put them in constants, availableNumbers, and you also get a setAvailableNumbers from Reacts
useState. And in here you do useState and you pass in the initial value. Now the initial value of all availableNumbers is the full range. So we're going to come back to here and
put the full range of the availableNumbers here. And similarly, the candidates in a constant and you get setCandidateNums. And in here we useState, and the initial value for the
candidateNumbers could be just an empty array. But here's the interesting thing about the increment that we're doing. We don't really need to worry about the transactions on 
these candidateNumbers and availableNumbers yet. We just need to come up with a UI to describe them. So we can just use mock values in here. Let's, for example, say that 2 and 3
are candidates. And let's say that we only have 1, 2, 3 and 4 and 5 as available, which means 6, 7 and 8 and 9 are used already. We can't play them anymore. So by using mock 
data like this, we get to focus on the UI description and not the transactions on the state. Okay, so now 2 and 3 needs to show up as candidates. They will be wrong candidates 
rendered as red if the number of stars is less than 5 and they will be blue candidates if the number of random stars is more than 5. And we know that 6, 7, 8 and 9 needs to show
up as green, used, not available anymore. So the number component needs access to this data, both the availableNumbers and the candidateNumbers, and actually the number of 
stars, to be able to render itself. So we need to pass some kind of data to the PlayNumber component. Let me put things on multiple lines. Let me also put the number component 
here on multiple lines. And now let's think about what kind of data we need to pass to the PlayNumber component to make it render itself. You could, for example, think about 
passing the state elements to each PlayNumber component. I could be passing the availableNumbers here and the candidateNumbers and the stars to make a PlayNumber decide its own
style. However, this is too much information for a single PlayNumber. A single PlayNumber doesn't care about all the availableNumbers. It doesn't care about all the 
candidateNumbers. It only cares about whether itself is an availableNumber, a candidateNumber, a usedNumber, or a wrongNumber. So instead of availableNumbers, we could pass this
PlayNumber component Boolean attributes, like, for example, is it used? Is it a candidate? This is a little bit better than passing the whole information down to the PlayNumber 
component. You want the component props to be exact, only the data that's needed to render the component and nothing else, because by passing more information than needed, the 
PlayNumber component would be rerendering itself in a few cases unnecessarily. However, instead of passing multiple Booleans about what status the PlayNumber is, we could just 
pass the status itself directly and pass just one value for the number component. And to do that in a readable way, maybe we can introduce a number status function and pass the
number ID here, the actual number, and this function is going to return what status the number is using all the data that's available here in StarMatch. So let's do that. 
We'll introduce a function, call it numberStatus. This function takes in a number and it will return one of four values. The order of the conditions that we're going to write in
this function actually matter because if the number is used, it can't be a candidate or wrong. So let's start with used. A number is used if it's not in the availableNumbers. 
So we could just have an if statement here and do a check on this availableNumbers array and say something like if the number is not in the availableNumbers array, and in 
JavaScript we can just use the includes method on an array. So if availableNumber includes number is false, the number is used. So we could just return used in here. Now if the
number is in the availableNumber array, now we can check if it's a candidate. So is the number in the candidateNums array? And we can use a similar check here. If number is in 
candidate, that means the number could be either a correct candidate or a wrong candidate. So we're going to return one of two values here. And finally, if the number is not 
used and it's not a candidate, it is an availableNumber. So let's return available here just for consistency and so that we can look up the style from the theme. By having 
consistent status for each number, we can just look up the style of the number from this theme, So I've got available, used. Now we need to figure out wrong and candidate. 
Candidate means we're still playing. And wrong means we picked candidates, but they are wrong. So we need to compute a value now. Remember how we didn't place the wrong numbers
on the state because we determined that this is something that we can compute? We need to do this computation now. So let's call this candidatesAreWrong. So the candidates are 
wrong when the sum of all the numbers in the candidateNumbers array is greater than the count of stars. Now, in the utils object we have a way to summon array. So we're just 
going to use that. So candidatesAreWrong when utils.sum for the candidateNumbers, the whole array of candidateNumbers, is greater than the count of stars. This makes all the 
current candidates wrong. So in here, in this condition, if the number is a candidate, then we're going to say, are the candidates wrong? And if they are wrong, then this 
candidateNumber has a status of wrong. And if the candidates are not wrong, then this candidateNumber is an actual candidate that needs to show up as blue. Okay, let's test this
logic. We are passing a new status property here, and this status property is going to be computed from all the mock data that we placed on the state. So, in the PlayNumber 
component, we need to introduce conditional styles based on this new status property. And we can use React style object for this. Now the style we need here is really simple.
We need to just change the background color of the number. So we do backgroundColor in here, and this backgroundColor is the value that we need to pick from the colors object.
And since we have the number status here, this is just a direct look up of the colors object. So the background of a PlayNumber is the value from colors that is associated with 
props.status, the new property that we just computed and passed to each number, this one. And we can test. And check it out. The numbers that are not available are showing up as
selected, and the numbers that are candidates are showing up as blue here because we have nine stars, and two plus three is still less than nine. If we render a case where two 
plus three is more than the number of stars, they are showing up as wrong. So what I just did here is complete UI logic. I didn't do any transactions on the state. I did not do
any math to figure out if the number should go in the candidateNumbers or if it should be removed from the availableNumbers. That's what we're going to do next. But just notice
how I focused on what state elements to introduce and what changes in the UI description to do to make it honor these new state elements. And now that we're done testing this UI
description, we can go back to the actual initial values that we need for each state element. We need empty array for the candidateNums, and we need the full list of numbers, 
and it's the exact same thing that we're using here to represent all the available numbers. So I can take this one here and make it the initial value for the available numbers,
and the UI is rendering all the numbers as available, no candidates regardless of the count of stars. The logic that we did here in the numberStatus function,, by the way,
is not very important. This logic will depend on the application you're writing. The React concept that you need to appreciate here is how we've introduced elements on the state
of this application, mocked the initial values of these elements, and changed our UI description, the function of our data, to honor these new elements. Now we're ready for the
next step, which is to figure out how to transact on these new state elements, to complete the story of this app. We'll do that next.

https://jscomplete.com/playground/rgs3.5

Behavior Functions: State => New State

Now that we have state elements and we have a UI description to honor these state elements, we need to come up with the logic to figure out how to do transactions on these state
elements. This is the logic that's going to happen on each number click, and it needs to be here in the top‑level component where the state is owned. So let's define a function,
call this function what to do on each number click, so onNumberClick. This function needs to receive the number that was clicked. Here are the decisions that we need to make in
this function, based on the current status of the number, what should be the new status of the number? Now because we have computed the current status for each number, we 
shouldn't do that again. Each number here is aware of its own current status, so when we click on it, it can communicate this status to the onNumberClick. So let's test this
first increment. When we click on a number, let's report the status of the number that was clicked right here from the onNumberClick. We're going to have to pass this new 
behavior, the onNumberClick behavior, to the PlayNumber component. That's the component we're going to be clicking. So let's define a new prop here, call it onClick, and we pass
it here as onNumberClick. This is how the parent component is telling the child component what behavior to invoke each time it's clicked. In the PlayNumber component, we will
now be receiving this behavior as a prop. So instead of console logging here onClick, let's invoke this behavior. We can access it as props.onClick. This is what we're going to
be doing onClick, we're going to invoke the behavior that was defined by the parent, and we can pass in what number is being clicked. We can also pass in what's the status of 
the number that's being clicked instead of computing the status again. So in here we can also pass props.status. Now, down in the onNumberClick, this function is receiving the
number that was clicked and the current status of the number that was clicked, and the logic here needs to determine what is the new status of this number that was clicked. So 
now for these computations you have to take into consideration all the possible statuses for this number. We could be clicking on an available number. That's good. We could be 
clicking on a used number. That's not good. We should not be picking another used number. Once the number is used, it can't be used again, so that's actually a good condition to
start with. If the current status of the number is used, we can't do anything here. We should just return do nothing. Now, if the current number is not used, then we need to
make it into a candidate number, but also remember that we have an existing candidateNums array, so we're really appending a new number to the candidateNums array. And this 
should happen anyway. Let's come up with a new candidate numbers, and this is the existing candidateNums array concatenated with the number that was just clicked. From this 
point, we have two possibilities. The set of new candidate numbers could be just candidates, and for that case, we just need to place this new candidate numbers array on the
state of candidate numbers. But the other possibility that now with this addition to candidate numbers we have a right pick, and in that case we need to update the game to mark 
these candidate numbers as used and redraw the stars. So there are two branches here. So let's introduce an if statement. The logic of this statement is, do we have an exact 
pick or not? So we need to sum the new candidate array. We can use utils.sum for that, sum newCandidateNums, and check this number against the count of star. If it doesn't equal
the count of stars, then we don't have a correct answer, we just need to mark the number as candidates, and we have a setCandidateNumbers function to do that. We just do 
setCandidateNumbers, the newCandidateNumbers. However, in the else branch here, that means the sum of the newCandidateNumbers equals the count of stars. We have a correct pick.
All the newCandidateNumbers should be marked as used. They should be removed from the available numbers array, and we need to reset the candidate numbers to an empty array. 
And we also need to redraw the number of stars. So we actually need to invoke all three state updater functions, but we need to figure out the new available numbers. We need to
remove the new candidate numbers from the set of available numbers. So let's come up with newAvailableNums and compute that. This starts from availableNums, but then we can 
filter out all the candidate numbers. The JavaScript filter function will give us access to each available number, so give it a name here, and then the condition that we need
here is the available number included in the new candidate numbers. So we can do newCandidateNums.include, this n, and if this condition is true, we need to filter out the 
number from the available numbers, so we need to negate this for the JavaScript filter function. If the number is not included in the new candidate numbers, keep it in the new
available numbers, otherwise, remove it. Now that we have new available numbers, we can setAvailableNums. This is the state Hook updater function, and the value is the 
newAvailableNums. We also need to reset the candidate numbers, so setCandidateNums to be an empty array again, because the player is going to be picking more candidate numbers.
The other thing that we need here is to redraw the number of stars. We need to do that as well. Now that we have a correct pick, we need to redraw the number of stars. But 
here's the thing, we can only redraw numbers that are playable. We can't pick any numbers of stars. This is where the util function randomSumIn comes in handy. This takes in an
array and the max sum, and it will compute all the sum permutations in that array and pick a random sum from that that's less than the max here. The max is 9 for this game, and 
this array that we need to pick random sums from is the new available numbers array. So back in the onNumberClick, to redraw the number of stars we're going to do setStars, and 
in here we'll do utils.randomSumIn the newAvailableNumbers, and our max here is 9. Redraw a number of star that is playable, and I think we can test. I see a typo here. This 
includes needs an e. This is the exact type of problem that a strongly typed wrapper around JavaScript would detect. A very good next step after this course is for you to 
explore something like TypeScript. Okay, let's test our progress so far. We have nine stars. Pick 9, 9 is selected, and the new number of stars is picked. Pick 8, and we have a
new random stars, which is also 8, and now we have to pick two numbers. We have to pick either 7, 1 or 2, 6 or 5, 3. We can also pick 4, 3, and 1, and now three numbers are 
selected and we have a new number of stars, which is seven. So if I pick 7, I've got 2, and if I pick something more than the count of stars, it is now marked as wrong. Now we
didn't really do anything about the wrong status here, but we don't have to, because, remember, the state of candidates being wrong is always computed. No further logic is 
needed for marking a number as wrong. Now here's the thing, I marked the number as wrong, but now I have no way to unmark it. In the final game, you can click on a candidate
number to unmark it so that you can win the game. So let's do that next. This is a case that we need to handle right here before we put the number as a new candidate. We need 
another condition here that says if the number is available, then put it in the new candidate numbers, but if the number is not available, what should we do with it? So I'm 
going to introduce a new condition right here because this could be a simple turn array. We always need a new candidate numbers array. So in here we could say, if the current 
status of the number is available, then we can mark it as candidate. If it's not available, that means it's part of the candidate numbers array, and we should remove it. And we
can use the JavaScript filter function to do that declaratively. We can say candidateNums.filter the number that was just clicked. So this will give us access to existing 
candidate numbers, and we need to filter out the case when the candidate number does not equal the number that was clicked, so keep all the candidate numbers except the number
that was clicked. And this is one‑to‑many equal. So there we go, let's test. Let's pick 1, and now we have four. I'm going to go ahead and pick 2 and 2 is selected, and I'm 
going to pick 8, now the set of candidate numbers is marked as wrong, and if I pick 2 again, it should be unmarked as candidate. Pick 8, not a candidate anymore, so this worked
for both candidates and wrong numbers. And if I pick an available number, then the game should continue as normal. So once again, don't focus too much on this logic that we did
to make this feature work. This logic will be different based on the application. Just appreciate the fact that we're just transacting on the state, and the UI of the 
description that we've already made is ready for us to reflect these transactions.

https://jscomplete.com/playground/rgs3.6

Resetting the State

The code we have so far is under rgs3.5. And guess what? We have a playable game. We can actually win this game now, with 7, we can pick 6 and 1. There's 4, another 7, 8 and 9,
and done. But now the player has no way to play this game again. So when we reach this state, let's put a button here to play this game again. We need a condition here in the
left section of the game, and that's a simple condition that should determine if the game is done. And rendering this starsDisplay component should only happen if the game is
not done. If the game is done, we should render something else, the Play Again button. Now you might be tempted to put the computation about whether the game is done or not 
right here. In fact, it's really easy. The game is done when the available nums.length equal to 0. That's it. That's the condition that we need for when the game is done.
And if this condition is true, we need to render the play again UI logic. If this condition is false, we need to render the starsDisplay logic that we had before. So let's
assume we're going to have a PlayAgain component, and we're going to render this here if the condition is true. The thing is, whenever you have some kind of computation like
this, you shouldn't really do it right here within what the function returned. And that's for many reasons, but mostly for readability. And this is actually true for this other
computation here, but I'm going to focus on this one. This is a little bit less readable than doing something like gameIsDone. And that's why you should prefer to do these 
computations in variables before the return statement. So let's do that. Maybe right where we did the candidatesAreWrong, we can also do gameIsDone. And in here we put the 
exact same condition that we've tested. This right here is a much better place to do the computations. In fact, the structure of a React component should always be similar.
The first few lines should be any hooks into the state, any hooks into any side effects of this component, and then after that, you do any computations based on the state. 
This is core application logic. While the return statement here is a description of the UI based on all your states and all your computations out of that state. So I think
that distinction is handy. Okay, let's write the logic for this PlayAgain component. And that's another thing, when you have conditional UI, it's usually a good idea to put 
the conditional logic in a component rather than in‑lining it here, because that would make the top level component less readable. All right, let's do PlayAgain. PlayAgain is a
component. Put it right here. A component that takes props. And it could just return a simple div. Give it a class of GameDone, this is the class that I've prepared for this
section. And in here we can just have a simple button that says Play Again. And before you worry about how to play again, test that this logic is rendering correctly. Go over a
complete game in here and make sure that the Play Again button is going to show up. Test that. And there you go, Play Again is showing up. Okay. How do we play again? You have 
two important ways to play again. We can simply reset the state, and it's really easy. You can reset the state to the same initial values that you've started with on the very 
first render of the game. So we could have a function here. Let's call this function resetGame, and this is a very simple function that will basically do three sets state calls.
It will set the stars to the initial value, which is this thing in here. It will set the available numbers to the same initial value that we started with, which is a range from
1 to 9. And it will also set the candidate nums to an empty array, and this would reset the game because now we're back to the initial status of the game. And to use this
resetGame, we need to pass it to PlayAgain. So in here we can give it any name. I'm going to just name it onClick, right, separation of responsibilities. This PlayAgain button
doesn't really need to know what is going on onClick, it just needs instructions of what to do onClick. So onClick, this PlayAgain button receives it as a props, and on its own
onClick event it can just invoke this props that came from the parent. That's it. Let's go ahead and test. We need to play a full game in here. And now when I click PlayAgain,
the whole game should be reset and I can play again. So this is method one, and it's usually enough. However, things get complicated when your components have side effects. 
By side effects, I mean things like subscribing to data or starting timers, which is something we're going to do next. Remember, we're going to have to implement this time
limit on the game, so we're going to start a timer, and the timer in a component is basically side effect. So when you reset the game, you need to also reset any side effects,
not just the state of the game. So just keep that in mind. Once we implement this timer, you'll see how the timer is actually a side effect, and you'll see how React handles,
creating and removing side effects, and we'll come back to this resetGame function and write it in a better way that also takes into account the side effect of the game. 
We'll do that in the next video.

https://jscomplete.com/learn/react-beyond-basics/react-hooks-deep-dive

https://jscomplete.com/playground/rgs3.7

Using Side Effects Hooks

We are ready to implement this timer here. Now, this is the number of seconds left. You have 10 seconds to play this game, and we need the UI to reflect the countdown. So every
time we have a countdown, we need the UI to trigger a render. This means that we need to place this logic here on the state of the component to enable React to retrigger a UI
render for every second that ticks. So let's call this new concept secondsLeft, and let's give it a new state element. So I'll do secondsLeft, and I'll do setSecondsLeft in 
here. And this is a useState call, and the initial value of the secondsLeft is 10 seconds. That can be customizable later on. The secondsLeft is something that needs to be 
rendered here instead of the hardcoded 10 that we had in this dev, and test that. Now in JavaScript, when you need to start a timer that ticks every second, you have the option
to do a setInterval. This setInterval function can be a way for us to implement this countdown feature. But we can also implement it by taking advantage of the fact that React
will invoke our StarMatch function here every time a state changes. And the state is going to change every 1 second at minimum, which means we can also use a setTimeout call to
implement this exact same feature because we know that the StarMatch function is going to be invoked every second. Using setTimeout here is a bit more interesting for you to
understand the nature of a React component's side effects. So let's implement the countdown feature with a simple setTimeout call. But before we do, we need to understand how to
implement side effects in React. The only React Hook we've used so far is the useState Hook. React has a few other Hooks function, and one of them is useEffect. This, of course,
is React.useEffect, but it's available here globally in the playground. This useEffect is exactly what the name suggests. It is a way for you to introduce some side effect for
this component. The useEffect takes in a function, and it will run this function every time the owner component renders itself. So if we put a console.log line here, this line
really means that the component has done rendering. You'll see this line every time the component is done rendering. So when I click on a number here, the component has to 
rerender itself because the state has changed, and when it's done rendering again, it will console log this line. And it will continue doing that every time the component
renders, which means we can introduce our own side effect right here inside the useEffect in here. We need to setTimeout after exactly 1 second and give this timeout a function
to basically change the seconds left and decrement the current value by 1. So we can use the setSecondsLeft here, and the new secondsLeft would be the existing secondsLeft ‑ 1,
very simple. And guess what? Because useEffect is going to set the state in here, and because that set state is going to cause React to rerender the StarMatch component, the 
useEffect is going to continue to run, and this will actually make a loop. You can test this right away. The secondsLefts are going to start ticking immediately, and we don't
have any exit condition from this loop, so we need an exit condition, because right now it's just going to continue going under 0. So in here we could introduce an if statement
to exit this looping mechanism. And the if statement is basically if the secondsLeft is still greater than 0, only in that case introduce a timer. But once the secondsLeft are
0, then don't do this timer again. So now the timer should tick all the way to 0, and then it will stop because this condition is going to stop it. And we will not introduce a
new timer when the seconds are 0. Cool. But here's the thing. This useEffect is also going to run when the other state changes. So when I click a number to mark it as candidate
or used, the useEffect is going to trigger again. Which means if we run this code and start clicking numbers, this timer is going to be created far more often than we need to.
And that might introduce bugs if you're not careful, because every click here is triggering a useEffect call, and it's creating its own timer. The good practice here is that
whenever you create a side effect, you have to clean that side effect when it's no longer needed. The useEffect Hook has a mechanism for us to clean the side effect when it's no
longer needed. So let me show you this mechanism. Let me comment out this timer code and we'll get back to it later. The mechanism to clean a side effect is in the returned
value of this callback function within the side effect. You can return a function here, and React will invoke this function when it's about to unmount the component, when it's
about to rerender the component. So in here the console.log line could be something like this Component is changing, and React is going to invoke this function every time it 
sees a change in the component and the component needs to rerender or even when the component needs to be unmounted. So remember, the effect itself, run every time the component
is done rendering, done rendering. In here, the component is changing and it's going to rerender, so the Component is going to rerender, basically. These are the two mechanisms
for introducing a side effect and cleaning up that side effect. So if you render this code in here, you'll see that the component is done rendering. And when you click any 
number, you'll see how the component is going to rerender, and it rendered, and then it's done rendering. This happens on each click. So what we need to do for our timer is to
basically clean up any timer that we introduce in one render cycle if the component is going to rerender. To clean up a timer, the setTimeout call gives us back a timerId, so 
we can capture this timerId in here. And to clean the timer, to remove a timer, all you need to do is call the clearTimeout call on this timerId. So in here, in the same if
statement, we could return the cleanup effect. The cleanup effect is to basically call the clearTimeout call on the same timeId. So now every time the component rerenders
itself, we will remove the previous timer and introduce a new timer, and this way we will be sure that there will be no timer conflicts. You should always get in the habit of
cleaning up after your effects. If you introduce an effect, you should always return a function that cleans up after that effect. However, introducing this cleanup function
actually introduced another issue with this timer, and you can see that one in action if you click on one of the numbers repeatedly. You'll notice that the timer stops. 
Basically, you can cheat on this game if you need more time by just repeatedly clicking on a number. This is because the useEffect runs on every state change. And now when it
does, it resets the timer that's trying to decrement secondsLeft using the new cleanup function. So when we click on a number, we're also resetting the timer. Because this is
just an enhancement, I'll leave this issue as is in the first version of the game. However, I wrote an article with more details on why this problem is happening and the few
ways it can be solved. You can check that one out at this URL. So we have a timer and that timer is ticking down all the way to 0, and we can play and win the game before the
time runs out. But we should also change the status of the game to done when the time runs out and actually have a different message based on whether the time ran out or the 
player was able to pick all the nine numbers before the time runs out. So this gameIsDone condition can change now and account for the time, so we need to do one more condition 
about when the game is over. Let's actually create a new variable, call this variable gameIsLost. So the gameIsLost when the secondsLeft are exactly 0. And we should probably
change. gameIsDone to gameIsWon. If you're able to take all the available numbers down to 0, then you've won the game, but if you run out of time, you lost the game. And the 
game is done if either of these two variables are true. But here's the thing. Instead of managing two states about the game status, how about we come up with a single variable
that represent the game status? So let's do gameStatus in here, and we can put the same condition to figure out the gameStatus. If this is true, then the gameIsWon. And if this
condition is false, then we need to check the other condition. Are we out of time? If we're out of time, then the gameIsLost. Otherwise the game is still playing, so maybe we
call that status active. So this one gameStatus variable captures these two computations. It's usually better to have a single variable rather than two variables that are 
falling in the same scope of computations. Now, if the nested ternary here is bothering you, that is really not the point. You can have two if statements here to replace the
nested ternary, or even have function to compute the game status on every render. But I'm just going to move on. Now that we have gameStatus, we need to determine here whether
to show the PlayAgain or the StarsDisplay. If the condition is now if the gameStatus is not active, you need to show the PlayAgain. You show the PlayAgain in two cases, when the
game is won or lost. Also, let's pass the gameStatus itself to the PlayAgain component in order to show a different message if the game is won or lost. So we pass gameStatus as
gameStatus in here, and in the playAgain component, let's introduce a message, so we'll put that in a new dev here, give it a className of message, and the message here will
need to be different if the game is won or lost. So we know that the gameStatus is not active here, so we can just introduce a condition and the gameStatus is part of the props
of this component, so props.gameStatus. And we can simply have an inline condition here that says If the game is lost, render the message Game Over. If the game is won, render
a message for the winners. We can also use the exact same condition here to style this message and show it in a different color if the game is won and a different color if the
game is lost. And for that we can use React's style property and in here pass in an object that is based on the same condition. We can, for example, change the color of the 
message based on the props.gameStatus condition equaling to lost or won. If its lost, show the message as red. And if the game is won, show the message as green. React's style 
property is handy to do this inline conditional logic here that is depending on the component props. And I think we can test. So now if we let the timer run all the way down to
0, the game should be marked as lost, and the PlayAgain should show up with a Game Over message. But here's the thing. This reset is not working now. Why? Well, because we also
need to reset the secondsLeft to 10, remember? So when you need to reset the game, you need to reset all the state. And also you need to reset any side effects that you 
introduce in the game. Now, in here, we really stopped the timer so we don't have any more side effects. But in case you have a side effect, you need to call the cleanup as well
when you reset the game. So in the next video, I'm going to show you how to reset the game by unmounting the component rather than by resetting the state. Because when you 
unmount the component, remember, React will also call all the cleanups that you have. And I think that's a cleaner way to implement the PlayAgain button. Before we do that,
let's make sure that the game is winnable and that the display is going to render the nice message. If you noticed, the timer continued running all the way to 0 even though the
game was done. So we should actually stop the timer when the game is won. There's also another bug in this game. When the timer runs out and the game status is lost, the player
can still play the game. Let me show you that. So game over, and I can still click those numbers. That does not make sense. There are a few conditions that we need to do, so
let's go over them. The first one is right here. We should not introduce a new timer if the game has been won. If the game is done, and the game is done if the available numbers
are down to 0. So in here, we should only introduce a new timer if secondsLefts are greater than 0 and the available numbers are also greater than 0. These two conditions means 
that we're still playing, and we should continue counting down. But if the available numbers are 0, then the timer should stop. The other condition that we need is in the 
onNumberClick function. If we click a number and the game is actually done, then we should also do nothing. So we could just add another condition here to the same if statement.
If the game is not active, if gameStatus is not active, or the status of the current number that we're clicking is used, we really should do nothing and not change the state
again. So to test that, let the timer run down all the way to 0 and click again and see if you can click these numbers. You should not be able to click these numbers.

https://jscomplete.com/playground/rgs3.8

Unmounting and Remounting Components

Under the rgs3.7 link, we've implemented the timer, and we've implemented the statuses of the game. The game can be active, won, or lost, and the only thing that stopped working
for us is the Play Again button. So it is time for us to talk about that. Instead of this resetGame, I'm going to come up with a different mechanism to reset the game. And that
mechanism is to simply unmount the component from the DOM and remount it again. However, to accomplish that, I'm going to make the StarMatch component a container of another 
component that I will introduce, which I'm going to call Game because now this application is not just a single game. This application will render many games as we go on. So 
let's keep this ReactDOM.render call to render the StarMatch, but let's rename the StarMatch here into Game instead of StarMatch and introduce a new component and call that
component StarMatch. So we'll call this StarMatch, and this is a function that basically returns a game. So this is exactly the same and test that we didn't break anything.
Game is rendering, the timer is running down, and now I get this error that resetGame is not defined because I've used it here. So we need to come up with a different resetGame.
And to reset the game, you need to just unmount to this component and render a new component. And here is a trick to do that. If you specify a key for this component, remember
the key attribute? The key attribute is the unique identity that React uses to identify a component element, which means if the key element changes, say from 1 to 2, React will
see a completely different game because the game with the key 2 is a different element than the game with the key 1. So if we place a key here and change it when we click to
play again, React will just unmount game 1 and mount a brand new component that is game 2. And when React unmounts game 1, it will reset everything about game 1, including side
effects. And when it mounts a new game, it will introduce that with a brand new state for each game. So we can simply introduce a state here for the game ID. Let's call it
gameId, and you also get a setGameId call. And you can use the state hook for that and start it from any value really. So I'm going to start by 1. And when you return the game,
we return it with a gameId. This will render the game, but we still didn't replace the onClick mechanism here. Now here's the thing. Because the resetGame is now part of the 
StarMatch logic, we're going to have to pass a behavior here down to every Game component to design the reset mechanism. So a good name for this function would be startNewGame. 
And this is what this function is going to do. I'm just going to inline it here. This function is going to set the gameId to a different value. We can just increment the
existing gameId. So every time I need to reset the game, all I need to do is change the key attribute. Because the key attribute is hooked to a state in here, I can just change
the state and React will unmount the previous game that had the current key and mount a new game that has the new key. So now the Game component receives a prop called 
startNewGame, and this prop is going to reset the game. So we need to pass it down here to the PlayAgain component. The onClick becomes props.startNewGame. And now when the
timer runs down all the way to 0, it looks like we have an error. Oh, props is not defined. So a component here needs props. It's undefined. Let's test this again. When the
timer runs out, we should see the Game Over. When we click on that Play Again button, here's what's going to happen. React is going to change the gameId from 1 to 2, and that
will make the game unmount, clear all the side effects, and mount a new game with a new state. All the new state elements here are going to be brand new because we are mounting
a new game, and there you go. This should happen for both winning and losing the games. So let's test the other case here. Play Again should reset the whole thing. It will reset
the timer. It will clean up all the side effects. So this concludes the first playable version of this game. But before we conclude this course module, let me tell you about one
other important concept about React components, and that is how to extract some logic into a different entity. If you look at the Game component now, it is big. There is a lot 
of things going on here in the Game component. The other components are fine. They're small, they receive props, and they render things based on those props. But the Game 
component is huge. It has states, the initial values of the state. It has effects. It has computations about the state, it has functions to transact on the state, and it also
has its own render logic based on the state and the computations. Now the reason this component is huge is because it's the only state manager in this application. It has the
responsibility of managing the state, and it also has the responsibility of rendering the game tree. And while this works, there is actually a better way to split these two
responsibilities. We'll talk about that in the next video.

