# 📞 Callbacks in JavaScript

## 📑 Table of Contents
- [What are Callbacks?](#what-are-callbacks)
- [Callback Pattern](#callback-pattern)
- [Callback Hell](#callback-hell)
- [Error Handling](#error-handling)
- [Common Mistakes](#-common-mistakes)
- [Interview Tips](#-interview-tips)

---

## What are Callbacks?

A callback is a function passed as an argument to another function, to be executed later.

```javascript
function greet(name, callback) {
  console.log(`Hello, ${name}`);
  callback();
}

function sayGoodbye() {
  console.log('Goodbye!');
}

greet('John', sayGoodbye);
// Hello, John
// Goodbye!
```

---

## Callback Pattern

```javascript
// Asynchronous callback
setTimeout(() => {
  console.log('After 1 second');
}, 1000);

// Array methods
[1, 2, 3].forEach(num => {
  console.log(num);
});

// Event listeners
button.addEventListener('click', () => {
  console.log('Clicked!');
});
```

---

## Callback Hell

```javascript
// ❌ Callback hell (pyramid of doom)
getData(function(a) {
  getMoreData(a, function(b) {
    getMoreData(b, function(c) {
      getMoreData(c, function(d) {
        getMoreData(d, function(e) {
          // ...
        });
      });
    });
  });
});

// ✓ Better: Use Promises or async/await
```

---

## Error Handling

```javascript
// Node.js style: error-first callback
fs.readFile('file.txt', (err, data) => {
  if (err) {
    console.error('Error:', err);
    return;
  }
  console.log('Data:', data);
});

// Custom error handling
function fetchData(callback) {
  setTimeout(() => {
    const error = null;
    const data = {name: 'John'};
    callback(error, data);
  }, 1000);
}

fetchData((err, data) => {
  if (err) {
    console.error(err);
    return;
  }
  console.log(data);
});
```

---

## ⚠️ Common Mistakes

```javascript
// ❌ Callback not a function
setTimeout('console.log("Hi")', 1000);  // String, not function

// ✓ Pass function
setTimeout(() => console.log("Hi"), 1000);

// ❌ Forgetting to handle errors
readFile('file.txt', (err, data) => {
  // console.log(data);  // What if error?
});

// ✓ Handle errors
readFile('file.txt', (err, data) => {
  if (err) return console.error(err);
  console.log(data);
});
```

---

## 💼 Interview Tips

### Q1: What is a callback?

**Answer:**
A function passed as an argument to another function, executed later (often asynchronously).

### Q2: What is callback hell?

**Answer:**
Nested callbacks that make code hard to read and maintain. Also called "pyramid of doom".

Solution: Use Promises or async/await.

---

**[← Back: Execution Context](../06-advanced/04-execution-context.md)** | **[Next: Promises →](./02-promises.md)**

---

**Made with ❤️ for JavaScript learners**
