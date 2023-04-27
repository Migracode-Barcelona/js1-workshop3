# 3 - Arrays and callbacks

> ⚠️ **If your assignment has been given to you through GitHub Classroom, this repository *does not need to be forked*: open the created repository using CodeSpaces OR clone the created repository!**

> 💡 Inside a CodeSpace or VS Code, you can also use the shortcut: Control+Alt+N (or ⌃ Control+⌥ Option+N on macOS), or press F1 and then select/type Run Code, the code will run and the output will be shown in the Output window.

## Learning Objectives

By the end of this class, you should be able to answer these questions:

* Describe what an array method is and use them to manipulate an array
* Write code that chains array methods together
* Define what a callback is
* Write code that uses a callback to run code
* Define what an anonymous function is
* Write code that uses an anonymous function as a callback

## Array properties

Arrays, like strings, have a `length` property.

You can check this by starting a node console in your terminal.

```
$ node
> let arr = [1, 2, 3];
undefined
> arr
[1, 2, 3]
> arr.length
3
```

### Manipulating arrays <a href="#manipulating-arrays" id="manipulating-arrays"></a>

You can **get** a single value out of an array using **bracket notation**.

```
$ node
> let ingredients = ["Flour", "Water", "Salt"];
undefined
> ingredients[0]
Flour
> ingredients[1]
Water
> ingredients.length
3
```

Did you notice how we use `[0]` to get the first value? In programming we count starting at zero.

> The number inside of the brackets is called an **index**. Index just means the position of the item within the array.

You can also **set** a value using bracket notation and an assignment operator (`=`).

```
const scores = [80, 41, 47];

scores[2] = 29; // Change the last score
scores[3] = 51; // Add a new score
```

#### Exercise A (5 minutes) <a href="#exercise-a-5-minutes" id="exercise-a-5-minutes"></a>

* Create an array with the names of the people on your table
* `console.log` out the names and how many people are at the table
* Put someone from another table at the beginning of the array
* Add someone else to the end of the list

### Working with arrays <a href="#working-with-arrays" id="working-with-arrays"></a>

When working with lists it is often useful to manipulate, enhance, or search the information in that list.

Some examples of things you might want to do with a list of data:

* Only use the first 10 items in a list
* Get people from a list whose name starts with a `M`
* Find the first person in a list to be over 100 years old
* Arrange people in a list alphabetically
* Get the last 10 items in an array
* Add all the numbers up in a list
* Get all the cats in an array of animals
* From a list of numbers, add a `£` sign prefix
* Combine a list of romance films and thrillers

## Array methods

Do you remember how strings have special functions called methods? Don't worry if not! Here's an example to jog your memory:

```
$ node
> let name = "Daniel";
undefined
> name.toLowerCase()
daniel
```

Arrays also have several methods that you can use.

#### `.sort()` <a href="#sort" id="sort"></a>

_An array method that sorts the values in an array into ascending alphabetical or numerical order._

```
const unorderedLetters = ["z", "v", "b", "f", "g"];
const orderedLetters = unorderedLetters.sort();

const unorderedNumbers = [8, 5, 1, 4, 2];
const orderedNumbers = unorderedNumbers.sort();

console.log(orderedLetters); // logs [ 'b', 'f', 'g', 'v', 'z' ]
console.log(unorderedLetters); // logs [ 'b', 'f', 'g', 'v', 'z' ]

console.log(orderedNumbers); // logs [ 1, 2, 4, 5, 8 ]
console.log(unorderedNumbers); // logs [ 1, 2, 4, 5, 8 ]
```

> When you call this array method it uses the array on the left side of the dot as an input, and it sorts that array also returning it. Note how both ordered and unordered arrays are sorted now!

#### `.concat()` <a href="#concat" id="concat"></a>

_Adds (or concatenates) another value or array to the array._

```
$ node
> let arr = [1, 2, 3];
undefined
> arr.concat(4)
[1, 2, 3, 4]
> arr
[1, 2, 3]
```

Did you notice how calling the concat method did not change `arr`? This is because `concat`, like most array methods, returns a _new_ array, it does not alter the one you called the method on.

If you want to use the array returned by calling `.concat()` you should store it in a new variable.

```
const arr = [1, 2, 3];
const newArr = arr.concat(4);

console.log(newArr); // logs [1, 2, 3, 4]
```

#### `.slice()` <a href="#slice" id="slice"></a>

_Returns a slice of the array._

You can tell `.slice()` where you want the slice to begin and end by passing it two parameters.

```
$ node
> let arr = [0, 1, 2, 3, 4]
undefined
> arr.slice(0, 2)
[0, 1]
> ["a", "b", "c", "d"].slice(1, 2)
['b']
```

#### `.includes()` <a href="#includes" id="includes"></a>

_Returns true if a value is in the array._

```
const mentors = ["Daniel", "Irini", "Ashleigh", "Rob", "Etzali"];

function isAMentor(name) {
  return mentors.includes(name);
}

console.log("Is Rukmuni a mentor?");
console.log(isAMentor("Rukmini")); // logs false
```

#### `.join()` <a href="#join" id="join"></a>

_Returns all the array values joined together in a string. By default, this method takes no parameters and then the elements are divided with a comma `,`. If you provide it with a string parameter though, then it becomes the divider of the elements, like the example below:_

```
$ node
> ["H", "e", "l", "l", "o"].join();
'H,e,l,l,o'
> ["H", "e", "l", "l", "o"].join("--");
'H--e--l--l--o'
```

There is a string method `.split()`. In an interactive console try using the string `.split()` method and the array `.join()`. How could they work together?

#### Exercise B (10 minutes) <a href="#exercise-b-10-minutes" id="exercise-b-10-minutes"></a>

* Use the array of the people from your class
* Combine it with another array filled with the names from another class
* `console.log` the names in alphabetical order
* Create a function that takes a `name` and an array of names and returns a string. If the name is not in an array, it should return `<name> is not at the class with <people in the array>`. If the name is in the array, it should return `<name> is at the class with <people in the array>`.

### Array map <a href="#array-map" id="array-map"></a>

Imagine you have an array of names...

```
const mentors = ["Daniel ", "irina ", " Gordon", "ashleigh "];
```

You notice that the names are not formatted consistently. To fix the array you decide you need to trim whitespace and convert to lowercase. How do you do that for every value in the array?

We can write a function that changes one name:

```
function tidy(name) {
  return name.trim().toLowerCase();
}
```

All you need to run every name in the array through this function and update the array values. Thankfully there is an array method that does just this!

#### `.map()` <a href="#map" id="map"></a>

_Runs every item in the array through a function and returns a new array with the values returned by the function_.

Have a look at this other example:

```
function double(number) {
  return number * 2;
}

const numbers = [1, 2, 3];
const numbersDoubled = numbers.map(double);
```

The `map()` method runs the function we provided (`double`) on each item in the array and uses the return values to create a new array. In the example `numbersDoubled` is a new array containing `[2, 4, 6]`.

#### Callback functions <a href="#callback-functions" id="callback-functions"></a>

A **callback function** is a function that is passed _as an argument_ to another function, to be “called back” at a later time. . The term highlights that although we _provide_ the `double` function, the `.map()` method _calls_ it. (Notice how we never write `double()` to call the function).

We'll see callback functions used a lot more in the coming weeks.

Often, when a function is only needed for a map operation, developers will declare the callback function inside of the method call. Let's try copying and pasting the function declaration inside of the `.map()` method call.

```
const numbers = [1, 2, 3];
const numbersDoubled = numbers.map(function double(number) {
  return number * 2;
});
```

We can make this shorter by removing the function name to declare an _anonymous function_. We can do this because we are not using the function anywhere else in the code, so we do not need the function name to reference it.

```
const numbers = [1, 2, 3];
const numbersDoubled = numbers.map(function (number) {
  return number * 2;
});
```

We can make this code even shorter still. In the latest versions of JavaScript a way of declaring functions was introduced called _arrow functions_.

```
const numbers = [1, 2, 3];
const numbersDoubled = numbers.map((number) => {
  return number * 2;
});
```

The arrow function syntax lets you declare a function without the `function` keyword. (There are some other subtle differences between arrow functions and regular functions that you will learn about at a much later stage).

There is one last thing you can do to make your code shorter. If you remove the braces (`{}`) from an arrow function, the body of the function will be returned without needing to write the `return` keyword.

```
const numbers = [1, 2, 3];
const numbersDoubled = numbers.map((number) => number * 2);
```

In the example above, the expression `number * 2` is automatically returned because it comes directly after the `=>` arrow (instead of coming after curly braces). This is called an `implicit return`.

#### Exercise C (10 minutes) <a href="#exercise-c-10-minutes" id="exercise-c-10-minutes"></a>

I have a function defined below as:

```
function magician(yourFunc) {
  console.log(
    "I am magician! Watch as I mutate an array of strings to your heart's content!"
  );
  const namesArray = [
    "James",
    "Elamin",
    "Ismael",
    "Sanyia",
    "Chris",
    "Antigoni",
  ];

  const magicOutput = yourFunc(namesArray);

  return magicOutput;
}
```

This function does not need to be modified. Can you pass in a _callback function_ which will mutate `namesArray` such that it:

* Upper cases all letters in the array

#### Exercise D <a href="#exercise-d" id="exercise-d"></a>

Modify your callback function from the previous exercise so that it also:

* sorts  `namesArray` in alphabetical order

### Array forEach <a href="#array-foreach" id="array-foreach"></a>

The `.forEach()` method is similar to `.map()` except it does not return a new array.&#x20;

#### `.forEach()` <a href="#foreach" id="foreach"></a>

Say we want to log to the console a list of names.

```
const names = ["Daniel", "mozafar", "irina"];
```

We can use `.forEach()` to go through the array, item by item, and call a function we provide.

```
names.forEach(function (name, index) {
  console.log(index + ": " + name);
});
```

#### &#x20;<a href="#exercise-e-10-minutes" id="exercise-e-10-minutes"></a>

#### Exercise E (10 minutes) <a href="#exercise-e-10-minutes" id="exercise-e-10-minutes"></a>

* Create a function that takes a `birthYear`, and returns the age of someone
* You are given an array with year that 7 people were born, `[1964, 2008, 1999, 2005, 1978, 1985, 1919]`. Take this array and create another array containing their ages.
* `console.log` the birth years array



#### Exercise F (5 minutes) <a href="#exercise-f-5-minutes" id="exercise-f-5-minutes"></a>

You can drive in the UK at the age of 17.

* Write another function that takes a birth year and returns a string `Born in {year} can drive` or `Born in {year} can drive in {x} years`
* Use the array of birth years, `[ 1964, 2008, 1999, 2005, 1978, 1985, 1919 ]`, to get an array of strings saying if these people can drive
* `console.log` the answers

### Array filter <a href="#array-filter" id="array-filter"></a>

Imagine you have an array of students' test scores:

```
const testScores = [90, 50, 100, 66, 25, 80, 81];
```

You want to show only the test scores that are higher than 80. How do you do that for every value in the array?

We can write a function that checks if one score is greater than 80:

```
function isHighScore(score) {
  return score > 80;
}
```

To find out which scores were greater than 80, you'd have to run this function against every score in the array, and push the 80+ scores into a new array. Thankfully there is an array method that does just this!

#### `.filter()` <a href="#filter" id="filter"></a>

_Runs every item in the array through a condition that we set, and returns a new array with the values that match the condition_.

```
const highTestScores = testScores.filter(isHighScore);

console.log(highTestScores); // logs [90, 100, 81]
```

#### Exercise G (10 mins) <a href="#exercise-g-10-mins" id="exercise-g-10-mins"></a>

Create a function which:

* Takes an array of `birthYears`
* Uses `console.log` to print the message `These are the birth years of people who can drive: <filtered birth years>`
* Returns an array of people who can drive (remember, you can drive if you are 17 years or older)

### Array find <a href="#array-find" id="array-find"></a>

Imagine you have an array of names:

```
const names = ["Daniel", "James", "Irina", "Mozafar", "Ashleigh"];
```

How would you find the first name that's longer than 6 characters?

You can write a predicate function that checks if a string is longer than 6 characters:

```
function isLongName(name) {
  return name.length > 6;
}
```

To find the first item that satisfies the predicate you would have to go through each array item, and pass it into `isLongName`. Once it returns true, we can stop going through the array and grab the item that passed the predicate's test. Sounds complicated! Thankfully there is an array method that does just this!

#### `.find()` <a href="#find" id="find"></a>

_Searches through the array and returns the value of the first item that satisfies a predicate function._

```
const longName = names.find(isLongName);

console.log(longName); // logs Mozafar
```

#### Exercise H (10 mins) <a href="#exercise-h-10-mins" id="exercise-h-10-mins"></a>

Create a function which:

* Takes an array of names
* Looks to see if your name is in the array
* If it is, return `Found me!`; if not, return `Haven't found me :(`

#### Chaining <a href="#chaining" id="chaining"></a>

Notice how we were able to write one method after another e.g. `names.map(formatName).forEach(log)`? This is called _method chaining_.

You can call `.forEach()` after `.map()` because `.map()` returns a new array.

Consider this code:

```
function formatName(name) {
  return name.split("")[0].toUpperCase() + name.slice(1);
}

function log(name, index) {
  console.log(index + ": " + name);
}

const namesFormatted = names.map(formatName);
namesFormatted.forEach(log);
```

It can be written more simply (without assigning the array returned from `.map()` to a variable):

```
names.map(formatName).forEach(log);
```

Be careful though! You can not call `.map()` after `.forEach`.

```
names.forEach(log).map(formatName); // ERROR
```

This code does not work because `forEach()` does not return a new array (it returns `undefined`). The code is therefore attempting to call `.map()` on `undefined`, and `undefined` does not have a `.map()` method.

#### Exercise I (15 minutes) <a href="#exercise-i-15-minutes" id="exercise-i-15-minutes"></a>

Create a function which accepts an array of "messy" strings. Example:

```
[
  100,
  "iSMael",
  55,
  45,
  "sANyiA",
  66,
  "JaMEs",
  "eLAmIn",
  23,
  "IsMael",
  67,
  19,
  "ElaMIN",
];
```

This function should:

* Remove all non-string entries
* Change the strings to upper case, and add an exclamation mark to the end

If you're using the above example, you should expect to return an array with 2x `ELAMIN!`, 1x `SANYIA!`, 2x `ISMAEL!` and 1x `JAMES!`.

