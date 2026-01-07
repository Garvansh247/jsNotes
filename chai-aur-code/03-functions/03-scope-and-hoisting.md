# 🔍 Scope and Hoisting in JavaScript

## 📑 Table of Contents
- [What is Scope?](#what-is-scope)
- [Global Scope](#global-scope)
- [Function Scope](#function-scope)
- [Block Scope](#block-scope)
- [Lexical Scope](#lexical-scope)
- [Hoisting](#hoisting)
- [Temporal Dead Zone](#temporal-dead-zone)
- [Common Mistakes](#-common-mistakes)
- [Interview Tips](#-interview-tips)
- [Practice Exercises](#practice-exercises)

---

## What is Scope?

Scope determines the accessibility (visibility) of variables.

```javascript
let globalVar = "global";  // Accessible everywhere

function test() {
  let functionVar = "function";  // Only in function
  
  if (true) {
    let blockVar = "block";  // Only in block
  }
}
```

---

## Global Scope

```javascript
// Global variables
let globalVar = "I'm global";
var globalVar2 = "I'm also global";

function test() {
  console.log(globalVar);   // Can access
  console.log(globalVar2);  // Can access
}

// Global variables attach to window (browser)
var name = "John";
console.log(window.name);  // "John"

// let and const don't attach to window
let age = 30;
console.log(window.age);   // undefined
```

---

## Function Scope

```javascript
function test() {
  var x = 10;  // Function scoped
  let y = 20;  // Also function scoped
  
  if (true) {
    var z = 30;  // Still function scoped
    console.log(x, y, z);  // All accessible
  }
  
  console.log(x, y, z);  // All accessible (var ignores block)
}

// console.log(x);  // ReferenceError
```

---

## Block Scope

```javascript
{
  let x = 10;    // Block scoped
  const y = 20;  // Block scoped
  var z = 30;    // NOT block scoped
}

// console.log(x);  // ReferenceError
// console.log(y);  // ReferenceError
console.log(z);     // 30 (var ignores block)

// if, for, while create blocks
if (true) {
  let blockVar = "block";
}
// console.log(blockVar);  // ReferenceError

for (let i = 0; i < 3; i++) {
  // i is block scoped
}
// console.log(i);  // ReferenceError
```

---

## Lexical Scope

```javascript
function outer() {
  let outerVar = "outer";
  
  function inner() {
    let innerVar = "inner";
    console.log(outerVar);  // Can access outer scope
    console.log(innerVar);  // Can access own scope
  }
  
  inner();
  // console.log(innerVar);  // Cannot access inner scope
}

outer();
```

---

## Hoisting

### Variable Hoisting

```javascript
console.log(x);  // undefined (not ReferenceError)
var x = 5;

// Equivalent to:
var x;
console.log(x);  // undefined
x = 5;

// let and const are hoisted but in TDZ
// console.log(y);  // ReferenceError
let y = 10;
```

### Function Hoisting

```javascript
// Function declarations are fully hoisted
greet();  // "Hello!" (works)

function greet() {
  console.log("Hello!");
}

// Function expressions are NOT hoisted
// sayHi();  // TypeError
const sayHi = function() {
  console.log("Hi!");
};
```

---

## Temporal Dead Zone

```javascript
// TDZ for let/const
{
  // TDZ starts
  // console.log(x);  // ReferenceError
  // console.log(y);  // ReferenceError
  
  let x = 10;    // TDZ ends for x
  const y = 20;  // TDZ ends for y
  
  console.log(x, y);  // Works
}

// Example with typeof
console.log(typeof undeclared);  // "undefined"
// console.log(typeof x);  // ReferenceError (TDZ)
let x = 10;
```

---

## ⚠️ Common Mistakes

```javascript
// ❌ Forgetting var/let/const creates global
function test() {
  x = 10;  // Creates global variable!
}
test();
console.log(x);  // 10

// ✓ Always declare variables
function test2() {
  let x = 10;
}
```

---

## 💼 Interview Tips

### Q1: What is hoisting?

**Answer:**
JavaScript moves declarations to the top of their scope during compilation. Variables declared with `var` are hoisted and initialized with `undefined`. `let`/`const` are hoisted but remain in TDZ until declaration.

### Q2: What is the Temporal Dead Zone?

**Answer:**
The period between entering scope and variable declaration where accessing the variable causes ReferenceError.

```javascript
{
  // TDZ
  // console.log(x);  // ReferenceError
  let x = 10;  // TDZ ends
}
```

### Q3: What's the difference between var, let, and const scoping?

**Answer:**
- `var`: Function scoped
- `let`/`const`: Block scoped
- `var` is hoisted and initialized
- `let`/`const` are hoisted but in TDZ

---

## Practice Exercises

### Exercise 1: Predict Output
What will this code output?

```javascript
var x = 10;

function test() {
  console.log(x);
  var x = 20;
}

test();
```

<details>
<summary>Solution</summary>

```javascript
// undefined
// Due to hoisting, equivalent to:
function test() {
  var x;
  console.log(x);  // undefined
  x = 20;
}
```
</details>

---

**[← Back: Arrow Functions](./02-arrow-functions.md)** | **[Next: This Keyword →](./04-this-keyword.md)**

---

**Made with ❤️ for JavaScript learners**
