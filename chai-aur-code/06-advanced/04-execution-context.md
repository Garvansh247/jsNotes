# ⚙️ Execution Context in JavaScript

## 📑 Table of Contents
- [What is Execution Context?](#what-is-execution-context)
- [Types of Execution Context](#types-of-execution-context)
- [Creation Phase](#creation-phase)
- [Execution Phase](#execution-phase)
- [Call Stack](#call-stack)
- [Common Mistakes](#-common-mistakes)
- [Interview Tips](#-interview-tips)

---

## What is Execution Context?

An execution context is an environment where JavaScript code is evaluated and executed.

---

## Types of Execution Context

1. **Global Execution Context**: Default context, created when code starts
2. **Function Execution Context**: Created when a function is called
3. **Eval Execution Context**: Inside eval() function

---

## Creation Phase

During creation phase:
1. Create scope chain
2. Create variable object (variables, functions, arguments)
3. Determine value of `this`

```javascript
function test(a) {
  var b = 2;
  function inner() {}
  var c = function() {};
}

test(1);

// Creation phase creates:
// - Arguments object: {0: 1, length: 1}
// - Variables: b = undefined, c = undefined
// - Functions: inner() = function definition
```

---

## Execution Phase

During execution phase:
- Variable assignments are made
- Code is executed line by line

```javascript
console.log(a);  // undefined (hoisted)
var a = 10;
console.log(a);  // 10
```

---

## Call Stack

JavaScript uses a call stack to manage execution contexts.

```javascript
function first() {
  console.log('First');
  second();
  console.log('First again');
}

function second() {
  console.log('Second');
  third();
  console.log('Second again');
}

function third() {
  console.log('Third');
}

first();

// Call stack:
// 1. Global context
// 2. first()
// 3. second()
// 4. third() <- Top
// Then unwinds...
```

---

## ⚠️ Common Mistakes

```javascript
// Stack overflow
function recurse() {
  recurse();  // Infinite recursion
}

// recurse();  // RangeError: Maximum call stack size exceeded
```

---

## 💼 Interview Tips

### Q1: What is the execution context?

**Answer:**
An environment where JavaScript code is evaluated and executed. Contains scope chain, variable object, and `this` value.

### Q2: What is the call stack?

**Answer:**
A stack data structure that tracks function calls. Each function call creates a new execution context pushed onto the stack.

---

**[← Back: Classes and OOP](./03-classes-and-oop.md)** | **[Next: Callbacks →](../07-async-javascript/01-callbacks.md)**

---

**Made with ❤️ for JavaScript learners**
