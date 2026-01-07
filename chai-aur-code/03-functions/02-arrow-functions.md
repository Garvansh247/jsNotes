# 🎯 Arrow Functions in JavaScript

## 📑 Table of Contents
- [Arrow Function Syntax](#arrow-function-syntax)
- [When to Use Arrow Functions](#when-to-use-arrow-functions)
- [Differences from Regular Functions](#differences-from-regular-functions)
- [Limitations](#limitations)
- [Common Use Cases](#common-use-cases)
- [Common Mistakes](#-common-mistakes)
- [Interview Tips](#-interview-tips)
- [Practice Exercises](#practice-exercises)

---

## Arrow Function Syntax

```javascript
// Traditional function
function add(a, b) {
  return a + b;
}

// Arrow function
const add = (a, b) => {
  return a + b;
};

// Concise arrow function (implicit return)
const add = (a, b) => a + b;

// Single parameter (parentheses optional)
const square = x => x * 2;
const square2 = (x) => x * 2;  // Also valid

// No parameters
const greet = () => console.log("Hello");

// Multiple statements
const calculate = (x, y) => {
  let sum = x + y;
  let product = x * y;
  return {sum, product};
};

// Returning object (must wrap in parentheses)
const createPerson = (name, age) => ({name, age});
```

---

## When to Use Arrow Functions

```javascript
// Array methods
const numbers = [1, 2, 3, 4, 5];
const doubled = numbers.map(n => n * 2);
const evens = numbers.filter(n => n % 2 === 0);

// Callbacks
setTimeout(() => console.log("Hello"), 1000);

// Short functions
const greet = name => `Hello, ${name}`;
```

---

## Differences from Regular Functions

### 1. No `this` Binding

```javascript
// Regular function: dynamic `this`
const obj1 = {
  name: "John",
  greet: function() {
    console.log(`Hello, ${this.name}`);
  }
};
obj1.greet();  // "Hello, John"

// Arrow function: lexical `this`
const obj2 = {
  name: "Jane",
  greet: () => {
    console.log(`Hello, ${this.name}`);  // `this` from outer scope
  }
};
obj2.greet();  // "Hello, undefined"
```

### 2. No `arguments` Object

```javascript
// Regular function
function sum() {
  return Array.from(arguments).reduce((a, b) => a + b, 0);
}
console.log(sum(1, 2, 3));  // 6

// Arrow function (use rest parameters)
const sum = (...args) => args.reduce((a, b) => a + b, 0);
console.log(sum(1, 2, 3));  // 6
```

### 3. Cannot be Used as Constructor

```javascript
// Regular function
function Person(name) {
  this.name = name;
}
const john = new Person("John");  // Works

// Arrow function
const Person = (name) => {
  this.name = name;
};
// const jane = new Person("Jane");  // TypeError
```

---

## Limitations

```javascript
// 1. No `this` binding (good for callbacks, bad for methods)
const obj = {
  count: 0,
  increment: () => {
    this.count++;  // Won't work as expected
  }
};

// 2. No `arguments` object
const func = () => {
  console.log(arguments);  // ReferenceError
};

// 3. Cannot be used with `new`
const Func = () => {};
// new Func();  // TypeError

// 4. No `prototype` property
console.log(Func.prototype);  // undefined
```

---

## Common Use Cases

```javascript
// 1. Array methods
const numbers = [1, 2, 3, 4, 5];
const squared = numbers.map(n => n ** 2);
const sum = numbers.reduce((acc, n) => acc + n, 0);

// 2. Promises and async
fetch('/api/data')
  .then(response => response.json())
  .then(data => console.log(data))
  .catch(error => console.error(error));

// 3. Event listeners (when you don't need `this`)
button.addEventListener('click', () => {
  console.log('Clicked!');
});

// 4. setTimeout/setInterval
setTimeout(() => console.log('Done'), 1000);
```

---

## ⚠️ Common Mistakes

```javascript
// ❌ Wrong: Using arrow function for object methods
const obj = {
  name: "John",
  greet: () => console.log(`Hello, ${this.name}`)
};
obj.greet();  // "Hello, undefined"

// ✓ Correct
const obj = {
  name: "John",
  greet() { console.log(`Hello, ${this.name}`) }
};
```

---

## 💼 Interview Tips

### Q1: When should you NOT use arrow functions?

**Answer:**
1. Object methods (need `this`)
2. Prototype methods
3. Constructors
4. When you need `arguments` object
5. Event handlers that need `this`

### Q2: What's the difference between arrow and regular functions?

**Answer:**
- No `this` binding (lexical)
- No `arguments` object
- Cannot be used as constructor
- More concise syntax
- Implicit return for single expressions

---

## Practice Exercises

### Exercise 1: Convert to Arrow Function
Convert the following to arrow functions:

```javascript
function double(x) {
  return x * 2;
}

function greet(name) {
  return `Hello, ${name}`;
}
```

<details>
<summary>Solution</summary>

```javascript
const double = x => x * 2;
const greet = name => `Hello, ${name}`;
```
</details>

---

**[← Back: Function Basics](./01-function-basics.md)** | **[Next: Scope and Hoisting →](./03-scope-and-hoisting.md)**

---

**Made with ❤️ for JavaScript learners**
