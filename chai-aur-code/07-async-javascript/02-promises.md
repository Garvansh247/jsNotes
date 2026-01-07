# 🤝 Promises in JavaScript

## 📑 Table of Contents
- [What is a Promise?](#what-is-a-promise)
- [Promise States](#promise-states)
- [Creating Promises](#creating-promises)
- [then/catch/finally](#thencatchfinally)
- [Promise Methods](#promise-methods)
- [Common Mistakes](#-common-mistakes)
- [Interview Tips](#-interview-tips)

---

## What is a Promise?

A Promise represents a value that may be available now, in the future, or never.

```javascript
const promise = new Promise((resolve, reject) => {
  setTimeout(() => {
    resolve('Success!');
  }, 1000);
});

promise.then(result => {
  console.log(result);  // 'Success!'
});
```

---

## Promise States

1. **Pending**: Initial state
2. **Fulfilled**: Operation completed successfully
3. **Rejected**: Operation failed

```javascript
const promise = new Promise((resolve, reject) => {
  const success = true;
  
  if (success) {
    resolve('Success!');
  } else {
    reject('Error!');
  }
});
```

---

## Creating Promises

```javascript
// Basic promise
const promise = new Promise((resolve, reject) => {
  setTimeout(() => {
    resolve('Done!');
  }, 1000);
});

// Immediately resolved
const resolved = Promise.resolve('Immediate value');

// Immediately rejected
const rejected = Promise.reject('Error');
```

---

## then/catch/finally

```javascript
fetch('https://api.example.com/data')
  .then(response => response.json())
  .then(data => console.log(data))
  .catch(error => console.error(error))
  .finally(() => console.log('Done'));

// Chaining
getData()
  .then(a => getMoreData(a))
  .then(b => getMoreData(b))
  .then(c => console.log(c))
  .catch(error => console.error(error));
```

---

## Promise Methods

```javascript
// Promise.all: Wait for all
Promise.all([promise1, promise2, promise3])
  .then(results => console.log(results))
  .catch(error => console.error(error));

// Promise.race: First to complete
Promise.race([promise1, promise2])
  .then(result => console.log(result));

// Promise.allSettled: Wait for all (ES2020)
Promise.allSettled([promise1, promise2])
  .then(results => console.log(results));
// [{status: 'fulfilled', value: ...}, {status: 'rejected', reason: ...}]

// Promise.any: First fulfilled (ES2021)
Promise.any([promise1, promise2])
  .then(result => console.log(result));
```

---

## ⚠️ Common Mistakes

```javascript
// ❌ Forgetting to return in then
promise
  .then(data => {
    processData(data);  // Not returned!
  })
  .then(result => {
    console.log(result);  // undefined
  });

// ✓ Return the value/promise
promise
  .then(data => {
    return processData(data);
  })
  .then(result => {
    console.log(result);  // Correct value
  });

// ❌ Not handling rejections
promise.then(data => console.log(data));
// Unhandled promise rejection!

// ✓ Always use catch
promise
  .then(data => console.log(data))
  .catch(error => console.error(error));
```

---

## 💼 Interview Tips

### Q1: What are the Promise states?

**Answer:**
- **Pending**: Initial state
- **Fulfilled**: Success
- **Rejected**: Failure

### Q2: What's the difference between Promise.all and Promise.race?

**Answer:**
- `Promise.all`: Waits for all promises to fulfill (or one to reject)
- `Promise.race`: Resolves/rejects with first promise that settles

### Q3: How do you convert a callback to a Promise?

**Answer:**
```javascript
function getData(callback) {
  setTimeout(() => callback(null, 'data'), 1000);
}

// Convert to Promise
function getDataPromise() {
  return new Promise((resolve, reject) => {
    getData((err, data) => {
      if (err) reject(err);
      else resolve(data);
    });
  });
}
```

---

**[← Back: Callbacks](./01-callbacks.md)** | **[Next: Async/Await →](./03-async-await.md)**

---

**Made with ❤️ for JavaScript learners**
