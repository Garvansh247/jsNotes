# 🎭 The `this` Keyword in JavaScript

## 📑 Table of Contents
- [What is `this`?](#what-is-this)
- [this in Different Contexts](#this-in-different-contexts)
- [Binding Rules](#binding-rules)
- [call, apply, and bind](#call-apply-and-bind)
- [Arrow Functions and this](#arrow-functions-and-this)
- [Common Mistakes](#-common-mistakes)
- [Interview Tips](#-interview-tips)
- [Practice Exercises](#practice-exercises)

---

## What is `this`?

`this` is a keyword that refers to the context in which a function is executed.

```javascript
const person = {
  name: "John",
  greet() {
    console.log(`Hello, I'm ${this.name}`);
  }
};

person.greet();  // "Hello, I'm John"
```

---

## this in Different Contexts

### Global Context

```javascript
console.log(this);  // Window object (browser) or global (Node.js)

function test() {
  console.log(this);  // Window (non-strict) or undefined (strict mode)
}
```

### Object Methods

```javascript
const obj = {
  name: "John",
  greet() {
    console.log(this.name);
  }
};

obj.greet();  // "John" (this refers to obj)
```

### Constructor Functions

```javascript
function Person(name) {
  this.name = name;
}

const john = new Person("John");
console.log(john.name);  // "John"
```

### Event Handlers

```javascript
button.addEventListener('click', function() {
  console.log(this);  // Button element
});
```

---

## Binding Rules

### 1. Default Binding

```javascript
function greet() {
  console.log(this);
}

greet();  // Window (or undefined in strict mode)
```

### 2. Implicit Binding

```javascript
const obj = {
  name: "John",
  greet() {
    console.log(this.name);
  }
};

obj.greet();  // "John" (this = obj)
```

### 3. Explicit Binding

```javascript
function greet() {
  console.log(this.name);
}

const person = {name: "John"};
greet.call(person);   // "John"
greet.apply(person);  // "John"
```

### 4. new Binding

```javascript
function Person(name) {
  this.name = name;
}

const john = new Person("John");
// this = new empty object
```

---

## call, apply, and bind

### call()

```javascript
function greet(greeting) {
  console.log(`${greeting}, ${this.name}`);
}

const person = {name: "John"};
greet.call(person, "Hello");  // "Hello, John"
```

### apply()

```javascript
function introduce(greeting, punctuation) {
  console.log(`${greeting}, I'm ${this.name}${punctuation}`);
}

const person = {name: "John"};
introduce.apply(person, ["Hello", "!"]);  // "Hello, I'm John!"
```

### bind()

```javascript
function greet() {
  console.log(`Hello, ${this.name}`);
}

const person = {name: "John"};
const boundGreet = greet.bind(person);
boundGreet();  // "Hello, John"

// Partial application
function multiply(a, b) {
  return a * b;
}

const double = multiply.bind(null, 2);
console.log(double(5));  // 10
```

---

## Arrow Functions and this

```javascript
// Arrow functions don't have their own `this`
const obj = {
  name: "John",
  greet: () => {
    console.log(this.name);  // undefined (lexical this)
  },
  greet2() {
    const inner = () => {
      console.log(this.name);  // "John" (inherits from greet2)
    };
    inner();
  }
};

obj.greet();   // undefined
obj.greet2();  // "John"
```

---

## ⚠️ Common Mistakes

### Losing `this` Context

```javascript
const obj = {
  name: "John",
  greet() {
    console.log(this.name);
  }
};

const greet = obj.greet;
greet();  // undefined (lost context)

// Fix with bind
const boundGreet = obj.greet.bind(obj);
boundGreet();  // "John"
```

---

## 💼 Interview Tips

### Q1: What is `this` in JavaScript?

**Answer:**
`this` is a keyword that refers to the context in which a function is executed. Its value depends on how the function is called, not where it's defined.

### Q2: What are the four binding rules for `this`?

**Answer:**
1. **Default**: Global object or undefined (strict mode)
2. **Implicit**: Object calling the method
3. **Explicit**: Using call/apply/bind
4. **new**: New object created by constructor

### Q3: How do arrow functions handle `this`?

**Answer:**
Arrow functions don't have their own `this`. They inherit `this` from the enclosing lexical scope.

---

## Practice Exercises

### Exercise 1: Fix `this`
Fix the following code so it logs "John":

```javascript
const person = {
  name: "John",
  greet() {
    setTimeout(function() {
      console.log(this.name);
    }, 1000);
  }
};

person.greet();  // undefined
```

<details>
<summary>Solution</summary>

```javascript
// Solution 1: Arrow function
const person = {
  name: "John",
  greet() {
    setTimeout(() => {
      console.log(this.name);  // "John"
    }, 1000);
  }
};

// Solution 2: bind
const person = {
  name: "John",
  greet() {
    setTimeout(function() {
      console.log(this.name);
    }.bind(this), 1000);
  }
};
```
</details>

---

**[← Back: Scope and Hoisting](./03-scope-and-hoisting.md)** | **[Next: Conditionals →](../04-control-flow/01-conditionals.md)**

---

**Made with ❤️ for JavaScript learners**
