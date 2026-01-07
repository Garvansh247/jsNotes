# ⏳ Async/Await in JavaScript

## 📑 Table of Contents
- [Async Functions](#async-functions)
- [Await Keyword](#await-keyword)
- [Error Handling](#error-handling)
- [Practical Examples](#practical-examples)
- [Common Mistakes](#-common-mistakes)
- [Interview Tips](#-interview-tips)

---

## Async Functions

```javascript
// Async function always returns a Promise
async function getData() {
  return 'Data';
}

getData().then(data => console.log(data));  // 'Data'

// Equivalent to:
function getData() {
  return Promise.resolve('Data');
}
```

---

## Await Keyword

```javascript
// Wait for Promise to resolve
async function fetchData() {
  const response = await fetch('https://api.example.com/data');
  const data = await response.json();
  return data;
}

fetchData().then(data => console.log(data));

// Compare with Promises:
function fetchDataPromise() {
  return fetch('https://api.example.com/data')
    .then(response => response.json());
}
```

---

## Error Handling

```javascript
// Using try/catch
async function getData() {
  try {
    const response = await fetch('https://api.example.com/data');
    const data = await response.json();
    return data;
  } catch (error) {
    console.error('Error:', error);
    throw error;
  }
}

// Or catch at call site
getData()
  .then(data => console.log(data))
  .catch(error => console.error(error));
```

---

## Practical Examples

```javascript
// Sequential execution
async function sequential() {
  const data1 = await fetchData1();
  const data2 = await fetchData2(data1);
  const data3 = await fetchData3(data2);
  return data3;
}

// Parallel execution
async function parallel() {
  const [data1, data2, data3] = await Promise.all([
    fetchData1(),
    fetchData2(),
    fetchData3()
  ]);
  return {data1, data2, data3};
}

// Mixed
async function mixed() {
  const data1 = await fetchData1();
  const [data2, data3] = await Promise.all([
    fetchData2(data1),
    fetchData3(data1)
  ]);
  return {data1, data2, data3};
}
```

---

## ⚠️ Common Mistakes

```javascript
// ❌ Forgetting await
async function getData() {
  const data = fetch('url');  // Returns Promise, not data!
  console.log(data);  // Promise object
}

// ✓ Use await
async function getData() {
  const data = await fetch('url');
  console.log(data);  // Actual data
}

// ❌ Unnecessary sequential awaits
async function slow() {
  const data1 = await fetch('url1');  // Wait
  const data2 = await fetch('url2');  // Then wait
  return {data1, data2};
}

// ✓ Parallel when possible
async function fast() {
  const [data1, data2] = await Promise.all([
    fetch('url1'),
    fetch('url2')
  ]);
  return {data1, data2};
}
```

---

## 💼 Interview Tips

### Q1: What does async/await do?

**Answer:**
Syntactic sugar over Promises that makes asynchronous code look synchronous. `async` functions return Promises, `await` pauses execution until Promise resolves.

### Q2: Can you use await outside async function?

**Answer:**
No, except at top level in modules (ES2022).

```javascript
// ❌ Error
const data = await fetch('url');

// ✓ Inside async function
async function getData() {
  const data = await fetch('url');
}

// ✓ Top-level await (modules only, ES2022)
// In module:
const data = await fetch('url');
```

### Q3: How do you handle errors with async/await?

**Answer:**
Use try/catch blocks:

```javascript
async function getData() {
  try {
    const data = await fetch('url');
    return data;
  } catch (error) {
    console.error(error);
  }
}
```

---

**[← Back: Promises](./02-promises.md)** | **[Next: Fetch API →](./04-fetch-api.md)**

---

**Made with ❤️ for JavaScript learners**
