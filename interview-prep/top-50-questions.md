# 🎓 Top 50 JavaScript Interview Questions

## 📑 Table of Contents
- [Basic Concepts (1-15)](#basic-concepts)
- [Functions & Scope (16-25)](#functions--scope)
- [Objects & Arrays (26-35)](#objects--arrays)
- [Asynchronous JavaScript (36-45)](#asynchronous-javascript)
- [Advanced Topics (46-50)](#advanced-topics)

---

## Basic Concepts

### 1. What is JavaScript?

**Answer:**
JavaScript is a high-level, interpreted, dynamically-typed programming language primarily used for web development. It's one of the core technologies of the web alongside HTML and CSS.

**Key Features:**
- Runs in browsers and servers (Node.js)
- Event-driven and non-blocking
- Prototype-based object-oriented
- First-class functions
- Single-threaded with async capabilities

```javascript
// JavaScript can manipulate web pages
document.getElementById("demo").innerHTML = "Hello JavaScript!";

// And perform calculations
let sum = 10 + 20; // 30
```

---

### 2. What's the difference between var, let, and const?

**Answer:**

| Feature | var | let | const |
|---------|-----|-----|-------|
| Scope | Function | Block | Block |
| Hoisting | Yes (undefined) | Yes (TDZ) | Yes (TDZ) |
| Redeclaration | ✓ Allowed | ❌ Not allowed | ❌ Not allowed |
| Reassignment | ✓ Allowed | ✓ Allowed | ❌ Not allowed |

```javascript
// var - function scoped
function example1() {
  var x = 10;
  if (true) {
    var x = 20;  // Same variable
  }
  console.log(x); // 20
}

// let - block scoped
function example2() {
  let x = 10;
  if (true) {
    let x = 20;  // Different variable
  }
  console.log(x); // 10
}

// const - cannot reassign
const PI = 3.14;
// PI = 3.15; // Error!

// But can modify object properties
const obj = { a: 1 };
obj.a = 2; // OK!
```

---

### 3. What are JavaScript data types?

**Answer:**
JavaScript has **8 data types**: 7 primitive and 1 reference type.

**Primitive Types:**
1. **String**: `"hello"`, `'world'`
2. **Number**: `42`, `3.14`, `Infinity`, `NaN`
3. **BigInt**: `123n`
4. **Boolean**: `true`, `false`
5. **Undefined**: `undefined`
6. **Null**: `null`
7. **Symbol**: `Symbol("id")`

**Reference Type:**
8. **Object**: `{}`, `[]`, `function(){}`

```javascript
// Checking types
typeof "hello";        // "string"
typeof 42;             // "number"
typeof true;           // "boolean"
typeof undefined;      // "undefined"
typeof Symbol("id");   // "symbol"
typeof null;           // "object" (bug!)
typeof {};             // "object"
typeof [];             // "object"
typeof function(){};   // "function"

// Better array check
Array.isArray([]);     // true
```

---

### 4. What is hoisting?

**Answer:**
Hoisting is JavaScript's behavior of moving variable and function declarations to the top of their scope before code execution.

```javascript
// Function hoisting
greet(); // "Hello" - works!
function greet() {
  console.log("Hello");
}

// var hoisting
console.log(x); // undefined (not error!)
var x = 10;

// Equivalent to:
var x;
console.log(x); // undefined
x = 10;

// let/const hoisting (Temporal Dead Zone)
// console.log(y); // ReferenceError!
let y = 20;
```

**Key Points:**
- Function declarations are fully hoisted
- `var` variables are hoisted and initialized with `undefined`
- `let`/`const` are hoisted but not initialized (TDZ)

---

### 5. What are truthy and falsy values?

**Answer:**
**8 Falsy values** (everything else is truthy):
1. `false`
2. `0`
3. `-0`
4. `0n` (BigInt zero)
5. `""` (empty string)
6. `null`
7. `undefined`
8. `NaN`

```javascript
// Falsy examples
if (0) {}              // Doesn't execute
if ("") {}             // Doesn't execute
if (null) {}           // Doesn't execute

// Truthy examples (surprises!)
if ("0") {}            // Executes! (non-empty string)
if ("false") {}        // Executes!
if ([]) {}             // Executes! (empty array)
if ({}) {}             // Executes! (empty object)

// Practical use
let username = inputValue || "Guest";
// If inputValue is falsy, use "Guest"
```

---

### 6. Difference between == and ===?

**Answer:**
- **`==`** (loose equality): Performs type coercion
- **`===`** (strict equality): No type coercion, must be same type

```javascript
// Loose equality (==)
console.log(5 == "5");           // true (string converted to number)
console.log(true == 1);          // true
console.log(false == 0);         // true
console.log(null == undefined);  // true

// Strict equality (===)
console.log(5 === "5");          // false (different types)
console.log(true === 1);         // false
console.log(false === 0);        // false
console.log(null === undefined); // false

// Always prefer ===
if (value === 5) {  // ✓ Good
  // code
}
```

---

### 7. What is the difference between null and undefined?

**Answer:**
- **`undefined`**: Variable declared but not assigned, JavaScript's default
- **`null`**: Intentional absence of value, assigned by programmer

```javascript
let x;                  // undefined (not assigned)
let y = null;           // null (intentional)

console.log(x);         // undefined
console.log(y);         // null

// Function returns
function test() {}
console.log(test());    // undefined (no return)

// Object property
let obj = {};
console.log(obj.name);  // undefined (doesn't exist)

// Type checking
typeof undefined;       // "undefined"
typeof null;            // "object" (JavaScript bug!)
```

---

### 8. What is NaN? How to check for NaN?

**Answer:**
`NaN` means "Not-a-Number" but ironically, its type is `number`. It results from invalid math operations.

```javascript
// Operations that produce NaN
console.log("hello" / 2);        // NaN
console.log(Math.sqrt(-1));      // NaN
console.log(parseInt("abc"));    // NaN
console.log(0 / 0);              // NaN

// NaN is not equal to anything, even itself!
console.log(NaN === NaN);        // false
console.log(NaN == NaN);         // false

// Checking for NaN
// ❌ Wrong
if (value === NaN) {} // Never works!

// ✓ Correct methods
if (Number.isNaN(value)) {}      // Best
if (isNaN(value)) {}             // Works but converts first
if (value !== value) {}          // Clever trick (only NaN !== itself)

// Difference between isNaN and Number.isNaN
isNaN("hello");                  // true (converts to NaN first)
Number.isNaN("hello");           // false (doesn't convert)
```

---

### 9. What is the typeof operator?

**Answer:**
`typeof` returns a string indicating the type of a value.

```javascript
// Primitives
typeof "hello";        // "string"
typeof 42;             // "number"
typeof 42n;            // "bigint"
typeof true;           // "boolean"
typeof undefined;      // "undefined"
typeof Symbol("id");   // "symbol"

// Special cases
typeof null;           // "object" (bug!)
typeof NaN;            // "number"

// Objects
typeof {};             // "object"
typeof [];             // "object" (arrays are objects)
typeof function(){};   // "function" (special case)

// Better type checking
Array.isArray([]);     // true
value === null;        // check for null
Number.isNaN(value);   // check for NaN
```

---

### 10. Explain type coercion with examples.

**Answer:**
Type coercion is automatic conversion of values from one type to another.

```javascript
// String coercion
console.log("5" + 2);            // "52" (number to string)
console.log("5" + true);         // "5true"

// Number coercion
console.log("5" - 2);            // 3 (string to number)
console.log("5" * "2");          // 10
console.log(true + 1);           // 2 (true = 1)
console.log(false + 1);          // 1 (false = 0)

// Boolean coercion
if ("hello") {}                  // truthy
if (0) {}                        // falsy

// Comparison coercion
console.log(5 == "5");           // true
console.log(0 == false);         // true
console.log("" == 0);            // true

// Tricky examples
console.log([] + []);            // "" (empty string)
console.log([] + {});            // "[object Object]"
console.log(true + true + true); // 3
```

---

### 11. What is the ternary operator?

**Answer:**
The ternary operator is a concise way to write if-else statements.

**Syntax:** `condition ? expressionIfTrue : expressionIfFalse`

```javascript
// Instead of if-else
let age = 18;
let status;
if (age >= 18) {
  status = "adult";
} else {
  status = "minor";
}

// Use ternary
let status = age >= 18 ? "adult" : "minor";

// More examples
let result = score >= 50 ? "Pass" : "Fail";
let type = isLoggedIn ? "user" : "guest";
let message = count > 0 ? "Items available" : "Out of stock";

// Nested ternary (avoid if confusing)
let grade = score >= 90 ? "A" : 
            score >= 80 ? "B" : 
            score >= 70 ? "C" : "F";

// With functions
let greet = isMorning ? "Good Morning" : "Good Evening";
console.log(greet);
```

---

### 12. What are template literals?

**Answer:**
Template literals (backticks) allow string interpolation and multi-line strings.

```javascript
// String interpolation
let name = "John";
let age = 30;

// Old way
let message = "My name is " + name + " and I'm " + age + " years old.";

// Template literal
let message = `My name is ${name} and I'm ${age} years old.`;

// Expressions inside ${}
let price = 100;
let tax = 10;
console.log(`Total: ${price + tax}`); // "Total: 110"

// Multi-line strings
let html = `
  <div>
    <h1>${name}</h1>
    <p>Age: ${age}</p>
  </div>
`;

// Function calls
console.log(`Uppercase: ${name.toUpperCase()}`);
// "Uppercase: JOHN"

// Tagged templates
function highlight(strings, ...values) {
  return strings.reduce((result, str, i) => 
    result + str + (values[i] ? `<b>${values[i]}</b>` : ""), ""
  );
}
let result = highlight`Name: ${name}, Age: ${age}`;
// "Name: <b>John</b>, Age: <b>30</b>"
```

---

### 13. What is the spread operator?

**Answer:**
The spread operator (`...`) expands iterables (arrays, objects, strings) into individual elements.

```javascript
// Array spreading
let arr1 = [1, 2, 3];
let arr2 = [...arr1, 4, 5];
console.log(arr2);              // [1, 2, 3, 4, 5]

// Copying arrays
let original = [1, 2, 3];
let copy = [...original];       // Shallow copy
copy.push(4);
console.log(original);          // [1, 2, 3] (unchanged)

// Combining arrays
let arr3 = [1, 2];
let arr4 = [3, 4];
let combined = [...arr3, ...arr4]; // [1, 2, 3, 4]

// Object spreading
let obj1 = { a: 1, b: 2 };
let obj2 = { ...obj1, c: 3 };
console.log(obj2);              // { a: 1, b: 2, c: 3 }

// Copying objects
let person = { name: "John" };
let personCopy = { ...person }; // Shallow copy

// Overriding properties
let defaults = { color: "red", size: "M" };
let custom = { ...defaults, color: "blue" };
console.log(custom);            // { color: "blue", size: "M" }

// Function arguments
function sum(a, b, c) {
  return a + b + c;
}
let numbers = [1, 2, 3];
console.log(sum(...numbers));   // 6

// String spreading
let str = "hello";
let chars = [...str];
console.log(chars);             // ["h", "e", "l", "l", "o"]
```

---

### 14. What is the rest parameter?

**Answer:**
The rest parameter (`...`) collects multiple elements into an array. It must be the last parameter.

```javascript
// Basic rest parameter
function sum(...numbers) {
  return numbers.reduce((total, num) => total + num, 0);
}
console.log(sum(1, 2, 3));      // 6
console.log(sum(1, 2, 3, 4, 5)); // 15

// With other parameters
function greet(greeting, ...names) {
  return `${greeting} ${names.join(", ")}!`;
}
console.log(greet("Hello", "John", "Jane", "Bob"));
// "Hello John, Jane, Bob!"

// Array destructuring with rest
let [first, second, ...rest] = [1, 2, 3, 4, 5];
console.log(first);             // 1
console.log(second);            // 2
console.log(rest);              // [3, 4, 5]

// Object destructuring with rest
let { a, b, ...others } = { a: 1, b: 2, c: 3, d: 4 };
console.log(a);                 // 1
console.log(b);                 // 2
console.log(others);            // { c: 3, d: 4 }

// Difference: Spread vs Rest
// Spread: expands array/object
let arr = [1, 2, 3];
console.log(...arr);            // 1 2 3 (spread)

// Rest: collects into array
function func(...args) {
  console.log(args);            // [1, 2, 3] (rest)
}
func(1, 2, 3);
```

---

### 15. Explain destructuring in JavaScript.

**Answer:**
Destructuring allows unpacking values from arrays or properties from objects into distinct variables.

```javascript
// Array destructuring
let arr = [1, 2, 3, 4, 5];
let [a, b] = arr;
console.log(a, b);              // 1 2

// Skip elements
let [first, , third] = arr;
console.log(first, third);      // 1 3

// Rest in destructuring
let [x, ...remaining] = arr;
console.log(x);                 // 1
console.log(remaining);         // [2, 3, 4, 5]

// Default values
let [p, q, r = 0] = [1, 2];
console.log(p, q, r);           // 1 2 0

// Object destructuring
let person = {
  name: "John",
  age: 30,
  city: "NYC"
};

let { name, age } = person;
console.log(name, age);         // "John" 30

// Renaming variables
let { name: userName, age: userAge } = person;
console.log(userName, userAge); // "John" 30

// Default values
let { name, country = "USA" } = person;
console.log(country);           // "USA"

// Nested destructuring
let user = {
  id: 1,
  details: {
    name: "John",
    address: {
      city: "NYC"
    }
  }
};

let { details: { name, address: { city } } } = user;
console.log(name, city);        // "John" "NYC"

// Function parameters
function greet({ name, age }) {
  return `${name} is ${age} years old`;
}
greet(person);                  // "John is 30 years old"

// Swapping variables
let a = 1, b = 2;
[a, b] = [b, a];
console.log(a, b);              // 2 1
```

---

## Functions & Scope

### 16. What is a closure?

**Answer:**
A closure is a function that has access to variables in its outer (enclosing) function's scope, even after the outer function has returned.

```javascript
// Basic closure
function outer() {
  let count = 0;
  
  function inner() {
    count++;
    console.log(count);
  }
  
  return inner;
}

let counter = outer();
counter(); // 1
counter(); // 2
counter(); // 3

// Practical example: Private variables
function createCounter() {
  let count = 0;
  
  return {
    increment: function() {
      count++;
      return count;
    },
    decrement: function() {
      count--;
      return count;
    },
    getCount: function() {
      return count;
    }
  };
}

let counter = createCounter();
console.log(counter.increment()); // 1
console.log(counter.increment()); // 2
console.log(counter.getCount());  // 2
// console.log(counter.count);    // undefined (private!)

// Closure in loop (classic interview question)
// ❌ Wrong
for (var i = 0; i < 3; i++) {
  setTimeout(function() {
    console.log(i);  // 3, 3, 3 (not 0, 1, 2!)
  }, 1000);
}

// ✓ Fix with let
for (let i = 0; i < 3; i++) {
  setTimeout(function() {
    console.log(i);  // 0, 1, 2
  }, 1000);
}

// ✓ Fix with IIFE
for (var i = 0; i < 3; i++) {
  (function(j) {
    setTimeout(function() {
      console.log(j); // 0, 1, 2
    }, 1000);
  })(i);
}
```

**Benefits:**
- Data privacy/encapsulation
- Creating factory functions
- Maintaining state
- Memoization

**Drawbacks:**
- Memory consumption (variables not garbage collected)

---

### 17. What is the difference between function declaration and function expression?

**Answer:**

```javascript
// Function Declaration
function greet() {
  return "Hello";
}

// Function Expression
let greet = function() {
  return "Hello";
};

// Named Function Expression
let greet = function greetFunc() {
  return "Hello";
};

// Arrow Function Expression
let greet = () => "Hello";
```

**Key Differences:**

| Feature | Declaration | Expression |
|---------|-------------|------------|
| Hoisting | ✓ Fully hoisted | ❌ Not hoisted |
| Name required | ✓ Yes | ❌ No (can be anonymous) |
| Can call before definition | ✓ Yes | ❌ No |

```javascript
// Function declaration - works!
greet1();  // "Hello"
function greet1() {
  return "Hello";
}

// Function expression - error!
// greet2();  // ReferenceError!
let greet2 = function() {
  return "Hello";
};
greet2();  // Now it works
```

---

### 18. What are arrow functions? How are they different?

**Answer:**
Arrow functions provide a shorter syntax and don't have their own `this`, `arguments`, `super`, or `new.target`.

```javascript
// Regular function
function add(a, b) {
  return a + b;
}

// Arrow function
let add = (a, b) => a + b;

// Variations
let square = x => x * x;        // Single param, no parentheses
let greet = () => "Hello";      // No params, need parentheses
let getObj = () => ({ a: 1 });  // Return object, wrap in ()

// Multi-line
let calculate = (a, b) => {
  let sum = a + b;
  return sum * 2;
};
```

**Key Differences:**

1. **No `this` binding**
```javascript
// Regular function
let obj = {
  name: "John",
  greet: function() {
    console.log(this.name);  // "John"
  }
};

// Arrow function
let obj = {
  name: "John",
  greet: () => {
    console.log(this.name);  // undefined (this = global/window)
  }
};
```

2. **No `arguments` object**
```javascript
// Regular function
function sum() {
  console.log(arguments);  // [1, 2, 3]
}
sum(1, 2, 3);

// Arrow function
let sum = () => {
  // console.log(arguments);  // ReferenceError!
};

// Use rest parameters instead
let sum = (...args) => {
  console.log(args);  // [1, 2, 3]
};
```

3. **Cannot be used as constructor**
```javascript
// Regular function
function Person(name) {
  this.name = name;
}
let john = new Person("John");  // Works

// Arrow function
let Person = (name) => {
  this.name = name;
};
// let john = new Person("John");  // TypeError!
```

**When to use Arrow Functions:**
- ✓ Callbacks and array methods
- ✓ When you want to preserve `this` context
- ✓ Short, simple functions

**When NOT to use:**
- ❌ Object methods (need `this`)
- ❌ Constructors
- ❌ When you need `arguments` object

---

[Content continues with questions 19-50...]

---

**[← Back to Interview Prep](./README.md)** | **[Next: Coding Challenges →](./coding-challenges.md)**

---

**Made with ❤️ for JavaScript learners**
