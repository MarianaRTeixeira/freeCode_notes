# <u>ES6</u>

## Testing Objects for Properties

It is useful to check if the property of a given object exists or not. We can use the `.hasOwnProperty(propname)` method of objects to determine if that object has the given property name. `.hasOwnProperty()` returns `true` or `false` if the property is found or not.

## Record Collection

You are given an object literal representing a part of your musical album collection. Each album has a unique id number as its key and several other properties. Not all albums have complete information.

You start with an `updateRecords` function that takes an object literal, `records`, containing the musical album collection, an `id`, a `prop` (like `artist` or `tracks`), and a `value`. Complete the function using the rules below to modify the object passed to the function.

- Your function must always return the entire record collection object.
- If `prop` isn't `tracks` and `value` isn't an empty string, update or set that album's `prop` to `value`.
- If `prop` is `tracks` but the album doesn't have a `tracks` property, create an empty array and add `value` to it.
- If `prop` is `tracks` and `value` isn't an empty string, add `value` to the end of the album's existing `tracks` array.
- If `value` is an empty string, delete the given `prop` property from the album.

**Note:** A copy of the `recordCollection` object is used for the tests.

------

After `updateRecords(recordCollection, 5439, "artist", "ABBA")`, `artist` should be the string `ABBA`

After `updateRecords(recordCollection, 5439, "tracks", "Take a Chance on Me")`, `tracks` should have the string `Take a Chance on Me` as the last element.

After `updateRecords(recordCollection, 2548, "artist", "")`, `artist` should not be set

After `updateRecords(recordCollection, 1245, "tracks", "Addicted to Love")`, `tracks` should have the string `Addicted to Love` as the last element.

After `updateRecords(recordCollection, 2468, "tracks", "Free")`, `tracks` should have the string `1999` as the first element.

After `updateRecords(recordCollection, 2548, "tracks", "")`, `tracks` should not be setAfter `updateRecords(recordCollection, 1245, "albumTitle", "Riptide")`, `albumTitle` should be the string `Riptide`

```js
// Setup
const recordCollection = {
  2548: {
    albumTitle: 'Slippery When Wet',
    artist: 'Bon Jovi',
    tracks: ['Let It Rock', 'You Give Love a Bad Name']
  },
  2468: {
    albumTitle: '1999',
    artist: 'Prince',
    tracks: ['1999', 'Little Red Corvette']
  },
  1245: {
    artist: 'Robert Palmer',
    tracks: []
  },
  5439: {
    albumTitle: 'ABBA Gold'
  }
};

// Only change code below this line
function updateRecords(records, id, prop, value) {
  if(prop !=='tracks' && value!==''){
    records[id][prop] = value;
  } else if(prop === 'tracks' && records[id].hasOwnProperty('tracks') === false){
    records[id][prop] = [value]
  } else if( prop === 'tracks' && value !== '') {
    records[id][prop].push(value);
  } else if( value === '') {
    delete records[id][prop];
  }
  return records;
}

updateRecords(recordCollection, 5439, 'artist', 'ABBA');
```

------

## Replace Loops using Recursion

Recursion is the concept that a function can be expressed in terms of itself. To help understand this, start by thinking about the following task: multiply the first `n` elements of an array to create the product of those elements. Using a `for` loop, you could do this:

```js
  function multiply(arr, n) {
    let product = 1;
    for (let i = 0; i < n; i++) {
      product *= arr[i];
    }
    return product;
  }
```

However, notice that `multiply(arr, n) == multiply(arr, n - 1) * arr[n - 1]`. That means you can rewrite `multiply` in terms of itself and never need to use a loop.

```js
  function multiply(arr, n) {
    if (n <= 0) {
      return 1;
    } else {
      return multiply(arr, n - 1) * arr[n - 1];
    }
  }
```

The recursive version of `multiply` breaks down like this. In the base case, where `n <= 0`, it returns 1. For larger values of `n`, it calls itself, but with `n - 1`. That function call is evaluated in the same way, calling `multiply` again until `n <= 0`. At this point, all the functions can return and the original `multiply` returns the answer.

**Note:** Recursive functions must have a base case when they return without calling the function again (in this example, when `n <= 0`), otherwise they can never finish executing.

------

Write a recursive function, `sum(arr, n)`, that returns the sum of the first `n` elements of an array `arr`.

- `sum([1], 0)` should equal 0.

- `sum([2, 3, 4], 1)` should equal 2.

- `sum([2, 3, 4, 5], 3)` should equal 9.

Your code should not rely on any kind of loops (`for` or `while` or higher order functions such as `forEach`, `map`, `filter`, or `reduce`.).You should use recursion to solve this problem.

```js
function sum(arr, n) {
  if(n <= 0) {
    return 0;
  } else {
    return sum(arr, n - 1) + arr[n - 1];
  }
}
```

------

## Profile Lookup

We have an array of objects representing different people in our contacts lists.

A `lookUpProfile` function that takes `name` and a property (`prop`) as arguments has been pre-written for you.

The function should check if `name` is an actual contact's `firstName` and the given property (`prop`) is a property of that contact.

If both are true, then return the "value" of that property.

If `name` does not correspond to any contacts then return the string `No such contact`.

If `prop` does not correspond to any valid properties of a contact found to match `name` then return the string `No such property`.

```js
// Setup
const contacts = [
  {
    firstName: "Akira",
    lastName: "Laine",
    number: "0543236543",
    likes: ["Pizza", "Coding", "Brownie Points"],
  },
  {
    firstName: "Harry",
    lastName: "Potter",
    number: "0994372684",
    likes: ["Hogwarts", "Magic", "Hagrid"],
  },
  {
    firstName: "Sherlock",
    lastName: "Holmes",
    number: "0487345643",
    likes: ["Intriguing Cases", "Violin"],
  },
  {
    firstName: "Kristian",
    lastName: "Vos",
    number: "unknown",
    likes: ["JavaScript", "Gaming", "Foxes"],
  },
];

function lookUpProfile(name, prop) {
  // Only change code below this line
for (let x = 0; x < contacts.length; x++) {
    if (contacts[x].firstName === name) {
      if (contacts[x].hasOwnProperty(prop)) {
        return contacts[x][prop];
      } else {
        return "No such property";
      }
    }
  } 
  return "No such contact"
  // Only change code above this line
}

lookUpProfile("Akira", "likes");
```

------

## Generate Random Whole Numbers within a Range

Instead of generating a random whole number between zero and a given number like we did before, we can generate a random whole number that falls within a range of two specific numbers.

To do this, we'll define a minimum number `min` and a maximum number `max`.

Here's the formula we'll use. Take a moment to read it and try to understand what this code is doing:

```js
Math.floor(Math.random() * (max - min + 1)) + min
```

------

Create a function called `randomRange` that takes a range `myMin` and `myMax` and returns a random whole number that's greater than or equal to `myMin`, and is less than or equal to `myMax`, inclusive.

```js
function randomRange(myMin, myMax) {
  // Only change code below this line
  return Math.floor(Math.random() * (myMax - myMin + 1) + myMin);
  // Only change code above this line
}
```

------

## Use the parseInt Function with a Radix

The `parseInt()` function parses a string and returns an integer. It takes a second argument for the radix, which specifies the base of the number in the string. The radix can be an integer between 2 and 36.

The function call looks like:

```js
parseInt(string, radix);
```

And here's an example:

```js
const a = parseInt("11", 2);
```

The radix variable says that `11` is in the binary system, or base 2. This example converts the string `11` to an integer `3`.

------

Use `parseInt()` in the `convertToInteger` function so it converts a binary number to an integer and returns it.

```js
function convertToInteger(str) {
return parseInt(str, 2)
}

convertToInteger("10011");
```

------

## Use the Conditional (Ternary) Operator

The conditional operator, also called the ternary operator, can be used as a one line if-else expression.

The syntax is `a ? b : c`, where `a` is the condition, `b` is the code to run when the condition returns `true`, and `c` is the code to run when the condition returns `false`.

The following function uses an `if/else` statement to check a condition:

```js
function findGreater(a, b) {
  if(a > b) {
    return "a is greater";
  }
  else {
    return "b is greater or equal";
  }
}
```

This can be re-written using the conditional operator:

```js
function findGreater(a, b) {
  return a > b ? "a is greater" : "b is greater or equal";
}
```

------

Use the conditional operator in the `checkEqual` function to check if two numbers are equal or not. The function should return either the string `Equal` or the string `Not Equal`

```js
function checkEqual(a, b) {
return a === b ? "Equal" : "Not Equal"
}

checkEqual(1, 2);
```

------



## Use Recursion to Create a Countdown

In a [previous challenge](https://www.freecodecamp.org/learn/javascript-algorithms-and-data-structures/basic-javascript/replace-loops-using-recursion), you learned how to use recursion to replace a `for` loop. Now, let's look at a more complex function that returns an array of consecutive integers starting with `1` through the number passed to the function.

As mentioned in the previous challenge, there will be a base case. The base case tells the recursive function when it no longer needs to call itself. It is a simple case where the return value is already known. There will also be a recursive call which executes the original function with different arguments. If the function is written correctly, eventually the base case will be reached.

For example, say you want to write a recursive function that returns an array containing the numbers `1` through `n`. This function will need to accept an argument, `n`, representing the final number. Then it will need to call itself with progressively smaller values of `n` until it reaches `1`. You could write the function as follows:

```javascript
function countup(n) {
  if (n < 1) {
    return [];
  } else {
    const countArray = countup(n - 1);
    countArray.push(n);
    return countArray;
  }
}
console.log(countup(5));
```

The value `[1, 2, 3, 4, 5]` will be displayed in the console.

At first, this seems counterintuitive since the value of `n` *decreases*, but the values in the final array are *increasing*. This happens because the push happens last, after the recursive call has returned. At the point where `n` is pushed into the array, `countup(n - 1)` has already been evaluated and returned `[1, 2, ..., n - 1]`.

------

We have defined a function called `countdown` with one parameter (`n`). The function should use recursion to return an array containing the integers `n` through `1` based on the `n` parameter. If the function is called with a number less than 1, the function should return an empty array. For example, calling this function with `n = 5` should return the array `[5, 4, 3, 2, 1]`. Your function must use recursion by calling itself and must not use loops of any kind.

- `countdown(-1)` should return an empty array.

- countdown(10)` should return `[10, 9, 8, 7, 6, 5, 4, 3, 2, 1]
- countdown(5)` should return `[5, 4, 3, 2, 1]
- Your code should not rely on any kind of loops (`for`, `while` or higher order functions such as `forEach`, `map`, `filter`, and `reduce`).
- You should use recursion to solve this problem.

```js
function countdown(n){
  if(n < 1){
    return [];
  } else {
    const array = countdown (n-1);
    array.unshift(n);
    return array
  }
}
```

------

## Use Recursion to Create a Range of Numbers

Continuing from the previous challenge, we provide you another opportunity to create a recursive function to solve a problem.

------

We have defined a function named `rangeOfNumbers` with two parameters. The function should return an array of integers which begins with a number represented by the `startNum` parameter and ends with a number represented by the `endNum` parameter. The starting number will always be less than or equal to the ending number. Your function must use recursion by calling itself and not use loops of any kind. It should also work for cases where both `startNum` and `endNum` are the same.

------

```js
function rangeOfNumbers(startNum, endNum) {
  if (endNum - startNum === 0) {
    return [startNum];
  } else {
    var numbers = rangeOfNumbers(startNum, endNum - 1);
    numbers.push(endNum);
    return numbers;
  }
}
```



------

------

------


Search 8,000+ tutorials





Menu

[JavaScript Algorithms and Data Structures](https://www.freecodecamp.org/learn/javascript-algorithms-and-data-structures)[ES6](https://www.freecodecamp.org/learn/javascript-algorithms-and-data-structures/#es6)

## Prevent Object Mutation

As seen in the previous challenge, `const` declaration alone doesn't really protect your data from mutation. To ensure your data doesn't change, JavaScript provides a function `Object.freeze` to prevent data mutation.

Any attempt at changing the object will be rejected, with an error thrown if the script is running in strict mode.

```js
let obj = {
  name:"FreeCodeCamp",
  review:"Awesome"
};
Object.freeze(obj);
obj.review = "bad";
obj.newProp = "Test";
console.log(obj); 
```

The `obj.review` and `obj.newProp` assignments will result in errors, because our editor runs in strict mode by default, and the console will display the value `{ name: "FreeCodeCamp", review: "Awesome" }`.

------

In this challenge you are going to use `Object.freeze` to prevent mathematical constants from changing. You need to freeze the `MATH_CONSTANTS` object so that no one is able to alter the value of `PI`, add, or delete properties.



```js
function freezeObj() {
  const MATH_CONSTANTS = {
    PI: 3.14
  };
  // Only change code below this line
Object.freeze(MATH_CONSTANTS)

  // Only change code above this line
  try {
    MATH_CONSTANTS.PI = 99;
  } catch(ex) {
    console.log(ex);
  }
  return MATH_CONSTANTS.PI;
}
const PI = freezeObj();
```

------

## Profile Lookup



We have an array of objects representing different people in our contacts lists.

A `lookUpProfile` function that takes `name` and a property (`prop`) as arguments has been pre-written for you.

The function should check if `name` is an actual contact's `firstName` and the given property (`prop`) is a property of that contact.

If both are true, then return the "value" of that property.

If `name` does not correspond to any contacts then return the string `No such contact`.

If `prop` does not correspond to any valid properties of a contact found to match `name` then return the string `No such property`.

```js
// Setup
const contacts = [
  {
    firstName: "Akira",
    lastName: "Laine",
    number: "0543236543",
    likes: ["Pizza", "Coding", "Brownie Points"],
  },
  {
    firstName: "Harry",
    lastName: "Potter",
    number: "0994372684",
    likes: ["Hogwarts", "Magic", "Hagrid"],
  },
  {
    firstName: "Sherlock",
    lastName: "Holmes",
    number: "0487345643",
    likes: ["Intriguing Cases", "Violin"],
  },
  {
    firstName: "Kristian",
    lastName: "Vos",
    number: "unknown",
    likes: ["JavaScript", "Gaming", "Foxes"],
  },
];

function lookUpProfile(name, prop) {
  // Only change code below this line
    for ( let i=0 ; i< contacts.length; i++){
      if(contacts[i].firstName === name){
          return contacts[i][prop] || "No such property";
      }
    }
    return "No such contact"
  // Only change code above this line
}

var data = lookUpProfile("Kristian", "number");
console.log(data)
```

------

## Use Destructuring Assignment to Assign Variables from Nested Objects



You can use the same principles from the previous two lessons to destructure values from nested objects.

Using an object similar to previous examples:

```js
const user = {
  johnDoe: { 
    age: 34,
    email: 'johnDoe@freeCodeCamp.com'
  }
};
```

Here's how to extract the values of object properties and assign them to variables with the same name:

```js
const { johnDoe: { age, email }} = user;
```

And here's how you can assign an object properties' values to variables with different names:

```js
const { johnDoe: { age: userAge, email: userEmail }} = user;
```

------

Replace the two assignments with an equivalent destructuring assignment. It should still assign the variables `lowToday` and `highToday` the values of `today.low` and `today.high` from the `LOCAL_FORECAST` object.

```js
const LOCAL_FORECAST = {
  yesterday: { low: 61, high: 75 },
  today: { low: 64, high: 77 },
  tomorrow: { low: 68, high: 80 }
};

// Only change code below this line
/*   
const lowToday = LOCAL_FORECAST.today.low;
const highToday = LOCAL_FORECAST.today.high; */
const { today : { low: lowToday , high: highToday}} = LOCAL_FORECAST;

// Only change code above this line
```

------

## Use Destructuring Assignment to Assign Variables from Arrays

ES6 makes destructuring arrays as easy as destructuring objects.

One key difference between the spread operator and array destructuring is that the spread operator unpacks all contents of an array into a comma-separated list. Consequently, you cannot pick or choose which elements you want to assign to variables.

Destructuring an array lets us do exactly that:

```js
const [a, b] = [1, 2, 3, 4, 5, 6];
console.log(a, b);
```

The console will display the values of `a` and `b` as `1, 2`.

The variable `a` is assigned the first value of the array, and `b` is assigned the second value of the array. We can also access the value at any index in an array with destructuring by using commas to reach the desired index:

```js
const [a, b,,, c] = [1, 2, 3, 4, 5, 6];
console.log(a, b, c);
```

The console will display the values of `a`, `b`, and `c` as `1, 2, 5`.

------

Use destructuring assignment to swap the values of `a` and `b` so that `a` receives the value stored in `b`, and `b` receives the value stored in `a`.

```js
let a = 8, b = 6;
// Only change code below this line
[a,b]=[b,a]
console.log(a)
```

------

## Use Destructuring Assignment with the Rest Parameter to Reassign Array Elements

In some situations involving array destructuring, we might want to collect the rest of the elements into a separate array.

The result is similar to `Array.prototype.slice()`, as shown below:

```js
const [a, b, ...arr] = [1, 2, 3, 4, 5, 7];
console.log(a, b);
console.log(arr);
```

The console would display the values `1, 2` and `[3, 4, 5, 7]`.

Variables `a` and `b` take the first and second values from the array. After that, because of the rest parameter's presence, `arr` gets the rest of the values in the form of an array. The rest element only works correctly as the last variable in the list. As in, you cannot use the rest parameter to catch a subarray that leaves out the last element of the original array.

------

Use destructuring assignment with the rest parameter to perform an effective `Array.prototype.slice()` so that `arr` is a sub-array of the original array `source` with the first two elements omitted.

```js
const source = [1,2,3,4,5,6,7,8,9,10];
function removeFirstTwo(list) {
  // Only change code below this line
  const [a, b, ...arr] = list; // Change this line
  // Only change code above this line
  return arr;
}
const arr = removeFirstTwo(source);
console.log(arr)
```

------

## Use Destructuring Assignment to Pass an Object as a Function's Parameters

In some cases, you can destructure the object in a function argument itself.

Consider the code below:

```js
const profileUpdate = (profileData) => {
  const { name, age, nationality, location } = profileData;

}
```

This effectively destructures the object sent into the function. This can also be done in-place:

```js
const profileUpdate = ({ name, age, nationality, location }) => {

}
```

When `profileData` is passed to the above function, the values are destructured from the function parameter for use within the function.

------

Use destructuring assignment within the argument to the function `half` to send only `max` and `min` inside the function.

```js
const stats = {
  max: 56.78,
  standard_deviation: 4.34,
  median: 34.54,
  mode: 23.87,
  min: -0.75,
  average: 35.85
};

// Only change code below this line
//const half = (stats) => (stats.max + stats.min) / 2.0; 
const half = ({min, max}) => (max + min) / 2.0;
console.log(half(stats))
// Only change code above this line

```

------

## Create Strings using Template Literals

A new feature of ES6 is the template literal. This is a special type of string that makes creating complex strings easier.

Template literals allow you to create multi-line strings and to use string interpolation features to create strings.

Consider the code below:

```js
const person = {
  name: "Zodiac Hasbro",
  age: 56
};

const greeting = `Hello, my name is ${person.name}!
I am ${person.age} years old.`;

console.log(greeting);
```

The console will display the strings `Hello, my name is Zodiac Hasbro!` and `I am 56 years old.`.

A lot of things happened there. Firstly, the example uses backticks (```), not quotes (`'` or `"`), to wrap the string. Secondly, notice that the string is multi-line, both in the code and the output. This saves inserting `\n` within strings. The  {variable} syntax used above is a placeholder. Basically, you won't have to use concatenation with the + operator anymore. To add variables to strings, you just drop the variable in a template string and wrap it with { and }. Similarly, you can include other expressions in your string literal, for example ${a + b}. This new way of creating strings gives you more flexibility to create robust strings.

------

Use template literal syntax with backticks to create an array of list element (`li`) strings. Each list element's text should be one of the array elements from the `failure` property on the `result` object and have a `class` attribute with the value `text-warning`. The `makeList` function should return the array of list item strings.

Use an iterator method (any kind of loop) to get the desired output (shown below).

```js
[
  '<li class="text-warning">no-var</li>',
  '<li class="text-warning">var-on-top</li>',
  '<li class="text-warning">linebreak</li>'
]
```

------

```js
const result = {
  success: ["max-length", "no-amd", "prefer-arrow-functions"],
  failure: ["no-var", "var-on-top", "linebreak"],
  skipped: ["no-extra-semi", "no-dup-keys"]
};
function makeList(arr) {
  "use strict";
  // change code below this line
  const failureItems = [];
  for (let i = 0; i < arr.length; i++) {
    failureItems.push(`<li class="text-warning">${arr[i]}</li>`);
  }
  // change code above this line
  return failureItems;
}

const failuresList = makeList(result.failure);
```

------

## Write Concise Object Literal Declarations Using Object Property Shorthand

ES6 adds some nice support for easily defining object literals.

Consider the following code:

```js
const getMousePosition = (x, y) => ({
  x: x,
  y: y
});
```

`getMousePosition` is a simple function that returns an object containing two properties. ES6 provides the syntactic sugar to eliminate the redundancy of having to write `x: x`. You can simply write `x` once, and it will be converted to`x: x` (or something equivalent) under the hood. Here is the same function from above rewritten to use this new syntax:

```js
const getMousePosition = (x, y) => ({ x, y });
```

------

Use object property shorthand with object literals to create and return an object with `name`, `age` and `gender` properties.

```js
const createPerson = (name, age, gender) => {
  // Only change code below this line
  return({
    name,
    age,
    gender
  }); 
  // Only change code above this line
};
```

------

## Write Concise Declarative Functions with ES6

When defining functions within objects in ES5, we have to use the keyword `function` as follows:

```js
const person = {
  name: "Taylor",
  sayHello: function() {
    return `Hello! My name is ${this.name}.`;
  }
};
```

With ES6, you can remove the `function` keyword and colon altogether when defining functions in objects. Here's an example of this syntax:

```js
const person = {
  name: "Taylor",
  sayHello() {
    return `Hello! My name is ${this.name}.`;
  }
};
```

------

Refactor the function `setGear` inside the object `bicycle` to use the shorthand syntax described above.

```js
// Only change code below this line
const bicycle = {
  gear: 2,
  //setGear: function(newGear) {
   setGear (newGear) {
    this.gear = newGear;
  }
};
// Only change code above this line
bicycle.setGear(3);
console.log(bicycle.gear);
```

------

## Use class Syntax to Define a Constructor Function

ES6 provides a new syntax to create objects, using the class keyword.

It should be noted that the `class` syntax is just syntax, and not a full-fledged class-based implementation of an object-oriented paradigm, unlike in languages such as Java, Python, Ruby, etc.

In ES5, we usually define a `constructor` function and use the `new` keyword to instantiate an object.

```js
var SpaceShuttle = function(targetPlanet){
  this.targetPlanet = targetPlanet;
}
var zeus = new SpaceShuttle('Jupiter');
```

The `class` syntax simply replaces the `constructor` function creation:

```js
class SpaceShuttle {
  constructor(targetPlanet) {
    this.targetPlanet = targetPlanet;
  }
}
const zeus = new SpaceShuttle('Jupiter');
```

It should be noted that the `class` keyword declares a new function, to which a constructor is added. This constructor is invoked when `new` is called to create a new object.

**Note:** UpperCamelCase should be used by convention for ES6 class names, as in `SpaceShuttle` used above.

The `constructor` method is a special method for creating and initializing an object created with a class. You will learn more about it in the Object Oriented Programming section of the JavaScript Algorithms And Data Structures Certification.

------

Use the `class` keyword and write a `constructor` to create the `Vegetable` class.

The `Vegetable` class allows you to create a vegetable object with a property `name` that gets passed to the `constructor`.

```js
// Only change code below this line
class Vegetable  {
  constructor(name) {
    this.name = name;
  }
  
}
// Only change code above this line

const carrot = new Vegetable('carrot');
console.log(carrot.name); // Should display 'carrot'
```

------

## Use getters and setters to Control Access to an Object

You can obtain values from an object and set the value of a property within an object.

These are classically called getters and setters.

Getter functions are meant to simply return (get) the value of an object's private variable to the user without the user directly accessing the private variable.

Setter functions are meant to modify (set) the value of an object's private variable based on the value passed into the setter function. This change could involve calculations, or even overwriting the previous value completely.

```js
class Book {
  constructor(author) {
    this._author = author;
  }
  // getter
  get writer() {
    return this._author;
  }
  // setter
  set writer(updatedAuthor) {
    this._author = updatedAuthor;
  }
}
const novel = new Book('anonymous');
console.log(novel.writer);
novel.writer = 'newAuthor';
console.log(novel.writer);
```

The console would display the strings `anonymous` and `newAuthor`.

Notice the syntax used to invoke the getter and setter. They do not even look like functions. Getters and setters are important because they hide internal implementation details.

**Note:** It is convention to precede the name of a private variable with an underscore (`_`). However, the practice itself does not make a variable private.

------

Use the `class` keyword to create a `Thermostat` class. The `constructor` accepts a Fahrenheit temperature.

In the class, create a `getter` to obtain the temperature in Celsius and a `setter` to set the temperature in Celsius.

Remember that `C = 5/9 * (F - 32)` and `F = C * 9.0 / 5 + 32`, where `F` is the value of temperature in Fahrenheit, and `C` is the value of the same temperature in Celsius.

**Note:** When you implement this, you will track the temperature inside the class in one scale, either Fahrenheit or Celsius.

This is the power of a getter and a setter. You are creating an API for another user, who can get the correct result regardless of which one you track.

In other words, you are abstracting implementation details from the user.

------

```js
// Only change code below this line
class Thermostat {
  
  constructor(fahrenheit) {
    this.fahrenheit = fahrenheit;
    }
  get temperature(){
    return (5/9) * (this.fahrenheit - 32);
  	}

  set temperature(celsius){
      this.fahrenheit = (celsius * 9) / 5+32
  	}
	}
// Only change code above this line

const thermos = new Thermostat(76); // Setting in Fahrenheit scale
let temp = thermos.temperature; // 24.44 in Celsius
thermos.temperature = 26;
temp = thermos.temperature; // 26 in Celsius
```

------

## Use * to Import Everything from a File

Suppose you have a file and you wish to import all of its contents into the current file. This can be done with the `import * as` syntax. Here's an example where the contents of a file named `math_functions.js` are imported into a file in the same directory:

```js
import * as myMathModule from "./math_functions.js";
```

The above `import` statement will create an object called `myMathModule`. This is just a variable name, you can name it anything. The object will contain all of the exports from `math_functions.js` in it, so you can access the functions like you would any other object property. Here's how you can use the `add` and `subtract` functions that were imported:

```js
myMathModule.add(2,3);
myMathModule.subtract(5,3);
```

------

The code in this file requires the contents of the file: `string_functions.js`, that is in the same directory as the current file. Use the `import * as` syntax to import everything from the file into an object called `stringFunctions`.

```js
import * as stringFunctions from './string_functions.js';
// Only change code above this line

stringFunctions.uppercaseString("hello");
stringFunctions.lowercaseString("WORLD!");
```

------

## Create an Export Fallback with export default

In the `export` lesson, you learned about the syntax referred to as a named export. This allowed you to make multiple functions and variables available for use in other files.

There is another `export` syntax you need to know, known as export default. Usually you will use this syntax if only one value is being exported from a file. It is also used to create a fallback value for a file or module.

Below are examples using `export default`:

```js
export default function add(x, y) {
  return x + y;
}

export default function(x, y) {
  return x + y;
}
```

The first is a named function, and the second is an anonymous function.

Since `export default` is used to declare a fallback value for a module or file, you can only have one value be a default export in each module or file. Additionally, you cannot use `export default` with `var`, `let`, or `const`

------

The following function should be the fallback value for the module. Please add the necessary code to do so.

```js
export default function subtract(x, y) {
  return x - y;
}
```

------

## Create a JavaScript Promise

A promise in JavaScript is exactly what it sounds like - you use it to make a promise to do something, usually asynchronously. When the task completes, you either fulfill your promise or fail to do so. `Promise` is a constructor function, so you need to use the `new` keyword to create one. It takes a function, as its argument, with two parameters - `resolve` and `reject`. These are methods used to determine the outcome of the promise. The syntax looks like this:

```js
const myPromise = new Promise((resolve, reject) => {

});
```

------

Create a new promise called `makeServerRequest`. Pass in a function with `resolve` and `reject` parameters to the constructor.

```js
const makeServerRequest = new Promise ((resolve, reject) => {

});
```

## Complete a Promise with resolve and reject

A promise has three states: `pending`, `fulfilled`, and `rejected`. The promise you created in the last challenge is forever stuck in the `pending` state because you did not add a way to complete the promise. The `resolve` and `reject` parameters given to the promise argument are used to do this. `resolve` is used when you want your promise to succeed, and `reject` is used when you want it to fail. These are methods that take an argument, as seen below.

```js
const myPromise = new Promise((resolve, reject) => {
  if(condition here) {
    resolve("Promise was fulfilled");
  } else {
    reject("Promise was rejected");
  }
});
```

The example above uses strings for the argument of these functions, but it can really be anything. Often, it might be an object, that you would use data from, to put on your website or elsewhere.

------

Make the promise handle success and failure. If `responseFromServer` is `true`, call the `resolve` method to successfully complete the promise. Pass `resolve` a string with the value `We got the data`. If `responseFromServer` is `false`, use the `reject` method instead and pass it the string: `Data not received`.

```js
const makeServerRequest = new Promise((resolve, reject) => {
  // responseFromServer represents a response from a server
  let responseFromServer;
    
  if(responseFromServer) {
    // Change this line
    resolve(' We got the data')
  } else {  
    // Change this line
    reject ('Data not received')
  }
});
```

------

## Handle a Fulfilled Promise with then

Promises are most useful when you have a process that takes an unknown amount of time in your code (i.e. something asynchronous), often a server request. When you make a server request it takes some amount of time, and after it completes you usually want to do something with the response from the server. This can be achieved by using the `then` method. The `then` method is executed immediately after your promise is fulfilled with `resolve`. Here’s an example:

```js
myPromise.then(result => {
  
});
```

`result` comes from the argument given to the `resolve` method.

------

Add the `then` method to your promise. Use `result` as the parameter of its callback function and log `result` to the console.

```js
const makeServerRequest = new Promise((resolve, reject) => {
  // responseFromServer is set to true to represent a successful response from a server
  let responseFromServer = true;
    
  if(responseFromServer) {
    resolve("We got the data");
  } else {  
    reject("Data not received");
  }
});
makeServerRequest.then(result => {
  console.log(result)
});
```

------

## Handle a Rejected Promise with catch

`catch` is the method used when your promise has been rejected. It is executed immediately after a promise's `reject` method is called. Here’s the syntax:

```js
myPromise.catch(error => {
  
});
```

`error` is the argument passed in to the `reject` method.

------

Add the `catch` method to your promise. Use `error` as the parameter of its callback function and log `error` to the console.

```js
const makeServerRequest = new Promise((resolve, reject) => {
  // responseFromServer is set to false to represent an unsuccessful response from a server
  let responseFromServer = false;
    
  if(responseFromServer) {
    resolve("We got the data");
  } else {  
    reject("Data not received");
  }
});

makeServerRequest.then(result => {
  console.log(result);
});
makeServerRequest.catch(error => {
  console.log(error)
})
```

------

------

------

# <u>Regular expressions</u>

## Using the Test Method

Regular expressions are used in programming languages to match parts of strings. You create patterns to help you do that matching.

If you want to find the word `the` in the string `The dog chased the cat`, you could use the following regular expression: `/the/`. Notice that quote marks are not required within the regular expression.

JavaScript has multiple ways to use regexes. One way to test a regex is using the `.test()` method. The `.test()` method takes the regex, applies it to a string (which is placed inside the parentheses), and returns `true` or `false` if your pattern finds something or not.

```js
let testStr = "freeCodeCamp";
let testRegex = /Code/;
testRegex.test(testStr);
```

The `test` method here returns `true`.

------

## Match Literal Strings

In the last challenge, you searched for the word `Hello` using the regular expression `/Hello/`. That regex searched for a literal match of the string `Hello`. Here's another example searching for a literal match of the string `Kevin`:

```js
let testStr = "Hello, my name is Kevin.";
let testRegex = /Kevin/;
testRegex.test(testStr);
```

This `test` call will return `true`.

Any other forms of `Kevin` will not match. For example, the regex `/Kevin/` will not match `kevin` or `KEVIN`.

```js
let wrongRegex = /kevin/;
wrongRegex.test(testStr);
```

This `test` call will return `false`.

A future challenge will show how to match those other forms as well.

------

## Match a Literal String with Different Possibilities

Using regexes like `/coding/`, you can look for the pattern `coding` in another string.

This is powerful to search single strings, but it's limited to only one pattern. You can search for multiple patterns using the `alternation` or `OR` operator: `|`.

This operator matches patterns either before or after it. For example, if you wanted to match the strings `yes` or `no`, the regex you want is `/yes|no/`.

You can also search for more than just two patterns. You can do this by adding more patterns with more `OR` operators separating them, like `/yes|no|maybe/`.

------

## Ignore Case While Matching

Up until now, you've looked at regexes to do literal matches of strings. But sometimes, you might want to also match case differences.

Case (or sometimes letter case) is the difference between uppercase letters and lowercase letters. Examples of uppercase are `A`, `B`, and `C`. Examples of lowercase are `a`, `b`, and `c`.

You can match both cases using what is called a flag. There are other flags but here you'll focus on the flag that ignores case - the `i` flag. You can use it by appending it to the regex. An example of using this flag is `/ignorecase/i`. This regex can match the strings `ignorecase`, `igNoreCase`, and `IgnoreCase`.

------

Write a regex `fccRegex` to match `freeCodeCamp`, no matter its case. Your regex should not match any abbreviations or variations with spaces.

```js
let myString = "freeCodeCamp";
let fccRegex = /freeCodeCamp/i; // Change this line
let result = fccRegex.test(myString);
```

## Extract Matches

So far, you have only been checking if a pattern exists or not within a string. You can also extract the actual matches you found with the `.match()` method.

To use the `.match()` method, apply the method on a string and pass in the regex inside the parentheses.

Here's an example:

```js
"Hello, World!".match(/Hello/);
let ourStr = "Regular expressions";
let ourRegex = /expressions/;
ourStr.match(ourRegex);
```

Here the first `match` would return `["Hello"]` and the second would return `["expressions"]`.

Note that the `.match` syntax is the "opposite" of the `.test` method you have been using thus far:

```js
'string'.match(/regex/);
/regex/.test('string');
```

------

Apply the `.match()` method to extract the string `coding`.

```js
let extractStr = "Extract the word 'coding' from this string.";
let codingRegex = /coding/; // Change this line
let result = extractStr.match(codingRegex); // Change this line
```

------

# Find More Than the First Match

So far, you have only been able to extract or search a pattern once.

```js
let testStr = "Repeat, Repeat, Repeat";
let ourRegex = /Repeat/;
testStr.match(ourRegex);
```

Here `match` would return `["Repeat"]`.

To search or extract a pattern more than once, you can use the `g` flag.

```js
let repeatRegex = /Repeat/g;
testStr.match(repeatRegex);
```

And here `match` returns the value `["Repeat", "Repeat", "Repeat"]`

------

Using the regex `starRegex`, find and extract both `Twinkle` words from the string `twinkleStar`.

**Note**
You can have multiple flags on your regex like `/search/gi`

```js
let twinkleStar = "Twinkle, twinkle, little star";
let starRegex = /Twinkle/gi; // Change this line
let result = twinkleStar.match(starRegex); // Change this line
```

# Match Anything with Wildcard Period

Sometimes you won't (or don't need to) know the exact characters in your patterns. Thinking of all words that match, say, a misspelling would take a long time. Luckily, you can save time using the wildcard character: `.`

The wildcard character `.` will match any one character. The wildcard is also called `dot` and `period`. You can use the wildcard character just like any other character in the regex. For example, if you wanted to match `hug`, `huh`, `hut`, and `hum`, you can use the regex `/hu./` to match all four words.

```js
let humStr = "I'll hum a song";
let hugStr = "Bear hug";
let huRegex = /hu./;
huRegex.test(humStr);
huRegex.test(hugStr);
```

Both of these `test` calls would return `true`.

------

Complete the regex `unRegex` so that it matches the strings `run`, `sun`, `fun`, `pun`, `nun`, and `bun`. Your regex should use the wildcard character.

```js
let exampleStr = "Let's have fun with regular expressions!";
let unRegex = /.un/; // Change this line
let result = unRegex.test(exampleStr);
```

# Match Single Character with Multiple Possibilities

You learned how to match literal patterns (`/literal/`) and wildcard character (`/./`). Those are the extremes of regular expressions, where one finds exact matches and the other matches everything. There are options that are a balance between the two extremes.

You can search for a literal pattern with some flexibility with character classes. Character classes allow you to define a group of characters you wish to match by placing them inside square (`[` and `]`) brackets.

For example, you want to match `bag`, `big`, and `bug` but not `bog`. You can create the regex `/b[aiu]g/` to do this. The `[aiu]` is the character class that will only match the characters `a`, `i`, or `u`.

```js
let bigStr = "big";
let bagStr = "bag";
let bugStr = "bug";
let bogStr = "bog";
let bgRegex = /b[aiu]g/;
bigStr.match(bgRegex);
bagStr.match(bgRegex);
bugStr.match(bgRegex);
bogStr.match(bgRegex);
```

In order, the four `match` calls would return the values `["big"]`, `["bag"]`, `["bug"]`, and `null`.

------

Use a character class with vowels (`a`, `e`, `i`, `o`, `u`) in your regex `vowelRegex` to find all the vowels in the string `quoteSample`.

**Note:** Be sure to match both upper- and lowercase vowels.

```js
let quoteSample = "Beware of bugs in the above code; I have only proved it correct, not tried it.";
let vowelRegex = /[aeiou]/ig; // Change this line
let result = quoteSample.match(vowelRegex); // Change this line
```

# Match Letters of the Alphabet

You saw how you can use character sets to specify a group of characters to match, but that's a lot of typing when you need to match a large range of characters (for example, every letter in the alphabet). Fortunately, there is a built-in feature that makes this short and simple.

Inside a character set, you can define a range of characters to match using a hyphen character: `-`.

For example, to match lowercase letters `a` through `e` you would use `[a-e]`.

```js
let catStr = "cat";
let batStr = "bat";
let matStr = "mat";
let bgRegex = /[a-e]at/;
catStr.match(bgRegex);
batStr.match(bgRegex);
matStr.match(bgRegex);
```

In order, the three `match` calls would return the values `["cat"]`, `["bat"]`, and `null`.

------

Match all the letters in the string `quoteSample`.

**Note**: Be sure to match both uppercase and lowercase letters.

```js
let quoteSample = "The quick brown fox jumps over the lazy dog.";
let alphabetRegex = /[a-z]/ig; // Change this line
let result = quoteSample.match(alphabetRegex); // Change this line

```

# Match Numbers and Letters of the Alphabet

Using the hyphen (`-`) to match a range of characters is not limited to letters. It also works to match a range of numbers.

For example, `/[0-5]/` matches any number between `0` and `5`, including the `0` and `5`.

Also, it is possible to combine a range of letters and numbers in a single character set.

```js
let jennyStr = "Jenny8675309";
let myRegex = /[a-z0-9]/ig;
jennyStr.match(myRegex);
```

------

Create a single regex that matches a range of letters between `h` and `s`, and a range of numbers between `2` and `6`. Remember to include the appropriate flags in the regex.

```js
let quoteSample = "Blueberry 3.141592653s are delicious.";
let myRegex = /[h-s2-6]/ig; // Change this line
let result = quoteSample.match(myRegex); // Change this line
```

------

# Match Single Characters Not Specified

So far, you have created a set of characters that you want to match, but you could also create a set of characters that you do not want to match. These types of character sets are called negated character sets.

To create a negated character set, you place a caret character (`^`) after the opening bracket and before the characters you do not want to match.

For example, `/[^aeiou]/gi` matches all characters that are not a vowel. Note that characters like `.`, `!`, `[`, `@`, `/` and white space are matched - the negated vowel character set only excludes the vowel characters.

------

Create a single regex that matches all characters that are not a number or a vowel. Remember to include the appropriate flags in the regex.

 

```js
let quoteSample = "3 blind mice.";
let myRegex = /[^aeiou^0-9]/gi; // Change this line
let result = quoteSample.match(myRegex); // Change this line
```

# Match Characters that Occur One or More Times

Sometimes, you need to match a character (or group of characters) that appears one or more times in a row. This means it occurs at least once, and may be repeated.

You can use the `+` character to check if that is the case. Remember, the character or pattern has to be present consecutively. That is, the character has to repeat one after the other.

For example, `/a+/g` would find one match in `abc` and return `["a"]`. Because of the `+`, it would also find a single match in `aabc` and return `["aa"]`.

If it were instead checking the string `abab`, it would find two matches and return `["a", "a"]` because the `a` characters are not in a row - there is a `b` between them. Finally, since there is no `a` in the string `bcd`, it wouldn't find a match.

------

You want to find matches when the letter `s` occurs one or more times in `Mississippi`. Write a regex that uses the `+` sign.

```js
let difficultSpelling = "Mississippi";
let myRegex = /s+/g; // Change this line
let result = difficultSpelling.match(myRegex);
```

# Match Characters that Occur Zero or More Times

The last challenge used the plus `+` sign to look for characters that occur one or more times. There's also an option that matches characters that occur zero or more times.

The character to do this is the asterisk or star: `*`.

```js
let soccerWord = "gooooooooal!";
let gPhrase = "gut feeling";
let oPhrase = "over the moon";
let goRegex = /go*/;
soccerWord.match(goRegex);
gPhrase.match(goRegex);
oPhrase.match(goRegex);
```

In order, the three `match` calls would return the values `["goooooooo"]`, `["g"]`, and `null`.

------

For this challenge, `chewieQuote` has been initialized as the string `Aaaaaaaaaaaaaaaarrrgh!` behind the scenes. Create a regex `chewieRegex` that uses the `*` character to match an uppercase `A` character immediately followed by zero or more lowercase `a` characters in `chewieQuote`. Your regex does not need flags or character classes, and it should not match any of the other quotes.

```js
// Only change code below this line
let chewieRegex = /Aa*/; // Change this line
// Only change code above this line

let result = chewieQuote.match(chewieRegex);
```

# Find Characters with Lazy Matching

In regular expressions, a greedy match finds the longest possible part of a string that fits the regex pattern and returns it as a match. The alternative is called a lazy match, which finds the smallest possible part of the string that satisfies the regex pattern.

You can apply the regex `/t[a-z]*i/` to the string `"titanic"`. This regex is basically a pattern that starts with `t`, ends with `i`, and has some letters in between.

Regular expressions are by default greedy, so the match would return `["titani"]`. It finds the largest sub-string possible to fit the pattern.

However, you can use the `?` character to change it to lazy matching. `"titanic"` matched against the adjusted regex of `/t[a-z]*?i/` returns `["ti"]`.

**Note:** Parsing HTML with regular expressions should be avoided, but pattern matching an HTML string with regular expressions is completely fine.

------

Fix the regex `/<.*>/` to return the HTML tag `<h1>` and not the text `"<h1>Winter is coming</h1>"`. Remember the wildcard `.` in a regular expression matches any character.

```js
let text = "<h1>Winter is coming</h1>";
let myRegex = /<.*?>/; // Change this line
let result = text.match(myRegex);
```

# Find One or More Criminals in a Hunt

Time to pause and test your new regex writing skills. A group of criminals escaped from jail and ran away, but you don't know how many. However, you do know that they stay close together when they are around other people. You are responsible for finding all of the criminals at once.

Here's an example to review how to do this:

The regex `/z+/` matches the letter `z` when it appears one or more times in a row. It would find matches in all of the following strings:

```js
"z"
"zzzzzz"
"ABCzzzz"
"zzzzABC"
"abczzzzzzzzzzzzzzzzzzzzzabc"
```

But it does not find matches in the following strings since there are no letter `z` characters:

```js
""
"ABC"
"abcabc"
```

------

Write a greedy regex that finds one or more criminals within a group of other people. A criminal is represented by the capital letter `C`.

`let reCriminals = /C+/; // Change this line`

# Match Beginning String Patterns

Prior challenges showed that regular expressions can be used to look for a number of matches. They are also used to search for patterns in specific positions in strings.

In an earlier challenge, you used the caret character (`^`) inside a character set to create a negated character set in the form `[^thingsThatWillNotBeMatched]`. Outside of a character set, the caret is used to search for patterns at the beginning of strings.

```js
let firstString = "Ricky is first and can be found.";
let firstRegex = /^Ricky/;
firstRegex.test(firstString);
let notFirst = "You can't find Ricky now.";
firstRegex.test(notFirst);
```

The first `test` call would return `true`, while the second would return `false`.

------

Use the caret character in a regex to find `Cal` only in the beginning of the string `rickyAndCal`.

```js
let rickyAndCal = "Cal and Ricky both like racing.";
let calRegex = /^Cal/; // Change this line
let result = calRegex.test(rickyAndCal);
```

# Match Ending String Patterns

In the last challenge, you learned to use the caret character to search for patterns at the beginning of strings. There is also a way to search for patterns at the end of strings.

You can search the end of strings using the dollar sign character `$` at the end of the regex.

```js
let theEnding = "This is a never ending story";
let storyRegex = /story$/;
storyRegex.test(theEnding);
let noEnding = "Sometimes a story will have to end";
storyRegex.test(noEnding);
```

The first `test` call would return `true`, while the second would return `false`.

------

Use the anchor character (`$`) to match the string `caboose` at the end of the string

```js
let lastRegex = /caboose$/; // Change this line
let result = lastRegex.test(caboose);
```

# atch All Letters and Numbers

Using character classes, you were able to search for all letters of the alphabet with `[a-z]`. This kind of character class is common enough that there is a shortcut for it, although it includes a few extra characters as well.

The closest character class in JavaScript to match the alphabet is `\w`. This shortcut is equal to `[A-Za-z0-9_]`. This character class matches upper and lowercase letters plus numbers. Note, this character class also includes the underscore character (`_`).

```js
let longHand = /[A-Za-z0-9_]+/;
let shortHand = /\w+/;
let numbers = "42";
let varNames = "important_var";
longHand.test(numbers);
shortHand.test(numbers);
longHand.test(varNames);
shortHand.test(varNames);
```

All four of these `test` calls would return `true`.

These shortcut character classes are also known as shorthand character classes.

------

Use the shorthand character class `\w` to count the number of alphanumeric characters in various quotes and strings.

```js
let quoteSample = "The five boxing wizards jump quickly.";
let alphabetRegexV2 = /\w/g; // Change this line -- globally

let result = quoteSample.match(alphabetRegexV2).length;
```

# Match Everything But Letters and Numbers

You've learned that you can use a shortcut to match alphanumerics `[A-Za-z0-9_]` using `\w`. A natural pattern you might want to search for is the opposite of alphanumerics.

You can search for the opposite of the `\w` with `\W`. Note, the opposite pattern uses a capital letter. This shortcut is the same as `[^A-Za-z0-9_]`.

```js
let shortHand = /\W/;
let numbers = "42%";
let sentence = "Coding!";
numbers.match(shortHand);
sentence.match(shortHand);
```

The first `match` call would return the value `["%"]` and the second would return `["!"]`.

------

Use the shorthand character class `\W` to count the number of non-alphanumeric characters in various quotes and strings.

```js
let quoteSample = "The five boxing wizards jump quickly.";
let nonAlphabetRegex = /\W/g; // Change this line
let result = quoteSample.match(nonAlphabetRegex).length;
```

# Match All Numbers

You've learned shortcuts for common string patterns like alphanumerics. Another common pattern is looking for just digits or numbers.

The shortcut to look for digit characters is `\d`, with a lowercase `d`. This is equal to the character class `[0-9]`, which looks for a single character of any number between zero and nine.

------

Use the shorthand character class `\d` to count how many digits are in movie titles. Written out numbers ("six" instead of 6) do not count.

```js
let movieName = "2001: A Space Odyssey";
let numRegex = /\d/g; // Change this line
let result = movieName.match(numRegex).length;

```

## Match All Non-Numbers

The last challenge showed how to search for digits using the shortcut `\d` with a lowercase `d`. You can also search for non-digits using a similar shortcut that uses an uppercase `D` instead.

The shortcut to look for non-digit characters is `\D`. This is equal to the character class `[^0-9]`, which looks for a single character that is not a number between zero and nine.

------

Use the shorthand character class for non-digits `\D` to count how many non-digits are in movie titles.

```js
let movieName = "2001: A Space Odyssey";
let noNumRegex = /\D/g; // Change this line
let result = movieName.match(noNumRegex).length;
```



# Restrict Possible Usernames

Usernames are used everywhere on the internet. They are what give users a unique identity on their favorite sites.

You need to check all the usernames in a database. Here are some simple rules that users have to follow when creating their username.

1. Usernames can only use alpha-numeric characters.
2. The only numbers in the username have to be at the end. There can be zero or more of them at the end. Username cannot start with the number.
3. Username letters can be lowercase and uppercase.
4. Usernames have to be at least two characters long. A two-character username can only use alphabet letters as characters.

------

Change the regex `userCheck` to fit the constraints listed above.

```js
let username = "JackOfAllTrades";
let userCheck = /^[a-z][a-z]+\d*$|^[a-z]\d\d+$/i;
let result = userCheck.test(username);
console.log(result)
/* Code Explanation
^ - start of input
[a-z] - first character is a letter
[a-z]+ - following characters are letters
\d*$ - input ends with 0 or more digits
| - or
^[a-z] - first character is a letter
\d\d+ - following characters are 2 or more digits
$ - end of input */
```

# Match Whitespace

The challenges so far have covered matching letters of the alphabet and numbers. You can also match the whitespace or spaces between letters.

You can search for whitespace using `\s`, which is a lowercase `s`. This pattern not only matches whitespace, but also carriage return, tab, form feed, and new line characters. You can think of it as similar to the character class `[ \r\t\f\n\v]`.

```js
let whiteSpace = "Whitespace. Whitespace everywhere!"
let spaceRegex = /\s/g;
whiteSpace.match(spaceRegex);
```

This `match` call would return `[" ", " "]`.

------

Change the regex `countWhiteSpace` to look for multiple whitespace characters in a string.

```js
let sample = "Whitespace is important in separating words";
let countWhiteSpace = /\s/g; // Change this line
let result = sample.match(countWhiteSpace);
```

# Match Non-Whitespace Characters

You learned about searching for whitespace using `\s`, with a lowercase `s`. You can also search for everything except whitespace.

Search for non-whitespace using `\S`, which is an uppercase `s`. This pattern will not match whitespace, carriage return, tab, form feed, and new line characters. You can think of it being similar to the character class `[^ \r\t\f\n\v]`.

```js
let whiteSpace = "Whitespace. Whitespace everywhere!"
let nonSpaceRegex = /\S/g;
whiteSpace.match(nonSpaceRegex).length;
```

The value returned by the `.length` method would be `32`.

------

Change the regex `countNonWhiteSpace` to look for multiple non-whitespace characters in a string.

```js
let sample = "Whitespace is important in separating words";
let countNonWhiteSpace = /\S/g; // Change this line
let result = sample.match(countNonWhiteSpace);
```

# Specify Upper and Lower Number of Matches

Recall that you use the plus sign `+` to look for one or more characters and the asterisk `*` to look for zero or more characters. These are convenient but sometimes you want to match a certain range of patterns.

You can specify the lower and upper number of patterns with quantity specifiers. Quantity specifiers are used with curly brackets (`{` and `}`). You put two numbers between the curly brackets - for the lower and upper number of patterns.

For example, to match only the letter `a` appearing between `3` and `5` times in the string `ah`, your regex would be `/a{3,5}h/`.

```js
let A4 = "aaaah";
let A2 = "aah";
let multipleA = /a{3,5}h/;
multipleA.test(A4);
multipleA.test(A2);
```

The first `test` call would return `true`, while the second would return `false`.

------

Change the regex `ohRegex` to match the entire phrase `Oh no` only when it has `3` to `6` letter `h`'s.



```js
let ohStr = "Ohhh no";
let ohRegex = /Oh{3,6}\sno/; // Change this line
let result = ohRegex.test(ohStr);
console.log(result)
```

# Specify Only the Lower Number of Matches

You can specify the lower and upper number of patterns with quantity specifiers using curly brackets. Sometimes you only want to specify the lower number of patterns with no upper limit.

To only specify the lower number of patterns, keep the first number followed by a comma.

For example, to match only the string `hah` with the letter `a` appearing at least `3` times, your regex would be `/ha{3,}h/`.

```js
let A4 = "haaaah";
let A2 = "haah";
let A100 = "h" + "a".repeat(100) + "h";
let multipleA = /ha{3,}h/;
multipleA.test(A4);
multipleA.test(A2);
multipleA.test(A100);
```

In order, the three `test` calls would return `true`, `false`, and `true`.

------

Change the regex `haRegex` to match the word `Hazzah` only when it has four or more letter `z`'s.

```js
let haStr = "Hazzzzah";
let haRegex = /Haz{4,}ah/g; // Change this line 
//
let result = haRegex.test(haStr);
```

------

# Specify Upper and Lower Number of Matches



Recall that you use the plus sign `+` to look for one or more characters and the asterisk `*` to look for zero or more characters. These are convenient but sometimes you want to match a certain range of patterns.

You can specify the lower and upper number of patterns with quantity specifiers. Quantity specifiers are used with curly brackets (`{` and `}`). You put two numbers between the curly brackets - for the lower and upper number of patterns.

For example, to match only the letter `a` appearing between `3` and `5` times in the string `ah`, your regex would be `/a{3,5}h/`.

```js
let A4 = "aaaah";
let A2 = "aah";
let multipleA = /a{3,5}h/;
multipleA.test(A4);
multipleA.test(A2);
```

The first `test` call would return `true`, while the second would return `false`.

------

Change the regex `ohRegex` to match the entire phrase `Oh no` only when it has `3` to `6` letter `h`'s.

```js
let ohStr = "Ohhh no";

let ohRegex = /Oh{3,6} no/g; // Change this line

let result = ohRegex.test(ohStr);
```

# Specify Exact Number of Matches

You can specify the lower and upper number of patterns with quantity specifiers using curly brackets. Sometimes you only want a specific number of matches.

To specify a certain number of patterns, just have that one number between the curly brackets.

For example, to match only the word `hah` with the letter `a` `3` times, your regex would be `/ha{3}h/`.

```js
let A4 = "haaaah";
let A3 = "haaah";
let A100 = "h" + "a".repeat(100) + "h";
let multipleHA = /ha{3}h/;
multipleHA.test(A4);
multipleHA.test(A3);
multipleHA.test(A100);
```

In order, the three `test` calls would return `false`, `true`, and `false`.

------

Change the regex `timRegex` to match the word `Timber` only when it has four letter `m`'s.

------

```js
let timStr = "Timmmmber";
let timRegex = /Tim{4}ber/; // Change this line
let result = timRegex.test(timStr);
```

# Check for All or None

Sometimes the patterns you want to search for may have parts of it that may or may not exist. However, it may be important to check for them nonetheless.

You can specify the possible existence of an element with a question mark, `?`. This checks for zero or one of the preceding element. You can think of this symbol as saying the previous element is optional.

For example, there are slight differences in American and British English and you can use the question mark to match both spellings.

```js
let american = "color";
let british = "colour";
let rainbowRegex= /colou?r/;
rainbowRegex.test(american);
rainbowRegex.test(british);
```

Both uses of the `test` method would return `true`.

------

Change the regex `favRegex` to match both the American English (`favorite`) and the British English (`favourite`) version of the word.

```js
let favWord = "favorite";
let favRegex = /favou?rite/; // Change this line
let result = favRegex.test(favWord);
```

# Positive and Negative Lookahead

Lookaheads are patterns that tell JavaScript to look-ahead in your string to check for patterns further along. This can be useful when you want to search for multiple patterns over the same string.

There are two kinds of lookaheads: positive lookahead and negative lookahead.

A positive lookahead will look to make sure the element in the search pattern is there, but won't actually match it. A positive lookahead is used as `(?=...)` where the `...` is the required part that is not matched.

On the other hand, a negative lookahead will look to make sure the element in the search pattern is not there. A negative lookahead is used as `(?!...)` where the `...` is the pattern that you do not want to be there. The rest of the pattern is returned if the negative lookahead part is not present.

Lookaheads are a bit confusing but some examples will help.

```js
let quit = "qu";
let noquit = "qt";
let quRegex= /q(?=u)/;
let qRegex = /q(?!u)/;
quit.match(quRegex);
noquit.match(qRegex);
```

Both of these `match` calls would return `["q"]`.

A more practical use of lookaheads is to check two or more patterns in one string. Here is a (naively) simple password checker that looks for between 3 and 6 characters and at least one number:

```js
let password = "abc123";
let checkPass = /(?=\w{3,6})(?=\D*\d)/;
checkPass.test(password);
```

------

Use lookaheads in the `pwRegex` to match passwords that are greater than 5 characters long, and have two consecutive digits.

## Hints

### Hint 1

Remeber to use 2 `lookaheads` to check the patterns in the string. The first `lookahead` is very similar to that given in the example - ‘(?=\w{3,6})’ - only the `lower-number` 3 is too low for our test cases, and an `upper-number` is completely unneccesarry. This first `lookahead` is only used to find a string consisting of a certain amount of characters. A second `lookahead` must be used to check for consecutive numerical values at the end of the string.

### Hint 2

The second `lookahead` is also similar to that given in the example - `(?=\D*\d)` - however, this expression too must be modified to pass all test cases. Remember to specify the exact amount of numbers you want to appear at the end of the string.

```js
let sampleWord = "astronaut";
let pwRegex = /(?=\w{6})(?=\w*\d{2})/; // Change this line
let result = pwRegex.test(sampleWord);
console.log(result)
```

* /w - The \w metacharacter matches word characters.A word character is a character a-z, A-Z, 0-9, including _ (underscore).
* \w* - The *n** quantifier matches any string that contains zero or more occurrences of *n*. (match characters)
* The \d metacharacter matches digits from 0 to 9.



# Check For Mixed Grouping of Characters

Sometimes we want to check for groups of characters using a Regular Expression and to achieve that we use parentheses `()`.

If you want to find either `Penguin` or `Pumpkin` in a string, you can use the following Regular Expression: `/P(engu|umpk)in/g`

Then check whether the desired string groups are in the test string by using the `test()` method.

```js
let testStr = "Pumpkin";
let testRegex = /P(engu|umpk)in/;
testRegex.test(testStr);
```

The `test` method here would return `true`.

------

Fix the regex so that it checks for the names of `Franklin Roosevelt` or `Eleanor Roosevelt` in a case sensitive manner and it should make concessions for middle names.

Then fix the code so that the regex that you have created is checked against `myString` and either `true` or `false` is returned depending on whether the regex matches.

```js
let myString = "Eleanor Roosevelt";
let myRegex = /(Franklin|Eleanor).*Roosevelt/; // Change this line
//Use .* to allow for middle names.

let result = myRegex.test(myString); // Change this line
// After passing the challenge experiment with myString and see how the grouping works
console.log(result)
```

# Reuse Patterns Using Capture Groups

Say you want to match a word that occurs multiple times like below.

```js
let repeatStr = "row row row your boat";
```

You could use `/row row row/`, but what if you don't know the specific word repeated? Capture groups can be used to find repeated substrings.

Capture groups are constructed by enclosing the regex pattern to be captured in parentheses. In this case, the goal is to capture a word consisting of alphanumeric characters so the capture group will be `\w+` enclosed by parentheses: `/(\w+)/`.

The substring matched by the group is saved to a temporary "variable", which can be accessed within the same regex using a backslash and the number of the capture group (e.g. `\1`). Capture groups are automatically numbered by the position of their opening parentheses (left to right), starting at 1.

The example below matches a word that occurs thrice separated by spaces:

```js
let repeatRegex = /(\w+) \1 \1/;
repeatRegex.test(repeatStr); // Returns true
repeatStr.match(repeatRegex); // Returns ["row row row", "row"]
```

Using the `.match()` method on a string will return an array with the matched substring, along with its captured groups.

------

Use capture groups in `reRegex` to match a string that consists of only the same number repeated exactly three times separated by single spaces.

Help;

-- The \d metacharacter matches digits from 0 to 9.

-- The *n*+ quantifier matches any string that contains at least one *n*.

-- The \s metacharacter matches whitespace character. Whitespace characters can be:

- A space character
- A tab character
- A carriage return character
- A new line character
- A vertical tab character
- A form feed character

-- The *n*$ quantifier matches any string with *n* at the end of it. 

-- The *^n* quantifier matches any string with *n* at the beginning of it.

```js
let repeatNum = "42 42 42";
let reRegex = /^(\d+)\s\1\s\1$/; // Change this line
let result = reRegex.test(repeatNum);
console.log(result) //true
```

# Use Capture Groups to Search and Replace

Searching is useful. However, you can make searching even more powerful when it also changes (or replaces) the text you match.

You can search and replace text in a string using `.replace()` on a string. The inputs for `.replace()` is first the regex pattern you want to search for. The second parameter is the string to replace the match or a function to do something.

```js
let wrongText = "The sky is silver.";
let silverRegex = /silver/;
wrongText.replace(silverRegex, "blue");
```

The `replace` call would return the string `The sky is blue.`.

You can also access capture groups in the replacement string with dollar signs (`$`).

```js
"Code Camp".replace(/(\w+)\s(\w+)/, '$2 $1');
```

The `replace` call would return the string `Camp Code`.

------

Write a regex `fixRegex` using three capture groups that will search for each word in the string `one two three`. Then update the `replaceText` variable to replace `one two three` with the string `three two one` and assign the result to the `result` variable. Make sure you are utilizing capture groups in the replacement string using the dollar sign (`$`) syntax.



```js

let str = "one two three";
let fixRegex = /(\w+)\s(\w+)\s(\w+)/; // Change this line
let replaceText = "$3 $2 $1"; // Change this line
let result = str.replace(fixRegex, replaceText);
console.log(result)
```

# Remove Whitespace from Start and End

Sometimes whitespace characters around strings are not wanted but are there. Typical processing of strings is to remove the whitespace at the start and end of it.

------

Write a regex and use the appropriate string methods to remove whitespace at the beginning and end of strings.

**Note:** The `String.prototype.trim()` method would work here, but you'll need to complete this challenge using regular expressions.

```js
let hello = "   Hello, World!  ";
let wsRegex = /^\s+|\s+$/g; // Change this line
let result = hello.replace(wsRegex, ""); // Change this line
console.log(result)
```

------

------

# Basic Data Structures



# Use an Array to Store a Collection of Data

The below is an example of the simplest implementation of an array data structure. This is known as a one-dimensional array, meaning it only has one level, or that it does not have any other arrays nested within it. Notice it contains booleans, strings, and numbers, among other valid JavaScript data types:

```js
let simpleArray = ['one', 2, 'three', true, false, undefined, null];
console.log(simpleArray.length);
```

The `console.log` call displays `7`.

All arrays have a length property, which as shown above, can be very easily accessed with the syntax `Array.length`. A more complex implementation of an array can be seen below. This is known as a multi-dimensional array, or an array that contains other arrays. Notice that this array also contains JavaScript objects, which we will examine very closely in our next section, but for now, all you need to know is that arrays are also capable of storing complex objects.

```js
let complexArray = [
  [
    {
      one: 1,
      two: 2
    },
    {
      three: 3,
      four: 4
    }
  ],
  [
    {
      a: "a",
      b: "b"
    },
    {
      c: "c",
      d: "d"
    }
  ]
];
```

------

# Use an Array to Store a Collection of Data

The below is an example of the simplest implementation of an array data structure. This is known as a one-dimensional array, meaning it only has one level, or that it does not have any other arrays nested within it. Notice it contains booleans, strings, and numbers, among other valid JavaScript data types:

```js
let simpleArray = ['one', 2, 'three', true, false, undefined, null];
console.log(simpleArray.length);
```

The `console.log` call displays `7`.

All arrays have a length property, which as shown above, can be very easily accessed with the syntax `Array.length`. A more complex implementation of an array can be seen below. This is known as a multi-dimensional array, or an array that contains other arrays. Notice that this array also contains JavaScript objects, which we will examine very closely in our next section, but for now, all you need to know is that arrays are also capable of storing complex objects.

```js
let complexArray = [
  [
    {
      one: 1,
      two: 2
    },
    {
      three: 3,
      four: 4
    }
  ],
  [
    {
      a: "a",
      b: "b"
    },
    {
      c: "c",
      d: "d"
    }
  ]
];
```

------

# Access an Array's Contents Using Bracket Notation



The fundamental feature of any data structure is, of course, the ability to not only store data, but to be able to retrieve that data on command. So, now that we've learned how to create an array, let's begin to think about how we can access that array's information.

When we define a simple array as seen below, there are 3 items in it:

```js
let ourArray = ["a", "b", "c"];
```

In an array, each array item has an index. This index doubles as the position of that item in the array, and how you reference it. However, it is important to note, that JavaScript arrays are zero-indexed, meaning that the first element of an array is actually at the ***zeroth*** position, not the first. In order to retrieve an element from an array we can enclose an index in brackets and append it to the end of an array, or more commonly, to a variable which references an array object. This is known as bracket notation. For example, if we want to retrieve the `a` from `ourArray` and assign it to a variable, we can do so with the following code:

```js
let ourVariable = ourArray[0];
```

Now `ourVariable` has the value of `a`.

In addition to accessing the value associated with an index, you can also *set* an index to a value using the same notation:

```js
ourArray[1] = "not b anymore";
```

Using bracket notation, we have now reset the item at index 1 from the string `b`, to `not b anymore`. Now `ourArray` is `["a", "not b anymore", "c"]`.

# Add Items to an Array with push() and unshift()

An array's length, like the data types it can contain, is not fixed. Arrays can be defined with a length of any number of elements, and elements can be added or removed over time; in other words, arrays are mutable. In this challenge, we will look at two methods with which we can programmatically modify an array: `Array.push()` and `Array.unshift()`.

Both methods take one or more elements as parameters and add those elements to the array the method is being called on; the `push()` method adds elements to the end of an array, and `unshift()` adds elements to the beginning. Consider the following:

```js
let twentyThree = 'XXIII';
let romanNumerals = ['XXI', 'XXII'];

romanNumerals.unshift('XIX', 'XX');
```

`romanNumerals` would have the value `['XIX', 'XX', 'XXI', 'XXII']`.

```js
romanNumerals.push(twentyThree);
```

`romanNumerals` would have the value `['XIX', 'XX', 'XXI', 'XXII', 'XXIII']`. Notice that we can also pass variables, which allows us even greater flexibility in dynamically modifying our array's data.

------

We have defined a function, `mixedNumbers`, which we are passing an array as an argument. Modify the function by using `push()` and `unshift()` to add `'I', 2, 'three'` to the beginning of the array and `7, 'VIII', 9` to the end so that the returned array contains representations of the numbers 1-9 in order.

```js
function mixedNumbers(arr) {
  // Only change code below this line
    arr.unshift('I', 2, 'three');
    arr.push(7, 'VIII', 9)
  // Only change code above this line
  return arr;
}

console.log(mixedNumbers(['IV', 5, 'six']));
```

# Remove Items from an Array with pop() and shift()

Both `push()` and `unshift()` have corresponding methods that are nearly functional opposites: `pop()` and `shift()`. As you may have guessed by now, instead of adding, `pop()` *removes* an element from the end of an array, while `shift()` removes an element from the beginning. The key difference between `pop()` and `shift()` and their cousins `push()` and `unshift()`, is that neither method takes parameters, and each only allows an array to be modified by a single element at a time.

Let's take a look:

```js
let greetings = ['whats up?', 'hello', 'see ya!'];

greetings.pop();
```

`greetings` would have the value `['whats up?', 'hello']`.

```js
greetings.shift();
```

`greetings` would have the value `['hello']`.

We can also return the value of the removed element with either method like this:

```js
let popped = greetings.pop();
```

`greetings` would have the value `[]`, and `popped` would have the value `hello`.

------

We have defined a function, `popShift`, which takes an array as an argument and returns a new array. Modify the function, using `pop()` and `shift()`, to remove the first and last elements of the argument array, and assign the removed elements to their corresponding variables, so that the returned array contains their values.

```js
function popShift(arr) {
  let popped = arr.pop(); // Change this line
  let shifted = arr.shift(); // Change this line
  return [shifted, popped];
}

console.log(popShift(['challenge', 'is', 'not', 'complete']));
```

# Remove Items Using splice()

Ok, so we've learned how to remove elements from the beginning and end of arrays using `shift()` and `pop()`, but what if we want to remove an element from somewhere in the middle? Or remove more than one element at once? Well, that's where `splice()` comes in. `splice()` allows us to do just that: **remove any number of consecutive elements** from anywhere in an array.

`splice()` can take up to 3 parameters, but for now, we'll focus on just the first 2. The first two parameters of `splice()` are integers which represent indexes, or positions, of the array that `splice()` is being called upon. And remember, arrays are *zero-indexed*, so to indicate the first element of an array, we would use `0`. `splice()`'s first parameter represents the index on the array from which to begin removing elements, while the second parameter indicates the number of elements to delete. For example:

```js
let array = ['today', 'was', 'not', 'so', 'great'];

array.splice(2, 2);
```

Here we remove 2 elements, beginning with the third element (at index 2). `array` would have the value `['today', 'was', 'great']`.

`splice()` not only modifies the array it's being called on, but it also returns a new array containing the value of the removed elements:

```js
let array = ['I', 'am', 'feeling', 'really', 'happy'];

let newArray = array.splice(3, 2);
```

`newArray` has the value `['really', 'happy']`.

------

We've initialized an array `arr`. Use `splice()` to remove elements from `arr`, so that it only contains elements that sum to the value of `10`.

```js
const arr = [2, 4, 5, 1, 7, 5, 2, 1];
// Only change code below this line
let newArr = arr.splice(1,4)
// Only change code above this line
console.log(arr);
console.log(newArr)
```

# Add Items Using splice()

Remember in the last challenge we mentioned that `splice()` can take up to three parameters? Well, you can use the third parameter, comprised of one or more element(s), to add to the array. This can be incredibly useful for quickly switching out an element, or a set of elements, for another.

```js
const numbers = [10, 11, 12, 12, 15];
const startIndex = 3;
const amountToDelete = 1;

numbers.splice(startIndex, amountToDelete, 13, 14);
console.log(numbers);
```

The second occurrence of `12` is removed, and we add `13` and `14` at the same index. The `numbers` array would now be `[ 10, 11, 12, 13, 14, 15 ]`.

Here, we begin with an array of numbers. Then, we pass the following to `splice()`: The index at which to begin deleting elements (3), the number of elements to be deleted (1), and the remaining arguments (13, 14) will be inserted starting at that same index. Note that there can be any number of elements (separated by commas) following `amountToDelete`, each of which gets inserted.

------

We have defined a function, `htmlColorNames`, which takes an array of HTML colors as an argument. Modify the function using `splice()` to remove the first two elements of the array and add `'DarkSalmon'` and `'BlanchedAlmond'` in their respective places.

```js
function htmlColorNames(arr) {
  // Only change code below this line
  arr.splice(0, 2, "DarkSalmon", "BlanchedAlmond")
  // Only change code above this line
  return arr;
}

console.log(htmlColorNames(['DarkGoldenRod', 'WhiteSmoke', 'LavenderBlush', 'PaleTurquoise', 'FireBrick']));
```

# Copy Array Items Using slice()

The next method we will cover is `slice()`. Rather than modifying an array, `slice()` copies or *extracts* a given number of elements to a new array, leaving the array it is called upon untouched. `slice()` takes only 2 parameters — the first is the index at which to begin extraction, and the second is the index at which to stop extraction (extraction will occur up to, but not including the element at this index). Consider this:

```js
let weatherConditions = ['rain', 'snow', 'sleet', 'hail', 'clear'];

let todaysWeather = weatherConditions.slice(1, 3);
```

`todaysWeather` would have the value `['snow', 'sleet']`, while `weatherConditions` would still have `['rain', 'snow', 'sleet', 'hail', 'clear']`.

In effect, we have created a new array by extracting elements from an existing array.

------

We have defined a function, `forecast`, that takes an array as an argument. Modify the function using `slice()` to extract information from the argument array and return a new array that contains the string elements `warm` and `sunny`.

```js
function forecast(arr) {
  // Only change code below this line
      
  return arr.slice(2,4);
}

// Only change code above this line
console.log(forecast(['cold', 'rainy', 'warm', 'sunny', 'cool', 'thunderstorms']));
```

# Copy an Array with the Spread Operator

While `slice()` allows us to be selective about what elements of an array to copy, among several other useful tasks, ES6's new spread operator allows us to easily copy *all* of an array's elements, in order, with a simple and highly readable syntax. The spread syntax simply looks like this: `...`

In practice, we can use the spread operator to copy an array like so:

```js
let thisArray = [true, true, undefined, false, null];
let thatArray = [...thisArray];
```

`thatArray` equals `[true, true, undefined, false, null]`. `thisArray` remains unchanged and `thatArray` contains the same elements as `thisArray`.

------

We have defined a function, `copyMachine` which takes `arr` (an array) and `num` (a number) as arguments. The function is supposed to return a new array made up of `num` copies of `arr`. We have done most of the work for you, but it doesn't work quite right yet. Modify the function using spread syntax so that it works correctly (hint: another method we have already covered might come in handy here!).

------

```js
function copyMachine(arr, num) {
  let newArr = [];
  while (num >= 1) {
    // Only change code below this line
     newArr.push([...arr])
    // Only change code above this line
    num--;
  }
  return newArr;
}

console.log(copyMachine([true, false, true], 2));
```

# Combine Arrays with the Spread Operator

Another huge advantage of the spread operator is the ability to combine arrays, or to insert all the elements of one array into another, at any index. With more traditional syntaxes, we can concatenate arrays, but this only allows us to combine arrays at the end of one, and at the start of another. Spread syntax makes the following operation extremely simple:

```js
let thisArray = ['sage', 'rosemary', 'parsley', 'thyme'];

let thatArray = ['basil', 'cilantro', ...thisArray, 'coriander'];
```

`thatArray` would have the value `['basil', 'cilantro', 'sage', 'rosemary', 'parsley', 'thyme', 'coriander']`.

Using spread syntax, we have just achieved an operation that would have been more complex and more verbose had we used traditional methods.

------

We have defined a function `spreadOut` that returns the variable `sentence`. Modify the function using the spread operator so that it returns the array `['learning', 'to', 'code', 'is', 'fun']`.

```js
function spreadOut() {
  let fragment = ['to', 'code'];
  let sentence = ['learning', ...fragment, 'is', 'fun'] ; // Change this line
  return sentence;
}

console.log(spreadOut());
```

# Check For The Presence of an Element With indexOf()

Since arrays can be changed, or *mutated*, at any time, there's no guarantee about where a particular piece of data will be on a given array, or if that element even still exists. Luckily, JavaScript provides us with another built-in method, `indexOf()`, that allows us to quickly and easily check for the presence of an element on an array. `indexOf()` takes an element as a parameter, and when called, it returns the position, or index, of that element, or `-1` if the element does not exist on the array.

For example:

```js
let fruits = ['apples', 'pears', 'oranges', 'peaches', 'pears'];

fruits.indexOf('dates');
fruits.indexOf('oranges');
fruits.indexOf('pears');
```

`indexOf('dates')` returns `-1`, `indexOf('oranges')` returns `2`, and `indexOf('pears')` returns `1` (the first index at which each element exists).

------

`indexOf()` can be incredibly useful for quickly checking for the presence of an element on an array. We have defined a function, `quickCheck`, that takes an array and an element as arguments. Modify the function using `indexOf()` so that it returns `true` if the passed element exists on the array, and `false` if it does not.

```js
function quickCheck(arr, elem) {
  // Only change code below this line
return arr.indexOf(elem) >= 0 ? true : false;
  // Only change code above this line
}

console.log(quickCheck(['squash', 'onions', 'shallots'], 'mushrooms'));
```

------

# Iterate Through All an Array's Items Using For Loops

Sometimes when working with arrays, it is very handy to be able to iterate through each item to find one or more elements that we might need, or to manipulate an array based on which data items meet a certain set of criteria. JavaScript offers several built in methods that each iterate over arrays in slightly different ways to achieve different results (such as `every()`, `forEach()`, `map()`, etc.), however the technique which is most flexible and offers us the greatest amount of control is a simple `for` loop.

Consider the following:

```js
function greaterThanTen(arr) {
  let newArr = [];
  for (let i = 0; i < arr.length; i++) {
    if (arr[i] > 10) {
      newArr.push(arr[i]);
    }
  }
  return newArr;
}

greaterThanTen([2, 12, 8, 14, 80, 0, 1]);
```

Using a `for` loop, this function iterates through and accesses each element of the array, and subjects it to a simple test that we have created. In this way, we have easily and programmatically determined which data items are greater than `10`, and returned a new array, `[12, 14, 80]`, containing those items.

------

We have defined a function, `filteredArray`, which takes `arr`, a nested array, and `elem` as arguments, and returns a new array. `elem` represents an element that may or may not be present on one or more of the arrays nested within `arr`. Modify the function, using a `for` loop, to return a filtered version of the passed array such that any array nested within `arr` containing `elem` has been removed.

```js
function filteredArray(arr, elem) {
  let newArr = [];
  // change code below this line

  for (let i = 0; i < arr.length; i++) {
    if (arr[i].indexOf(elem) == -1) {
      //Checks every parameter for the element and if is NOT there continues the code
      newArr.push(arr[i]); //Inserts the element of the array in the new filtered array
    }
  }

  // change code above this line
  return newArr;
}
// change code here to test different cases:
console.log(filteredArray([[3, 2, 3], [1, 6, 3], [3, 13, 26], [19, 3, 9]], 3));
```

# Create complex multi-dimensional arrays

Awesome! You have just learned a ton about arrays! This has been a fairly high level overview, and there is plenty more to learn about working with arrays, much of which you will see in later sections. But before moving on to looking at Objects, lets take one more look, and see how arrays can become a bit more complex than what we have seen in previous challenges.

One of the most powerful features when thinking of arrays as data structures, is that arrays can contain, or even be completely made up of other arrays. We have seen arrays that contain arrays in previous challenges, but fairly simple ones. However, arrays can contain an infinite depth of arrays that can contain other arrays, each with their own arbitrary levels of depth, and so on. In this way, an array can very quickly become a very complex data structure, known as a multi-dimensional, or nested array. Consider the following example:

```js
let nestedArray = [
  ['deep'],
  [
    ['deeper'], ['deeper'] 
  ],
  [
    [
      ['deepest'], ['deepest']
    ],
    [
      [
        ['deepest-est?']
      ]
    ]
  ]
];
```

The `deep` array is nested 2 levels deep. The `deeper` arrays are 3 levels deep. The `deepest` arrays are 4 levels, and the `deepest-est?` is 5.

While this example may seem convoluted, this level of complexity is not unheard of, or even unusual, when dealing with large amounts of data. However, we can still very easily access the deepest levels of an array this complex with bracket notation:

```js
console.log(nestedArray[2][1][0][0][0]);
```

This logs the string `deepest-est?`. And now that we know where that piece of data is, we can reset it if we need to:

```js
nestedArray[2][1][0][0][0] = 'deeper still';

console.log(nestedArray[2][1][0][0][0]);
```

Now it logs `deeper still`.

------

We have defined a variable, `myNestedArray`, set equal to an array. Modify `myNestedArray`, using any combination of strings, numbers, and booleans for data elements, so that it has exactly five levels of depth (remember, the outer-most array is level 1). Somewhere on the third level, include the string `deep`, on the fourth level, include the string `deeper`, and on the fifth level, include the string `deepest`.

```js
let myNestedArray = [
  // Only change code below this line
'level 1',                   /* myNestedArray[0]             */
  ['level 2'],	               /* myNestedArray[1][0]          */
  [['level 3','deep']],	       /* myNestedArray[2][0][0]       */
  [[['level 4','deeper']]],    /* myNestedArray[3][0][0][0]    */
  [[[['level 5','deepest']]]]  /* myNestedArray[4][0][0][0][0] */
  // Only change code above this line
];

let myNestedArray = [
  // Only change code below this line
  ['unshift', false, 1, 2, 3, 'complex', 'nested'],
  ['loop', 'shift', 6, 7, 1000, 'method'],
  ['concat', false, true, 'spread', 'array', ['deep']],
  ['mutate', 1327.98, 'splice', 'slice', 'push', [['deeper']]],
  ['iterate', 1.3849, 7, '8.4876', 'arbitrary', 'depth',[[['deepest']]]]
  // Only change code above this line
];
```

------

# Add Key-Value Pairs to JavaScript Objects

At their most basic, objects are just collections of key-value pairs. In other words, they are pieces of data (values) mapped to unique identifiers called properties (keys). Take a look at an example:

```js
const tekkenCharacter = {
  player: 'Hwoarang',
  fightingStyle: 'Tae Kwon Doe',
  human: true
};
```

The above code defines a Tekken video game character object called `tekkenCharacter`. It has three properties, each of which map to a specific value. If you want to add an additional property, such as "origin", it can be done by assigning `origin` to the object:

```js
tekkenCharacter.origin = 'South Korea';
```

This uses dot notation. If you were to observe the `tekkenCharacter` object, it will now include the `origin` property. Hwoarang also had distinct orange hair. You can add this property with bracket notation by doing:

```js
tekkenCharacter['hair color'] = 'dyed orange';
```

Bracket notation is required if your property has a space in it or if you want to use a variable to name the property. In the above case, the property is enclosed in quotes to denote it as a string and will be added exactly as shown. Without quotes, it will be evaluated as a variable and the name of the property will be whatever value the variable is. Here's an example with a variable:

```js
const eyes = 'eye color';

tekkenCharacter[eyes] = 'brown';
```

After adding all the examples, the object will look like this:

```js
{
  player: 'Hwoarang',
  fightingStyle: 'Tae Kwon Doe',
  human: true,
  origin: 'South Korea',
  'hair color': 'dyed orange',
  'eye color': 'brown'
};
```

------

A `foods` object has been created with three entries. Using the syntax of your choice, add three more entries to it: `bananas` with a value of `13`, `grapes` with a value of `35`, and `strawberries` with a value of `27`.

```js
let foods = {
  apples: 25,
  oranges: 32,
  plums: 28
};

// Only change code below this line
foods["bananas"]= 13;
foods["grapes"] = 35;
foods["strawberries"]= 27;
// Only change code above this line

console.log(foods);
```

# Modify an Object Nested Within an Object

Now let's take a look at a slightly more complex object. Object properties can be nested to an arbitrary depth, and their values can be any type of data supported by JavaScript, including arrays and even other objects. Consider the following:

```js
let nestedObject = {
  id: 28802695164,
  date: 'December 31, 2016',
  data: {
    totalUsers: 99,
    online: 80,
    onlineStatus: {
      active: 67,
      away: 13,
      busy: 8
    }
  }
};
```

`nestedObject` has three properties: `id` (value is a number), `date` (value is a string), and `data` (value is an object with its nested structure). While structures can quickly become complex, we can still use the same notations to access the information we need. To assign the value `10` to the `busy` property of the nested `onlineStatus` object, we use dot notation to reference the property:

```js
nestedObject.data.onlineStatus.busy = 10;
```

------

Here we've defined an object `userActivity`, which includes another object nested within it. Set the value of the `online` key to `45`.

```js
let userActivity = {
  id: 23894201352,
  date: 'January 1, 2017',
  data: {
    totalUsers: 51,
    online: 42
  }
};

// Only change code below this line
userActivity.data.online = 45;
// Only change code above this line

console.log(userActivity);
```

# Access Property Names with Bracket Notation

In the first object challenge we mentioned the use of bracket notation as a way to access property values using the evaluation of a variable. For instance, imagine that our `foods` object is being used in a program for a supermarket cash register. We have some function that sets the `selectedFood` and we want to check our `foods` object for the presence of that food. This might look like:

```js
let selectedFood = getCurrentFood(scannedItem);
let inventory = foods[selectedFood];
```

This code will evaluate the value stored in the `selectedFood` variable and return the value of that key in the `foods` object, or `undefined` if it is not present. Bracket notation is very useful because sometimes object properties are not known before runtime or we need to access them in a more dynamic way.

------

We've defined a function, `checkInventory`, which receives a scanned item as an argument. Return the current value of the `scannedItem` key in the `foods` object. You can assume that only valid keys will be provided as an argument to `checkInventory`.

```js
let foods = {
  apples: 25,
  oranges: 32,
  plums: 28,
  bananas: 13,
  grapes: 35,
  strawberries: 27
};

function checkInventory(scannedItem) {
  // Only change code below this line
return foods[scannedItem]
  // Only change code above this line
}

console.log(checkInventory("apples"));
```

# Use the delete Keyword to Remove Object Properties

Now you know what objects are and their basic features and advantages. In short, they are key-value stores which provide a flexible, intuitive way to structure data, ***and***, they provide very fast lookup time. Throughout the rest of these challenges, we will describe several common operations you can perform on objects so you can become comfortable applying these useful data structures in your programs.

In earlier challenges, we have both added to and modified an object's key-value pairs. Here we will see how we can *remove* a key-value pair from an object.

Let's revisit our `foods` object example one last time. If we wanted to remove the `apples` key, we can remove it by using the `delete` keyword like this:

```js
delete foods.apples;
```

# Check if an Object has a Property

Now we can add, modify, and remove keys from objects. But what if we just wanted to know if an object has a specific property? JavaScript provides us with two different ways to do this. One uses the `hasOwnProperty()` method and the other uses the `in` keyword. If we have an object `users` with a property of `Alan`, we could check for its presence in either of the following ways:

```js
users.hasOwnProperty('Alan');
'Alan' in users;
```

Both of these would return `true`.

```js
let users = {
  Alan: {
    age: 27,
    online: true
  },
  Jeff: {
    age: 32,
    online: true
  },
  Sarah: {
    age: 48,
    online: true
  },
  Ryan: {
    age: 19,
    online: true
  }
};

function isEveryoneHere(userObj) {
  /* return ["Alan", "Jeff", "Sarah", "Ryan"].every(name =>
    userObj.hasOwnProperty(name)
  ); */
  if(
    userObj.hasOwnProperty('Alan') &&
    userObj.hasOwnProperty('Jeff') &&
     userObj.hasOwnProperty('Sarah') &&
       userObj.hasOwnProperty('Ryan') 
  ){
    return true
  } else {
    return false
  }
}

console.log(isEveryoneHere(users));
```

# Iterate Through the Keys of an Object with a for...in Statement

Sometimes you may need to iterate through all the keys within an object. This requires a specific syntax in JavaScript called a for...in statement. For our `users` object, this could look like:

```js
for (let user in users) {
  console.log(user);
}
```

This would log `Alan`, `Jeff`, `Sarah`, and `Ryan` - each value on its own line.

In this statement, we defined a variable `user`, and as you can see, this variable was reset during each iteration to each of the object's keys as the statement looped through the object, resulting in each user's name being printed to the console.

**NOTE:** Objects do not maintain an ordering to stored keys like arrays do; thus a key's position on an object, or the relative order in which it appears, is irrelevant when referencing or accessing that key.

------

We've defined a function `countOnline` which accepts one argument (a users object). Use a for...in statement within this function to loop through the users object passed into the function and return the number of users whose `online` property is set to `true`. An example of a users object which could be passed to `countOnline` is shown below. Each user will have an `online` property with either a `true` or `false` value.

```js
{
  Alan: {
    online: false
  },
  Jeff: {
    online: true
  },
  Sarah: {
    online: false
  }
}

//The function countOnline should use a for in statement to iterate through the object keys of the object passed to it.

//The function countOnline should return 1 when the object { Alan: { online: false }, Jeff: { online: true }, Sarah: { online: false } } is passed to it

//The function countOnline should return 2 when the object { Alan: { online: true }, Jeff: { online: false }, Sarah: { online: true } } is passed to it

//The function countOnline should return 0 when the object { Alan: { online: false }, Jeff: { //online: false }, Sarah: { online: false } } is passed to it


function countOnline(usersObj) {
  // Only change code below this line
  let result = 0;
  for (let users in usersObj) {
    if (usersObj[users].online === true) {
      result++;
    } 
  }
   return result;
  // Only change code above this line
}

console.log(countOnline(users));
```

# Generate an Array of All Object Keys with Object.keys()

We can also generate an array which contains all the keys stored in an object using the `Object.keys()` method and passing in an object as the argument. This will return an array with strings representing each property in the object. Again, there will be no specific order to the entries in the array.

------

Finish writing the `getArrayOfUsers` function so that it returns an array containing all the properties in the object it receives as an argument.

```js

let users = {
  Alan: {
    age: 27,
    online: false
  },
  Jeff: {
    age: 32,
    online: true
  },
  Sarah: {
    age: 48,
    online: false
  },
  Ryan: {
    age: 19,
    online: true
  }
};

function getArrayOfUsers(obj) {
  // Only change code below this line
return Object.keys(obj) 
  // Only change code above this line
}

console.log(getArrayOfUsers(users));
```

# Modify an Array Stored in an Object

Now you've seen all the basic operations for JavaScript objects. You can add, modify, and remove key-value pairs, check if keys exist, and iterate over all the keys in an object. As you continue learning JavaScript you will see even more versatile applications of objects. Additionally, the Data Structures lessons located in the Coding Interview Prep section of the curriculum also cover the ES6 Map and Set objects, both of which are similar to ordinary objects but provide some additional features. Now that you've learned the basics of arrays and objects, you're fully prepared to begin tackling more complex problems using JavaScript!

------

Take a look at the object we've provided in the code editor. The `user` object contains three keys. The `data` key contains five keys, one of which contains an array of `friends`. From this, you can see how flexible objects are as data structures. We've started writing a function `addFriend`. Finish writing it so that it takes a `user` object and adds the name of the `friend` argument to the array stored in `user.data.friends` and returns that array.

```js
The user object should have name, age, and data keys.

The addFriend function should accept a user object and a friend string as arguments and add the friend to the array of friends in the user object.

addFriend(user, "Pete") should return ["Sam", "Kira", "Tomo", "Pete"].
```

------

# Basic Algorithm Scripting

# Reverse a String

Reverse the provided string.

You may need to turn the string into an array before you can reverse it.

Your result must be a string.

------

```js


//`reverseString("hello")` should return a string.
//`reverseString("hello")` should return the string `olleh`.
//`reverseString("Howdy")` should return the string `ydwoH`.
//`reverseString("Greetings from Earth")` should return the string `htraE morf sgniteerG`.
/* function reverseString(str) {
  let reversedStr= '';
  for( let i= str.length - 1; i>=0; i--){
    reversedStr += str[i];
  }
  return reversedStr ;
}

Code Explanation
Starting at the last character of the string passed to the function, you build a new string reversedStr from str.

During each iteration of the for loop, reversedStr gets concatenated with itself and the current character.

Finally, you return the final value of reversedStr.
*/
function reverseString(str) {
  return str
    .split("")
    .reverse()
    .join("");
}
/*
Our goal is to take the input, str, and return it in reverse. Our first step is to split the string by characters using split(''). Notice that we don’t leave anything in between the single quotes, this tells the function to split the string by each character.

Using the split() function will turn our string into an array of characters, keep that in mind as we move forward.

Next we chain the reverse() function, which takes our array of characters and reverses them.

Finally, we chain join('') to put our characters back together into a string. Notice once again that we left no spaces in the argument for join, this makes sure that the array of characters is joined back together by each character.


*/
reverseString("hello");
```

# Factorialize a Number

Return the factorial of the provided integer.

If the integer is represented with the letter `n`, a factorial is the product of all positive integers less than or equal to `n`.

Factorials are often represented with the shorthand notation `n!`

For example: `5! = 1 * 2 * 3 * 4 * 5 = 120`

Only integers greater than or equal to zero will be supplied to the function.

------

```js
/* factorialize(5) should return a number.

factorialize(5) should return 120.

factorialize(10) should return 3628800.

factorialize(20) should return 2432902008176640000.

factorialize(0) should return 1. */
function factorialize(num) {
 let product = 1;
  for (let i = 2; i <= num; i++) {
    product *= i;
  }
  return product;
}

factorialize(5);
console.log(factorialize(5))
```

## Find the Longest Word in a String

```js
function findLongestWordLength(str) {
  //split words -- use space betewenn ''
  let words = str.split(' ');
  let maxLength = 0;
  //console.log(words)
  for (let i = 0; i < words.length; i++){
    if(words[i].length > maxLength) {
      maxLength = words[i].length;
    }
  }
  return maxLength;
}

findLongestWordLength("The quick brown fox jumped over the lazy dog");
console.log(findLongestWordLength("The quick brown fox jumped over the lazy dog"));

/* Code Explanation
Take the string and convert it into an array of words. Declare a variable to keep track of the maximum length and loop from 0 to the length of the array of words.

Then check for the longest word by comparing the current word to the previous one and storing the new longest word. At the end of the loop just return the number value of the variable maxLength.
*/
```

# Return Largest Numbers in Arrays

Return an array consisting of the largest number from each provided sub-array. For simplicity, the provided array will contain exactly 4 sub-arrays.

Remember, you can iterate through an array with a simple for loop, and access each member with array syntax `arr[i]`.

------



1. `largestOfFour([[4, 5, 1, 3], [13, 27, 18, 26], [32, 35, 37, 39], [1000, 1001, 857, 1]])` should return an array.

2. `largestOfFour([[13, 27, 18, 26], [4, 5, 1, 3], [32, 35, 37, 39], [1000, 1001, 857, 1]])` should return `[27, 5, 39, 1001]`.
3. `largestOfFour([[4, 9, 1, 3], [13, 35, 18, 26], [32, 35, 97, 39], [1000000, 1001, 857, 1]])` should return `[9, 35, 97, 1000000]`.
4. `largestOfFour([[17, 23, 25, 12], [25, 7, 34, 48], [4, -10, 18, 21], [-72, -3, -17, -10]])` should return `[25, 48, 21, -3]`.

## Hints

### Hint 1

You will get an array that contains sub arrays of numbers and you need to return an array with the largest number from each of the sub arrays. You will need to keep track of the array with the answer and the largest number of each sub-array.

### Hint 2

You can work with multidimensional arrays by `Array[Index][SubIndex]`

### Hint 3

Pay close attention to the timing of the storing of variables when working with loops

```js
#SOLUTION 1
function largestOfFour(arr) {
 //create a new array
 let results = [];
 //create a loop tp itenerate through the outer array
 for (let i = 0; i < arr.length; i++){
   //create a variable that holds the largest number and put in the first position
   let largestNumber = [i][0];
   //use a for loop for itenerate the subarray
   for (let j=1; j < arr[i].length; j++) {
    // Check if the element of the sub array is larger than the currently stored largest number. If so, then update the number in the variable.
    if (arr[i][j]>largestNumber){
      largestNumber = arr[i][j];
    }
   }
   results[i]= largestNumber;
 }
 return results;
}

largestOfFour([[4, 5, 1, 3], [13, 27, 18, 26], [32, 35, 37, 39], [1000, 1001, 857, 1]]);
console.log(largestOfFour([[4, 5, 1, 3], [13, 27, 18, 26], [32, 35, 37, 39], [1000, 1001, 857, 1]]))
```

# Confirm the Ending

Check if a string (first argument, `str`) ends with the given target string (second argument, `target`).

This challenge *can* be solved with the `.endsWith()` method, which was introduced in ES2015. But for the purpose of this challenge, we would like you to use one of the JavaScript substring methods instead.

```js
function confirmEnding(str, target) {
  return str.slice(str.length - target.length)===target;
}

confirmEnding("Bastian", "n");
console.log(confirmEnding("Bastian", "n"))
```

#### Code Explanation

- First we use the `slice` method copy the string.
- In order to get the last characters in `str` equivalent to the `target`'s length we use the `slice` method.
- The first parameter inside the `slice` method is the starting index and the second parameter would be the ending index.
- For example `str.slice(10, 17)` would return `give me`.
- In this case we only include one parameter which it will copy everything from the starting index.
- We substract the length of `str` and the length of `target`, that way, we shall get the last remaining characters equivalent to the `target`'s length.
- Finally we compare the return result of slice to `target` and check if they have the same characters.



# Repeat a String Repeat a String

Repeat a given string `str` (first argument) for `num` times (second argument). Return an empty string if `num` is not a positive number. For the purpose of this challenge, do *not* use the built-in `.repeat()` method.

```js
function repeatStringNumTimes(str, num) {
//check if num is negative and return an empty string if true.
    if(num < 1){
    return '';
//If not, we add the string to a call of our function with num being decreased by 1, which will add another str and another… until eventually num is 1. 
  } else {
    return str + repeatStringNumTimes(str, num - 1 )
  }
}


repeatStringNumTimes("abc", 3);
//console.log(repeatStringNumTimes("+", 6))
```

# Truncate a String

Truncate a string (first argument) if it is longer than the given maximum string length (second argument). Return the truncated string with a `...` ending.

```js
function truncateString(str, num) {
  if(str.length > num){
   
    return str.slice(0 , num) + '...';
  } else {
    return str;
  }
}

truncateString("A-tisket a-tasket A green and yellow basket", 8);
console.log(truncateString("A-tisket a-tasket A green and yellow basket", 8))
```

# Finders Keepers

Create a function that looks through an array `arr` and returns the first element in it that passes a 'truth test'. This means that given an element `x`, the 'truth test' is passed if `func(x)` is `true`. If no element passes the test, return `undefined`.

## Hints

### Hint 1

We need to return the element from an array that passes a function. Both the `function` and the `array` are passed into our function `findElement(arr, func)`. Looking through the array can be done with a `for` loop.

### Hint 2

`num` is passed to the function. We will need to set it to the elements we want to check with the function.

### Hint 3

Do not forget, if none of the numbers in the array pass the test, it should return `undefined`.

```js
function findElement(arr, func) {
  return arr.find(func);
}

findElement([1, 2, 3, 4], num => num % 2 === 0);

console.log(findElement([1, 2, 3, 4], num => num % 2 === 0))
console.log(findElement([1, 3, 5, 8, 9, 10], function(num) { return num % 2 === 0; }))

console.log(findElement([1, ,22, 3, 5, 9], function(num) { return num % 2 === 0; })
)
//gives the remainder after the integer division 
```

# Boo who

Check if a value is classified as a boolean primitive. Return `true` or `false`.

Boolean primitives are `true` and `false`.

Rules:

`booWho(true)` should return `true`.

`booWho(false)` should return `true`.

`booWho([1, 2, 3])` should return `false`.

`booWho([].slice)` should return `false`.

`booWho({ "a": 1 })` should return `false`.

`booWho(1)` should return `false`.

`booWho(NaN)` should return `false`.

`booWho("a")` should return `false`.

`booWho("true")` should return `false`.

`booWho("false")` should return `false`.

```js
function booWho(bool) {
  return typeof bool === "boolean";
}

// test here
booWho(null);
```

#### Code Explanation

- Uses the operator `typeof` to check if the variable is a boolean. If it is, it will return `true`. Otherwise, if it is any other type it will return `false`.



# Title Case a Sentence

Return the provided string with the first letter of each word capitalized. Make sure the rest of the word is in lower case.

For the purpose of this exercise, you should also capitalize connecting words like `the` and `of`.

`titleCase("I'm a little tea pot")` should return a string.

`titleCase("I'm a little tea pot")` should return the string `I'm A Little Tea Pot`.

`titleCase("sHoRt AnD sToUt")` should return the string `Short And Stout`.

`titleCase("HERE IS MY HANDLE HERE IS MY SPOUT")` should return the string `Here Is My Handle Here Is My Spout`.

```js
function titleCase(str) {
  const newTitle = str.split(' ');
 // console.log(newTitle)
  const updateTitle = []
  for ( let st in newTitle){
    updateTitle[st] = newTitle[st][0].toUpperCase() + newTitle[st].slice(1).toLowerCase();
  }
  return updateTitle.join(' ');
}

titleCase("I'm a little tea pot");
console.log(titleCase("I'm a little tea pot"))
```



#### Code Explanation

Split the string by white spaces, and create a variable to track the updated title. Then we use a loop to turn turn the first character of the word to uppercase and the rest to lowercase. by creating concatenated string composed of the whole word in lowercase with the first character replaced by its uppercase.

# Slice and Splice

You are given two arrays and an index.

Copy each element of the first array into the second array, in order.

Begin inserting elements at index `n` of the second array.

Return the resulting array. The input arrays should remain the same after the function runs.  

```js
function frankenSplice(arr1, arr2, n) {
let localArr = arr2.slice();
//console.log(localArr);

  localArr.splice(n, 0, ...arr1);

  return localArr;
}
console.log(frankenSplice([1, 2, 3], [4, 5, 6], 1))
frankenSplice([1, 2, 3], [4, 5, 6], 1);
```

# Falsy Bouncer

Remove all falsy values from an array.

Falsy values in JavaScript are `false`, `null`, `0`, `""`, `undefined`, and `NaN`.

Hint: Try converting each value to a Boolean.

## Hints

- Falsy is something which evaluates to FALSE. There are only six falsy values in JavaScript: undefined, null, NaN, 0, “” (empty string), and false of course.

- We need to make sure we have all the falsy values to compare, we can know it, maybe with a function with all the falsy values…
- Then we need to add a `filter()` with the falsy values function…

```js
  function bouncer(arr) {
    return arr.filter(Boolean);
  }

  bouncer([7, "ate", "", false, 9]);
  console.log(bouncer([7, "ate", "", false, 9]))
  console.log(bouncer(["a", "b", "c"]))
```

# Where do I Belong

Return the lowest index at which a value (second argument) should be inserted into an array (first argument) once it has been sorted. The returned value should be a number.

For example, `getIndexToIns([1,2,3,4], 1.5)` should return `1` because it is greater than `1` (index 0), but less than `2` (index 1).

Likewise, `getIndexToIns([20,3,5], 19)` should return `2` because once the array has been sorted it will look like `[3,5,20]` and `19` is less than `20` (index 2) and greater than `5` (index 1).

Parameters:

`getIndexToIns([10, 20, 30, 40, 50], 35)` should return `3`.

`getIndexToIns([10, 20, 30, 40, 50], 35)` should return a number.

`getIndexToIns([10, 20, 30, 40, 50], 30)` should return `2`.

`getIndexToIns([10, 20, 30, 40, 50], 30)` should return a number.

`getIndexToIns([40, 60], 50)` should return `1`.

`getIndexToIns([40, 60], 50)` should return a number.

`getIndexToIns([3, 10, 5], 3)` should return `0`.

`getIndexToIns([3, 10, 5], 3)` should return a number.

`getIndexToIns([5, 3, 20, 3], 5)` should return `2`.

`getIndexToIns([5, 3, 20, 3], 5)` should return a number.

`getIndexToIns([2, 20, 10], 19)` should return `2`.

`getIndexToIns([2, 20, 10], 19)` should return a number.

`getIndexToIns([2, 5, 10], 15)` should return `3`.

`getIndexToIns([2, 5, 10], 15)` should return a number.

`getIndexToIns([], 1)` should return `0`.

`getIndexToIns([], 1)` should return a number.

```js
function getIndexToIns(arr, num) {
  //sort from higher to low
  arr.sort((a,b)=> a - b);
  //When an item on the array is greater than the number we are comparing against, then we return the index.
  for(let i=0; i<arr.length; i++){
    if(arr[i]>=num){
       return i;
    }
  
  }
  return arr.length;
}

getIndexToIns([40, 60], 50);
console.log(getIndexToIns([10, 20, 30, 40, 50], 30))
```

# Mutations

Return `true` if the string in the first element of the array contains all of the letters of the string in the second element of the array.

For example, `["hello", "Hello"]`, should return `true` because all of the letters in the second string are present in the first, ignoring case.

The arguments `["hello", "hey"]` should return `false` because the string `hello` does not contain a `y`.

Lastly, `["Alien", "line"]`, should return `true` because all of the letters in `line` are present in `Alien`.

## Hints

### Hint 1

- If everything is lowercase it will be easier to compare.

### Hint 2

- Our strings might be easier to work with if they were arrays of characters.

### Hint 3

- A loop might help. Use `indexOf()` to check if the letter of the second word is on the first.
