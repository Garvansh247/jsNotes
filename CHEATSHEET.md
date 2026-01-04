# 🚀 JavaScript Complete Cheatsheet

A comprehensive quick reference for JavaScript covering all essential concepts, methods, and features.

## 📑 Table of Contents

- [Variables](#-variables)
- [Data Types](#-data-types)
- [Operators](#-operators)
- [Strings](#-strings)
- [Numbers & Math](#-numbers--math)
- [Arrays](#-arrays)
- [Objects](#-objects)
- [Functions](#-functions)
- [Control Flow](#-control-flow)
- [Loops](#-loops)
- [DOM Manipulation](#-dom-manipulation)
- [Events](#-events)
- [ES6+ Features](#-es6-features)
- [Async JavaScript](#-async-javascript)
- [Error Handling](#-error-handling)

---

## 📦 Variables

```javascript
// var - function scoped, hoisted, can be redeclared
var x = 10;
var x = 20; // OK

// let - block scoped, not fully hoisted, cannot be redeclared
let y = 10;
// let y = 20; // Error
y = 20; // OK

// const - block scoped, not fully hoisted, cannot be reassigned
const z = 10;
// z = 20; // Error
const obj = { a: 1 };
obj.a = 2; // OK - object properties can be modified
```

---

## 🏷️ Data Types

### Primitives (7 types)
```javascript
let str = "Hello";           // String
let num = 42;                // Number
let bigInt = 123n;           // BigInt
let bool = true;             // Boolean
let undef = undefined;       // Undefined
let nul = null;              // Null
let sym = Symbol("id");      // Symbol

// Check type
typeof str;                  // "string"
typeof num;                  // "number"
typeof bool;                 // "boolean"
typeof undef;                // "undefined"
typeof nul;                  // "object" (JS quirk!)
typeof sym;                  // "symbol"
```

### Reference Types
```javascript
let arr = [1, 2, 3];         // Array
let obj = { a: 1 };          // Object
let func = function() {};     // Function

typeof arr;                   // "object"
typeof obj;                   // "object"
typeof func;                  // "function"

// Better type checking
Array.isArray(arr);           // true
```

---

## ⚙️ Operators

### Arithmetic
```javascript
10 + 5    // 15 - Addition
10 - 5    // 5  - Subtraction
10 * 5    // 50 - Multiplication
10 / 5    // 2  - Division
10 % 3    // 1  - Modulus (remainder)
10 ** 2   // 100 - Exponentiation
```

### Assignment
```javascript
let x = 10;
x += 5;   // x = x + 5 → 15
x -= 5;   // x = x - 5 → 10
x *= 2;   // x = x * 2 → 20
x /= 4;   // x = x / 4 → 5
x %= 3;   // x = x % 3 → 2
x **= 2;  // x = x ** 2 → 4
```

### Comparison
```javascript
5 == "5"   // true  - loose equality (type coercion)
5 === "5"  // false - strict equality (no coercion)
5 != "5"   // false - loose inequality
5 !== "5"  // true  - strict inequality
5 > 3      // true
5 < 3      // false
5 >= 5     // true
5 <= 3     // false
```

### Logical
```javascript
true && false  // false - AND
true || false  // true  - OR
!true          // false - NOT

// Short-circuit evaluation
let result = null || "default";  // "default"
let user = isLoggedIn && getUserData(); // getUserData() only if isLoggedIn is true
```

### Special Operators
```javascript
// Ternary
let age = 18;
let canVote = age >= 18 ? "Yes" : "No";  // "Yes"

// Nullish Coalescing (??)
let value = null ?? "default";      // "default"
let value2 = 0 ?? "default";        // 0 (0 is not null/undefined)

// Optional Chaining (?.)
let user = { address: { city: "NYC" } };
let city = user?.address?.city;     // "NYC"
let zip = user?.address?.zip;       // undefined (no error)

// Spread (...)
let arr1 = [1, 2, 3];
let arr2 = [...arr1, 4, 5];         // [1, 2, 3, 4, 5]
let obj1 = { a: 1, b: 2 };
let obj2 = { ...obj1, c: 3 };       // { a: 1, b: 2, c: 3 }

// Rest (...)
function sum(...numbers) {
  return numbers.reduce((a, b) => a + b);
}
sum(1, 2, 3, 4);                    // 10
```

---

## 📝 Strings

### Creation
```javascript
let str1 = "Hello";                 // Double quotes
let str2 = 'World';                 // Single quotes
let str3 = `Hello ${str2}`;         // Template literal
```

### Common Methods
```javascript
let str = "  Hello World  ";

// Access
str.charAt(0);                      // "H"
str[0];                             // "H"
str.charCodeAt(0);                  // 72 (ASCII)

// Search
str.indexOf("World");               // 8
str.lastIndexOf("o");               // 10
str.includes("World");              // true
str.startsWith("Hello");            // false (has spaces)
str.endsWith("World");              // false (has spaces)
str.search(/world/i);               // 8 (regex search)

// Extract
str.slice(2, 7);                    // "Hello"
str.substring(2, 7);                // "Hello"
str.substr(2, 5);                   // "Hello" (deprecated)

// Modify
str.trim();                         // "Hello World"
str.trimStart();                    // "Hello World  "
str.trimEnd();                      // "  Hello World"
str.toUpperCase();                  // "  HELLO WORLD  "
str.toLowerCase();                  // "  hello world  "
str.replace("World", "JS");         // "  Hello JS  "
str.replaceAll("l", "L");           // "  HeLLo WorLd  "
str.repeat(2);                      // "  Hello World    Hello World  "
str.padStart(20, "*");              // "******  Hello World  "
str.padEnd(20, "*");                // "  Hello World  ******"

// Split/Join
str.split(" ");                     // ["", "", "Hello", "World", "", ""]
"Hello".split("");                  // ["H", "e", "l", "l", "o"]

// Template Literals
let name = "John";
let age = 30;
let message = `My name is ${name} and I'm ${age} years old.`;
```

---

## 🔢 Numbers & Math

### Number Methods
```javascript
let num = 123.456;

num.toFixed(2);                     // "123.46"
num.toPrecision(4);                 // "123.5"
num.toString();                     // "123.456"
num.toExponential(2);               // "1.23e+2"

// Parsing
parseInt("123");                    // 123
parseInt("123.456");                // 123
parseFloat("123.456");              // 123.456
Number("123");                      // 123

// Checking
Number.isInteger(123);              // true
Number.isNaN(NaN);                  // true
Number.isFinite(123);               // true
```

### Math Object
```javascript
Math.PI;                            // 3.141592653589793
Math.E;                             // 2.718281828459045

// Rounding
Math.round(4.7);                    // 5
Math.ceil(4.1);                     // 5
Math.floor(4.9);                    // 4
Math.trunc(4.9);                    // 4 (removes decimals)

// Min/Max
Math.min(1, 2, 3);                  // 1
Math.max(1, 2, 3);                  // 3

// Power/Root
Math.pow(2, 3);                     // 8
Math.sqrt(16);                      // 4
Math.cbrt(27);                      // 3

// Random
Math.random();                      // 0 to 1 (exclusive)
Math.floor(Math.random() * 10);     // 0 to 9
Math.floor(Math.random() * 10) + 1; // 1 to 10

// Random between min and max
function randomRange(min, max) {
  return Math.floor(Math.random() * (max - min + 1)) + min;
}

// Absolute
Math.abs(-5);                       // 5

// Sign
Math.sign(-5);                      // -1
Math.sign(5);                       // 1
Math.sign(0);                       // 0
```

---

## 📚 Arrays

### Creation
```javascript
let arr1 = [1, 2, 3];               // Literal
let arr2 = new Array(1, 2, 3);      // Constructor
let arr3 = Array.from("hello");     // ["h", "e", "l", "l", "o"]
let arr4 = Array.of(1, 2, 3);       // [1, 2, 3]
let arr5 = Array(5).fill(0);        // [0, 0, 0, 0, 0]
```

### Mutating Methods (Change Original Array)
```javascript
let arr = [1, 2, 3, 4, 5];

// Add/Remove at end
arr.push(6);                        // [1, 2, 3, 4, 5, 6] - returns new length
arr.pop();                          // [1, 2, 3, 4, 5] - returns removed element

// Add/Remove at start
arr.unshift(0);                     // [0, 1, 2, 3, 4, 5] - returns new length
arr.shift();                        // [1, 2, 3, 4, 5] - returns removed element

// Add/Remove at any position
arr.splice(2, 1);                   // [1, 2, 4, 5] - removes 1 element at index 2
arr.splice(2, 0, 3);                // [1, 2, 3, 4, 5] - adds 3 at index 2
arr.splice(2, 1, 99);               // [1, 2, 99, 4, 5] - replaces element at index 2

// Sort/Reverse
arr.sort();                         // Sorts alphabetically
arr.sort((a, b) => a - b);          // Sorts numerically ascending
arr.sort((a, b) => b - a);          // Sorts numerically descending
arr.reverse();                      // Reverses array

// Fill
arr.fill(0);                        // [0, 0, 0, 0, 0]
arr.fill(1, 2, 4);                  // Fills from index 2 to 4 with 1
```

### Non-Mutating Methods (Return New Array/Value)
```javascript
let arr = [1, 2, 3, 4, 5];

// Slice - extract portion
arr.slice(1, 3);                    // [2, 3]
arr.slice(-2);                      // [4, 5]

// Concat - join arrays
arr.concat([6, 7]);                 // [1, 2, 3, 4, 5, 6, 7]

// Join - array to string
arr.join(", ");                     // "1, 2, 3, 4, 5"

// Includes/IndexOf
arr.includes(3);                    // true
arr.indexOf(3);                     // 2
arr.lastIndexOf(3);                 // 2
```

### Iteration Methods
```javascript
let arr = [1, 2, 3, 4, 5];

// forEach - execute function for each element
arr.forEach((item, index) => console.log(item, index));

// map - transform each element
let doubled = arr.map(x => x * 2); // [2, 4, 6, 8, 10]

// filter - select elements
let evens = arr.filter(x => x % 2 === 0); // [2, 4]

// reduce - aggregate to single value
let sum = arr.reduce((acc, curr) => acc + curr, 0); // 15

// find - first element matching condition
let found = arr.find(x => x > 3);   // 4

// findIndex - index of first match
let index = arr.findIndex(x => x > 3); // 3

// some - at least one matches
let hasEven = arr.some(x => x % 2 === 0); // true

// every - all match
let allPositive = arr.every(x => x > 0); // true

// flat - flatten nested arrays
let nested = [1, [2, [3, [4]]]];
nested.flat();                      // [1, 2, [3, [4]]]
nested.flat(2);                     // [1, 2, 3, [4]]
nested.flat(Infinity);              // [1, 2, 3, 4]

// flatMap - map then flat
let arr2 = [1, 2, 3];
arr2.flatMap(x => [x, x * 2]);      // [1, 2, 2, 4, 3, 6]
```

### Destructuring & Spread
```javascript
let [a, b, c] = [1, 2, 3];          // a=1, b=2, c=3
let [first, ...rest] = [1, 2, 3, 4]; // first=1, rest=[2, 3, 4]
let [x, , z] = [1, 2, 3];           // x=1, z=3 (skip middle)

let arr1 = [1, 2];
let arr2 = [...arr1, 3, 4];         // [1, 2, 3, 4]
```

---

## 🎯 Objects

### Creation
```javascript
let obj1 = { a: 1, b: 2 };          // Literal
let obj2 = new Object();            // Constructor
let obj3 = Object.create(obj1);     // Inheritance
```

### Access & Modify
```javascript
let person = {
  name: "John",
  age: 30,
  "full name": "John Doe"
};

// Access
person.name;                        // "John" - dot notation
person["age"];                      // 30 - bracket notation
person["full name"];                // "John Doe" - required for spaces

// Optional chaining
person?.address?.city;              // undefined (no error)

// Modify
person.age = 31;
person["age"] = 31;
person.city = "NYC";                // Add new property

// Delete
delete person.city;
```

### Object Methods
```javascript
let obj = { a: 1, b: 2, c: 3 };

// Keys/Values/Entries
Object.keys(obj);                   // ["a", "b", "c"]
Object.values(obj);                 // [1, 2, 3]
Object.entries(obj);                // [["a", 1], ["b", 2], ["c", 3]]
Object.fromEntries([["a", 1]]);     // { a: 1 }

// Assign - merge objects
let obj2 = Object.assign({}, obj, { d: 4 }); // { a: 1, b: 2, c: 3, d: 4 }

// Freeze/Seal
Object.freeze(obj);                 // Cannot add/delete/modify
Object.seal(obj);                   // Cannot add/delete (can modify)
Object.isFrozen(obj);               // true
Object.isSealed(obj);               // true

// Check properties
"a" in obj;                         // true
obj.hasOwnProperty("a");            // true
```

### Destructuring & Spread
```javascript
let { a, b } = { a: 1, b: 2, c: 3 }; // a=1, b=2
let { x, ...rest } = { x: 1, y: 2, z: 3 }; // x=1, rest={y: 2, z: 3}
let { name: userName } = { name: "John" }; // userName="John" (rename)
let { age = 25 } = {};              // age=25 (default value)

let obj1 = { a: 1 };
let obj2 = { ...obj1, b: 2 };       // { a: 1, b: 2 }
```

### Shorthand Properties
```javascript
let name = "John";
let age = 30;

// ES6 shorthand
let person = { name, age };         // { name: "John", age: 30 }

// Method shorthand
let obj = {
  greet() {
    return "Hello";
  }
};
```

---

## 🔧 Functions

### Function Declaration
```javascript
function greet(name) {
  return `Hello ${name}`;
}
```

### Function Expression
```javascript
const greet = function(name) {
  return `Hello ${name}`;
};
```

### Arrow Function
```javascript
const greet = (name) => `Hello ${name}`;
const add = (a, b) => a + b;
const square = x => x * x;          // Single param, no parentheses
const log = () => console.log("Hi"); // No params, need parentheses
```

### Function Features
```javascript
// Default parameters
function greet(name = "Guest") {
  return `Hello ${name}`;
}

// Rest parameters
function sum(...numbers) {
  return numbers.reduce((a, b) => a + b, 0);
}

// IIFE (Immediately Invoked Function Expression)
(function() {
  console.log("Executed immediately");
})();

// Higher Order Functions
function higherOrder(callback) {
  callback();
}

// Returning functions
function multiplier(factor) {
  return function(x) {
    return x * factor;
  };
}
let double = multiplier(2);
double(5);                          // 10
```

---

## 🎮 Control Flow

### If/Else
```javascript
if (condition) {
  // code
} else if (anotherCondition) {
  // code
} else {
  // code
}
```

### Switch
```javascript
switch (value) {
  case 1:
    // code
    break;
  case 2:
  case 3:
    // code for both 2 and 3
    break;
  default:
    // code
}
```

### Ternary
```javascript
let result = condition ? valueIfTrue : valueIfFalse;
```

### Truthy/Falsy
```javascript
// 6 Falsy values
false
0
"" (empty string)
null
undefined
NaN

// Everything else is truthy, including:
"0", "false", [], {}, function(){}
```

---

## 🔁 Loops

### For Loop
```javascript
for (let i = 0; i < 5; i++) {
  console.log(i);
}
```

### While Loop
```javascript
let i = 0;
while (i < 5) {
  console.log(i);
  i++;
}
```

### Do-While Loop
```javascript
let i = 0;
do {
  console.log(i);
  i++;
} while (i < 5);
```

### For...of (Arrays, Strings)
```javascript
for (let item of [1, 2, 3]) {
  console.log(item);                // 1, 2, 3
}

for (let char of "hello") {
  console.log(char);                // h, e, l, l, o
}
```

### For...in (Objects)
```javascript
let obj = { a: 1, b: 2, c: 3 };
for (let key in obj) {
  console.log(key, obj[key]);       // a 1, b 2, c 3
}
```

### Break & Continue
```javascript
for (let i = 0; i < 10; i++) {
  if (i === 5) break;               // Exit loop
  if (i % 2 === 0) continue;        // Skip to next iteration
  console.log(i);                   // 1, 3
}
```

---

## 🌐 DOM Manipulation

### Selecting Elements
```javascript
document.getElementById("myId");
document.getElementsByClassName("myClass");
document.getElementsByTagName("div");
document.querySelector(".myClass");     // First match
document.querySelectorAll(".myClass");  // All matches (NodeList)
```

### Modifying Elements
```javascript
element.innerHTML = "<p>HTML content</p>";
element.textContent = "Text only";
element.innerText = "Visible text only";

element.setAttribute("class", "myClass");
element.getAttribute("class");
element.removeAttribute("class");

element.classList.add("newClass");
element.classList.remove("oldClass");
element.classList.toggle("active");
element.classList.contains("active");

element.style.color = "red";
element.style.backgroundColor = "blue";
```

### Creating/Removing Elements
```javascript
let div = document.createElement("div");
div.textContent = "Hello";
document.body.appendChild(div);

let clone = div.cloneNode(true);        // true = deep clone

div.remove();                           // Remove element
parent.removeChild(child);
```

### Traversing
```javascript
element.parentElement;
element.children;
element.firstElementChild;
element.lastElementChild;
element.nextElementSibling;
element.previousElementSibling;
```

---

## ⚡ Events

### Adding Event Listeners
```javascript
element.addEventListener("click", function(event) {
  console.log("Clicked!", event);
});

// Arrow function
element.addEventListener("click", (e) => {
  console.log("Clicked!", e);
});

// Remove event listener
function handler(e) {
  console.log(e);
}
element.addEventListener("click", handler);
element.removeEventListener("click", handler);
```

### Common Events
```javascript
// Mouse
click, dblclick, mousedown, mouseup, mousemove, mouseenter, mouseleave

// Keyboard
keydown, keypress, keyup

// Form
submit, change, input, focus, blur

// Window
load, DOMContentLoaded, resize, scroll

// Drag & Drop
dragstart, drag, dragend, dragenter, dragover, dragleave, drop
```

### Event Object
```javascript
element.addEventListener("click", (e) => {
  e.target;                         // Element that triggered event
  e.currentTarget;                  // Element listener is attached to
  e.preventDefault();               // Prevent default behavior
  e.stopPropagation();              // Stop event bubbling
  
  // Mouse events
  e.clientX, e.clientY;             // Mouse position
  e.button;                         // Which button clicked
  
  // Keyboard events
  e.key;                            // Key pressed
  e.code;                           // Physical key code
  e.ctrlKey, e.shiftKey, e.altKey;  // Modifier keys
});
```

---

## 🚀 ES6+ Features

### Let & Const
```javascript
let x = 10;                         // Block scoped, reassignable
const y = 20;                       // Block scoped, not reassignable
```

### Template Literals
```javascript
let name = "John";
let greeting = `Hello ${name}!`;
let multiline = `Line 1
Line 2
Line 3`;
```

### Arrow Functions
```javascript
const add = (a, b) => a + b;
```

### Destructuring
```javascript
let [a, b] = [1, 2];
let { name, age } = { name: "John", age: 30 };
```

### Spread & Rest
```javascript
let arr = [1, 2, 3];
let newArr = [...arr, 4, 5];
function sum(...nums) {
  return nums.reduce((a, b) => a + b);
}
```

### Default Parameters
```javascript
function greet(name = "Guest") {
  return `Hello ${name}`;
}
```

### Classes
```javascript
class Person {
  constructor(name) {
    this.name = name;
  }
  greet() {
    return `Hello ${this.name}`;
  }
}
```

### Modules
```javascript
// export
export const name = "John";
export function greet() {}
export default class Person {}

// import
import Person from "./person.js";
import { name, greet } from "./utils.js";
import * as utils from "./utils.js";
```

### Promises
```javascript
let promise = new Promise((resolve, reject) => {
  if (success) resolve(value);
  else reject(error);
});

promise
  .then(result => console.log(result))
  .catch(error => console.error(error))
  .finally(() => console.log("Done"));
```

### Async/Await
```javascript
async function fetchData() {
  try {
    let response = await fetch(url);
    let data = await response.json();
    return data;
  } catch (error) {
    console.error(error);
  }
}
```

### Optional Chaining
```javascript
let city = user?.address?.city;
```

### Nullish Coalescing
```javascript
let value = null ?? "default";      // "default"
let value2 = 0 ?? "default";        // 0
```

### Map & Set
```javascript
// Map
let map = new Map();
map.set("key", "value");
map.get("key");                     // "value"
map.has("key");                     // true
map.delete("key");
map.size;

// Set
let set = new Set([1, 2, 2, 3]);
set.add(4);
set.has(2);                         // true
set.delete(2);
set.size;                           // 3
```

---

## ⏱️ Async JavaScript

### setTimeout
```javascript
setTimeout(() => {
  console.log("After 2 seconds");
}, 2000);

let timerId = setTimeout(() => {}, 1000);
clearTimeout(timerId);              // Cancel timeout
```

### setInterval
```javascript
let intervalId = setInterval(() => {
  console.log("Every 2 seconds");
}, 2000);

clearInterval(intervalId);          // Stop interval
```

### Promises
```javascript
// Creating
let promise = new Promise((resolve, reject) => {
  setTimeout(() => resolve("Success"), 1000);
});

// Consuming
promise
  .then(result => console.log(result))
  .catch(error => console.error(error))
  .finally(() => console.log("Cleanup"));

// Promise methods
Promise.resolve(value);
Promise.reject(error);
Promise.all([p1, p2, p3]);          // All must succeed
Promise.allSettled([p1, p2, p3]);   // All must complete
Promise.race([p1, p2, p3]);         // First to complete
Promise.any([p1, p2, p3]);          // First to succeed
```

### Async/Await
```javascript
async function fetchUser() {
  try {
    let response = await fetch("/api/user");
    let data = await response.json();
    return data;
  } catch (error) {
    console.error(error);
  }
}

// Sequential
let user = await fetchUser();
let posts = await fetchPosts(user.id);

// Parallel
let [user, posts] = await Promise.all([
  fetchUser(),
  fetchPosts()
]);
```

### Fetch API
```javascript
// GET
fetch("https://api.example.com/data")
  .then(response => response.json())
  .then(data => console.log(data))
  .catch(error => console.error(error));

// POST
fetch("https://api.example.com/data", {
  method: "POST",
  headers: {
    "Content-Type": "application/json"
  },
  body: JSON.stringify({ name: "John" })
})
  .then(response => response.json())
  .then(data => console.log(data));

// With async/await
async function getData() {
  let response = await fetch("https://api.example.com/data");
  if (!response.ok) throw new Error("Failed");
  let data = await response.json();
  return data;
}
```

---

## ❌ Error Handling

### Try/Catch/Finally
```javascript
try {
  // Code that might throw error
  throw new Error("Something went wrong");
} catch (error) {
  console.error(error.message);
  console.error(error.stack);
} finally {
  // Always executes
  console.log("Cleanup");
}
```

### Error Types
```javascript
new Error("message");               // Generic error
new TypeError("not a function");
new ReferenceError("not defined");
new SyntaxError("invalid syntax");
new RangeError("out of range");
```

### Custom Errors
```javascript
class CustomError extends Error {
  constructor(message) {
    super(message);
    this.name = "CustomError";
  }
}

throw new CustomError("Custom error occurred");
```

### Error Handling Patterns
```javascript
// With promises
promise
  .then(result => {})
  .catch(error => console.error(error));

// With async/await
async function getData() {
  try {
    let data = await fetch(url);
    return data;
  } catch (error) {
    console.error(error);
    throw error; // Re-throw if needed
  }
}
```

---

## 🎯 Quick Tips

- Use `const` by default, `let` when you need to reassign, avoid `var`
- Use strict equality (`===`) instead of loose (`==`)
- Prefer arrow functions for callbacks
- Use template literals for string concatenation
- Destructure when accessing multiple properties
- Use optional chaining to avoid null/undefined errors
- Prefer async/await over promise chains for readability
- Use `Array.from()` or spread operator to convert array-like objects
- Remember the 6 falsy values: `false`, `0`, `""`, `null`, `undefined`, `NaN`
- Use `console.table()` for better object/array visualization

---

**🔗 Navigation**
- [← Back to README](./README.md)
- [📚 Chai aur Code Section →](./chai-aur-code/)
- [🙏 Namaste JavaScript Section →](./namaste-javascript/)

---

**Made with ❤️ for JavaScript learners**
