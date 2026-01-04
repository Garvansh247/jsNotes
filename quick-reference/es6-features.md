# ⚡ ES6+ Features Complete Guide

## 📑 Table of Contents
- [Let and Const](#let-and-const)
- [Arrow Functions](#arrow-functions)
- [Template Literals](#template-literals)
- [Destructuring](#destructuring)
- [Spread and Rest Operators](#spread-and-rest-operators)
- [Default Parameters](#default-parameters)
- [Classes](#classes)
- [Modules](#modules)
- [Promises](#promises)
- [Async/Await](#asyncawait)
- [Symbol](#symbol)
- [Map and Set](#map-and-set)
- [for...of Loop](#forof-loop)
- [Optional Chaining](#optional-chaining)
- [Nullish Coalescing](#nullish-coalescing)
- [Private Class Fields](#private-class-fields)

---

## Let and Const

**ES6 (2015)** - Block-scoped variable declarations

```javascript
// let - reassignable
let x = 10;
x = 20;  // OK

// const - not reassignable
const y = 10;
// y = 20;  // Error!

// Block scope
if (true) {
  let blockScoped = "only here";
  const alsoBlockScoped = "only here";
}
// console.log(blockScoped);  // Error!

// const with objects/arrays (properties can change)
const person = { name: "John" };
person.name = "Jane";  // OK
person.age = 30;       // OK
// person = {};        // Error!

const arr = [1, 2, 3];
arr.push(4);          // OK
// arr = [];          // Error!
```

---

## Arrow Functions

**ES6 (2015)** - Concise function syntax

```javascript
// Traditional function
function add(a, b) {
  return a + b;
}

// Arrow function
const add = (a, b) => a + b;

// Variations
const square = x => x * x;              // Single parameter, no parentheses
const greet = () => "Hello";            // No parameters
const getUser = () => ({ name: "John" }); // Returning object, wrap in ()

// Multi-line
const calculate = (a, b) => {
  const sum = a + b;
  return sum * 2;
};

// Key differences from regular functions
// 1. No 'this' binding
const obj = {
  name: "John",
  regularFunc: function() {
    console.log(this.name);  // "John"
  },
  arrowFunc: () => {
    console.log(this.name);  // undefined (this = global)
  }
};

// 2. No 'arguments' object
const regular = function() {
  console.log(arguments);  // [1, 2, 3]
};
regular(1, 2, 3);

const arrow = (...args) => {
  console.log(args);  // [1, 2, 3] (use rest parameter)
};
arrow(1, 2, 3);

// 3. Cannot be used as constructor
// const Person = (name) => { this.name = name; };
// new Person("John");  // TypeError!
```

---

## Template Literals

**ES6 (2015)** - String interpolation and multi-line strings

```javascript
// String interpolation
const name = "John";
const age = 30;
const message = `My name is ${name} and I'm ${age} years old.`;

// Expressions
const price = 100;
const tax = 0.1;
console.log(`Total: $${price + (price * tax)}`);  // "Total: $110"

// Multi-line strings
const html = `
  <div>
    <h1>${name}</h1>
    <p>Age: ${age}</p>
  </div>
`;

// Tagged templates
function highlight(strings, ...values) {
  return strings.reduce((result, str, i) => 
    result + str + (values[i] ? `<b>${values[i]}</b>` : ""), ""
  );
}

const user = "John";
const result = highlight`Hello ${user}, welcome!`;
// "Hello <b>John</b>, welcome!"
```

---

## Destructuring

**ES6 (2015)** - Extract values from arrays/objects

```javascript
// Array destructuring
const arr = [1, 2, 3, 4, 5];
const [a, b] = arr;                    // a=1, b=2
const [first, , third] = arr;          // first=1, third=3
const [x, ...rest] = arr;              // x=1, rest=[2,3,4,5]

// Default values
const [p, q, r = 0] = [1, 2];          // p=1, q=2, r=0

// Swapping variables
let m = 1, n = 2;
[m, n] = [n, m];                       // m=2, n=1

// Object destructuring
const person = {
  name: "John",
  age: 30,
  city: "NYC"
};

const { name, age } = person;          // name="John", age=30

// Renaming
const { name: userName } = person;     // userName="John"

// Default values
const { country = "USA" } = person;    // country="USA"

// Nested destructuring
const user = {
  id: 1,
  details: {
    name: "John",
    address: {
      city: "NYC"
    }
  }
};

const { details: { name, address: { city } } } = user;
// name="John", city="NYC"

// Function parameters
function greet({ name, age }) {
  return `${name} is ${age} years old`;
}
greet(person);  // "John is 30 years old"
```

---

## Spread and Rest Operators

**ES6 (2015)** - `...` operator with multiple uses

```javascript
// SPREAD - Expand iterables

// Arrays
const arr1 = [1, 2, 3];
const arr2 = [...arr1, 4, 5];          // [1, 2, 3, 4, 5]
const copy = [...arr1];                // Shallow copy

// Combining arrays
const combined = [...arr1, ...arr2];   // [1, 2, 3, 1, 2, 3, 4, 5]

// Objects
const obj1 = { a: 1, b: 2 };
const obj2 = { ...obj1, c: 3 };        // { a: 1, b: 2, c: 3 }
const objCopy = { ...obj1 };           // Shallow copy

// Override properties
const defaults = { color: "red", size: "M" };
const custom = { ...defaults, color: "blue" };
// { color: "blue", size: "M" }

// Function arguments
function sum(a, b, c) {
  return a + b + c;
}
const numbers = [1, 2, 3];
console.log(sum(...numbers));          // 6

// REST - Collect into array

// Function parameters
function sum(...numbers) {
  return numbers.reduce((a, b) => a + b, 0);
}
sum(1, 2, 3, 4, 5);                    // 15

// With other parameters
function greet(greeting, ...names) {
  return `${greeting} ${names.join(", ")}!`;
}
greet("Hello", "John", "Jane");        // "Hello John, Jane!"

// Array destructuring
const [first, ...remaining] = [1, 2, 3, 4];
// first=1, remaining=[2, 3, 4]

// Object destructuring
const { a, ...others } = { a: 1, b: 2, c: 3 };
// a=1, others={ b: 2, c: 3 }
```

---

## Default Parameters

**ES6 (2015)** - Default function parameter values

```javascript
// Traditional approach
function greet(name) {
  name = name || "Guest";
  return `Hello ${name}`;
}

// ES6 default parameters
function greet(name = "Guest") {
  return `Hello ${name}`;
}

console.log(greet());           // "Hello Guest"
console.log(greet("John"));     // "Hello John"

// Multiple defaults
function createUser(name = "Anonymous", age = 0, role = "user") {
  return { name, age, role };
}

// Expressions as defaults
function calculate(a, b = a * 2) {
  return a + b;
}
calculate(5);                   // 15 (5 + 10)

// Using previous parameters
function greet(firstName, lastName, fullName = `${firstName} ${lastName}`) {
  return fullName;
}
greet("John", "Doe");           // "John Doe"

// With destructuring
function displayUser({ name = "Guest", age = 0 } = {}) {
  console.log(`${name}, ${age}`);
}

displayUser({ name: "John", age: 30 });  // "John, 30"
displayUser({ name: "Jane" });            // "Jane, 0"
displayUser();                            // "Guest, 0"
```

---

## Classes

**ES6 (2015)** - Class syntax for OOP

```javascript
// Class declaration
class Person {
  constructor(name, age) {
    this.name = name;
    this.age = age;
  }
  
  // Method
  greet() {
    return `Hello, I'm ${this.name}`;
  }
  
  // Getter
  get info() {
    return `${this.name}, ${this.age}`;
  }
  
  // Setter
  set newAge(age) {
    if (age > 0) {
      this.age = age;
    }
  }
  
  // Static method
  static species() {
    return "Homo sapiens";
  }
}

const john = new Person("John", 30);
console.log(john.greet());       // "Hello, I'm John"
console.log(john.info);          // "John, 30" (getter)
john.newAge = 31;                // setter
console.log(Person.species());   // "Homo sapiens" (static)

// Inheritance
class Employee extends Person {
  constructor(name, age, jobTitle) {
    super(name, age);              // Call parent constructor
    this.jobTitle = jobTitle;
  }
  
  // Override method
  greet() {
    return `${super.greet()}, I'm a ${this.jobTitle}`;
  }
  
  work() {
    return `${this.name} is working`;
  }
}

const emp = new Employee("Jane", 25, "Developer");
console.log(emp.greet());        // "Hello, I'm Jane, I'm a Developer"
console.log(emp.work());         // "Jane is working"

// Private fields (ES2022)
class BankAccount {
  #balance = 0;                  // Private field
  
  deposit(amount) {
    this.#balance += amount;
  }
  
  getBalance() {
    return this.#balance;
  }
}

const account = new Bank Account();
account.deposit(100);
console.log(account.getBalance());  // 100
// console.log(account.#balance);   // SyntaxError!
```

---

## Modules

**ES6 (2015)** - Import/Export for code organization

```javascript
// ========== math.js ==========
// Named exports
export const PI = 3.14159;

export function add(a, b) {
  return a + b;
}

export function subtract(a, b) {
  return a - b;
}

// Or export at once
const multiply = (a, b) => a * b;
const divide = (a, b) => a / b;
export { multiply, divide };

// Default export (one per file)
export default function calculate(a, b, operation) {
  return operation(a, b);
}

// ========== main.js ==========
// Import default
import calculate from "./math.js";

// Import named exports
import { add, subtract, PI } from "./math.js";

// Import all as namespace
import * as math from "./math.js";

// Rename imports
import { add as sum } from "./math.js";

// Import default and named together
import calculate, { add, PI } from "./math.js";

// Usage
console.log(add(5, 3));              // 8
console.log(math.PI);                // 3.14159
console.log(calculate(10, 2, subtract)); // 8
```

---

## Promises

**ES6 (2015)** - Asynchronous programming

```javascript
// Creating a promise
const promise = new Promise((resolve, reject) => {
  setTimeout(() => {
    const success = true;
    if (success) {
      resolve("Operation successful!");
    } else {
      reject("Operation failed!");
    }
  }, 1000);
});

// Consuming promises
promise
  .then(result => {
    console.log(result);           // "Operation successful!"
    return result.toUpperCase();
  })
  .then(upperResult => {
    console.log(upperResult);      // "OPERATION SUCCESSFUL!"
  })
  .catch(error => {
    console.error(error);
  })
  .finally(() => {
    console.log("Cleanup");
  });

// Promise static methods
Promise.resolve(42)
  .then(value => console.log(value));  // 42

Promise.reject("Error")
  .catch(err => console.error(err));   // "Error"

// Promise.all - wait for all
const p1 = Promise.resolve(1);
const p2 = Promise.resolve(2);
const p3 = Promise.resolve(3);

Promise.all([p1, p2, p3])
  .then(results => console.log(results));  // [1, 2, 3]

// Promise.race - first to complete
Promise.race([p1, p2, p3])
  .then(result => console.log(result));    // 1

// Promise.allSettled - wait for all to settle (ES2020)
Promise.allSettled([p1, p2, Promise.reject("error")])
  .then(results => console.log(results));
// [{ status: "fulfilled", value: 1 }, ...]

// Promise.any - first to fulfill (ES2021)
Promise.any([p1, p2, p3])
  .then(result => console.log(result));    // 1
```

---

## Async/Await

**ES2017 (ES8)** - Syntactic sugar for promises

```javascript
// Async function always returns a promise
async function fetchData() {
  return "Data fetched";
}

fetchData().then(data => console.log(data));  // "Data fetched"

// Await pauses execution until promise resolves
async function getData() {
  const data = await fetchData();
  console.log(data);
  return data;
}

// Error handling with try/catch
async function fetchUser(id) {
  try {
    const response = await fetch(`/api/users/${id}`);
    if (!response.ok) throw new Error("User not found");
    const user = await response.json();
    return user;
  } catch (error) {
    console.error("Error:", error);
    throw error;
  }
}

// Sequential vs Parallel
async function sequential() {
  const user = await fetchUser(1);      // Wait
  const posts = await fetchPosts(user.id); // Then wait
  return { user, posts };
}

async function parallel() {
  const [user, posts] = await Promise.all([
    fetchUser(1),
    fetchPosts(1)
  ]);
  return { user, posts };
}

// Top-level await (ES2022)
const data = await fetchData();  // At top level in modules
```

---

[Content continues for remaining ES6+ features...]

---

**[← Back to Quick Reference](./README.md)** | **[Back to Main README](../README.md)**

---

**Made with ❤️ for JavaScript learners**
