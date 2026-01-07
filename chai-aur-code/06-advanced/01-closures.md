# 🔒 Closures in JavaScript

## 📑 Table of Contents
- [What is a Closure?](#what-is-a-closure)
- [Lexical Scope](#lexical-scope)
- [Practical Examples](#practical-examples)
- [Common Use Cases](#common-use-cases)
- [Memory Considerations](#memory-considerations)
- [Common Mistakes](#-common-mistakes)
- [Interview Tips](#-interview-tips)

---

## What is a Closure?

A closure is a function that has access to its outer function's scope, even after the outer function has returned.

```javascript
function outer() {
  let count = 0;
  
  function inner() {
    count++;
    console.log(count);
  }
  
  return inner;
}

const counter = outer();
counter();  // 1
counter();  // 2
counter();  // 3
// 'count' is preserved in closure
```

---

## Lexical Scope

```javascript
const globalVar = 'global';

function outer() {
  const outerVar = 'outer';
  
  function inner() {
    const innerVar = 'inner';
    console.log(globalVar);  // Accessible
    console.log(outerVar);   // Accessible
    console.log(innerVar);   // Accessible
  }
  
  inner();
}

outer();
```

---

## Practical Examples

### Counter

```javascript
function createCounter() {
  let count = 0;
  
  return {
    increment() { return ++count; },
    decrement() { return --count; },
    get() { return count; }
  };
}

const counter = createCounter();
console.log(counter.increment());  // 1
console.log(counter.increment());  // 2
console.log(counter.get());        // 2
console.log(counter.decrement());  // 1
```

### Private Variables

```javascript
function createPerson(name) {
  let _name = name;  // Private variable
  
  return {
    getName() { return _name; },
    setName(newName) { _name = newName; }
  };
}

const person = createPerson('John');
console.log(person.getName());  // 'John'
person.setName('Jane');
console.log(person.getName());  // 'Jane'
// console.log(person._name);   // undefined (private)
```

---

## Common Use Cases

### Module Pattern

```javascript
const calculator = (function() {
  let result = 0;
  
  return {
    add(x) {
      result += x;
      return this;
    },
    subtract(x) {
      result -= x;
      return this;
    },
    getResult() {
      return result;
    }
  };
})();

calculator.add(5).add(3).subtract(2);
console.log(calculator.getResult());  // 6
```

### Function Factories

```javascript
function makeMultiplier(factor) {
  return function(number) {
    return number * factor;
  };
}

const double = makeMultiplier(2);
const triple = makeMultiplier(3);

console.log(double(5));  // 10
console.log(triple(5));  // 15
```

### Event Handlers

```javascript
function setupButtons() {
  for (let i = 0; i < 3; i++) {
    const button = document.getElementById(`btn-${i}`);
    button.addEventListener('click', function() {
      console.log(`Button ${i} clicked`);
    });
  }
}
```

---

## Memory Considerations

```javascript
// Closures can cause memory leaks if not careful
function createLargeArray() {
  const largeArray = new Array(1000000).fill('data');
  
  return function() {
    console.log(largeArray.length);
  };
}

const fn = createLargeArray();
// largeArray stays in memory as long as fn exists

// To release memory:
fn = null;
```

---

## ⚠️ Common Mistakes

### Loop Problem

```javascript
// ❌ Wrong: var creates closure issue
for (var i = 0; i < 3; i++) {
  setTimeout(function() {
    console.log(i);  // 3, 3, 3
  }, 1000);
}

// ✓ Correct: let creates block scope
for (let i = 0; i < 3; i++) {
  setTimeout(function() {
    console.log(i);  // 0, 1, 2
  }, 1000);
}

// ✓ Alternative: IIFE
for (var i = 0; i < 3; i++) {
  (function(index) {
    setTimeout(function() {
      console.log(index);  // 0, 1, 2
    }, 1000);
  })(i);
}
```

---

## 💼 Interview Tips

### Q1: What is a closure?

**Answer:**
A closure is a function that retains access to its lexical scope, even when the function executes outside that scope.

### Q2: Give a practical use case for closures.

**Answer:**
- Data privacy (private variables)
- Function factories
- Module pattern
- Event handlers
- Callbacks

### Q3: Can closures cause memory leaks?

**Answer:**
Yes, if closures retain references to large objects that are no longer needed, they prevent garbage collection.

---

**[← Back: Events](../05-dom-manipulation/04-events.md)** | **[Next: Prototypes →](./02-prototypes.md)**

---

**Made with ❤️ for JavaScript learners**
