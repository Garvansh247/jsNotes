# ⚡ Function Basics in JavaScript

## 📑 Table of Contents
- [Function Declaration](#function-declaration)
- [Function Expression](#function-expression)
- [Parameters and Arguments](#parameters-and-arguments)
- [Return Values](#return-values)
- [Default Parameters](#default-parameters)
- [Rest Parameters](#rest-parameters)
- [Function Scope](#function-scope)
- [Common Mistakes](#-common-mistakes)
- [Interview Tips](#-interview-tips)
- [Practice Exercises](#practice-exercises)

---

## Function Declaration

```javascript
// Basic function declaration
function greet() {
  console.log("Hello!");
}

greet();  // "Hello!"

// Function with parameters
function greetPerson(name) {
  console.log(`Hello, ${name}!`);
}

greetPerson("John");  // "Hello, John!"

// Function with return value
function add(a, b) {
  return a + b;
}

let result = add(5, 3);
console.log(result);  // 8

// Hoisting: can call before declaration
sayHi();  // "Hi!"

function sayHi() {
  console.log("Hi!");
}
```

---

## Function Expression

```javascript
// Anonymous function expression
const greet = function() {
  console.log("Hello!");
};

greet();  // "Hello!"

// Named function expression
const factorial = function fact(n) {
  if (n <= 1) return 1;
  return n * fact(n - 1);  // Can use name inside
};

console.log(factorial(5));  // 120

// NOT hoisted: must be declared before use
// sayHi();  // Error: sayHi is not defined
const sayHi = function() {
  console.log("Hi!");
};
```

---

## Parameters and Arguments

```javascript
// Multiple parameters
function fullName(firstName, lastName) {
  return `${firstName} ${lastName}`;
}

console.log(fullName("John", "Doe"));  // "John Doe"

// Arguments object (traditional functions)
function sum() {
  let total = 0;
  for (let i = 0; i < arguments.length; i++) {
    total += arguments[i];
  }
  return total;
}

console.log(sum(1, 2, 3, 4, 5));  // 15

// Too few arguments
function greet(name, age) {
  console.log(`${name} is ${age} years old`);
}

greet("John");  // "John is undefined years old"

// Too many arguments (extras ignored)
greet("John", 30, "extra");  // "John is 30 years old"
```

---

## Return Values

```javascript
// Explicit return
function add(a, b) {
  return a + b;
}

// Implicit return (undefined)
function doSomething() {
  console.log("Doing something");
  // No return statement
}

console.log(doSomething());  // undefined

// Early return
function divide(a, b) {
  if (b === 0) {
    return "Cannot divide by zero";
  }
  return a / b;
}

// Return objects (must wrap in parentheses with arrow functions)
function createPerson(name, age) {
  return {
    name: name,
    age: age
  };
}

console.log(createPerson("John", 30));  // {name: "John", age: 30}
```

---

## Default Parameters

```javascript
// ES6 default parameters
function greet(name = "Guest", greeting = "Hello") {
  return `${greeting}, ${name}!`;
}

console.log(greet());                    // "Hello, Guest!"
console.log(greet("John"));              // "Hello, John!"
console.log(greet("John", "Hi"));        // "Hi, John!"

// Default with expressions
function createUser(name, id = Date.now()) {
  return {name, id};
}

// Undefined triggers default, null doesn't
function test(x = 10) {
  console.log(x);
}

test();        // 10
test(undefined);  // 10
test(null);    // null
test(0);       // 0
```

---

## Rest Parameters

```javascript
// Rest parameter (collects remaining arguments)
function sum(...numbers) {
  return numbers.reduce((total, num) => total + num, 0);
}

console.log(sum(1, 2, 3, 4, 5));  // 15

// Mix regular and rest parameters
function greetAll(greeting, ...names) {
  return names.map(name => `${greeting}, ${name}!`).join(' ');
}

console.log(greetAll("Hello", "John", "Jane", "Bob"));
// "Hello, John! Hello, Jane! Hello, Bob!"

// Rest must be last parameter
// function invalid(...nums, last) {}  // SyntaxError
```

---

## Function Scope

```javascript
// Global scope
let globalVar = "I'm global";

function test() {
  // Function scope
  let localVar = "I'm local";
  console.log(globalVar);  // Can access global
  console.log(localVar);   // Can access local
}

test();
console.log(globalVar);    // "I'm global"
// console.log(localVar);  // Error: localVar is not defined

// Block scope (let/const)
function blockScopeTest() {
  if (true) {
    let blockVar = "block";
    var functionVar = "function";
  }
  // console.log(blockVar);    // Error
  console.log(functionVar);    // "function"
}

// Nested functions
function outer() {
  let outerVar = "outer";
  
  function inner() {
    let innerVar = "inner";
    console.log(outerVar);  // Can access outer scope
    console.log(innerVar);  // Can access inner scope
  }
  
  inner();
  // console.log(innerVar);  // Error: innerVar is not defined
}

outer();
```

---

## ⚠️ Common Mistakes

### 1. Forgetting to Return

```javascript
// ❌ Wrong: No return
function add(a, b) {
  a + b;  // Result is lost
}

console.log(add(2, 3));  // undefined

// ✓ Correct
function add2(a, b) {
  return a + b;
}

console.log(add2(2, 3));  // 5
```

### 2. Function vs Function Expression Hoisting

```javascript
// ✓ Works: function declaration hoisted
sayHi();
function sayHi() {
  console.log("Hi!");
}

// ❌ Error: function expression not hoisted
// greet();  // ReferenceError
const greet = function() {
  console.log("Hello!");
};
```

---

## 💼 Interview Tips

### Q1: What's the difference between function declaration and function expression?

**Answer:**
- **Declaration**: Hoisted, can be called before definition
- **Expression**: Not hoisted, must be defined before use

```javascript
// Declaration
sayHi();  // Works
function sayHi() {}

// Expression
// greet();  // Error
const greet = function() {};
```

### Q2: What are default parameters?

**Answer:**
Default values for function parameters when not provided or undefined.

```javascript
function greet(name = "Guest") {
  return `Hello, ${name}`;
}

greet();        // "Hello, Guest"
greet("John");  // "Hello, John"
```

### Q3: What are rest parameters?

**Answer:**
Collects remaining arguments into an array.

```javascript
function sum(...numbers) {
  return numbers.reduce((a, b) => a + b, 0);
}

sum(1, 2, 3, 4);  // 10
```

---

## Practice Exercises

### Exercise 1: Power Function
Write a function to calculate power.

```javascript
function power(base, exponent = 2) {
  // Your code here
}

console.log(power(2, 3));  // 8
console.log(power(3));     // 9
```

<details>
<summary>Solution</summary>

```javascript
function power(base, exponent = 2) {
  return Math.pow(base, exponent);
  // or: return base ** exponent;
}
```
</details>

---

**[← Back: Object Methods](../02-arrays-and-objects/04-object-methods.md)** | **[Next: Arrow Functions →](./02-arrow-functions.md)**

---

**Made with ❤️ for JavaScript learners**
