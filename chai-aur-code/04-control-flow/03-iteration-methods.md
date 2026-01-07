# 🔄 Iteration Methods in JavaScript

## 📑 Table of Contents
- [forEach](#foreach)
- [map](#map)
- [filter](#filter)
- [reduce](#reduce)
- [find and findIndex](#find-and-findindex)
- [some and every](#some-and-every)
- [Method Chaining](#method-chaining)
- [Common Mistakes](#-common-mistakes)
- [Interview Tips](#-interview-tips)
- [Practice Exercises](#practice-exercises)

---

## forEach

Executes a function for each array element.

```javascript
const numbers = [1, 2, 3, 4, 5];

numbers.forEach((num, index, array) => {
  console.log(`Index ${index}: ${num}`);
});

// Practical example: sum array
let sum = 0;
numbers.forEach(num => sum += num);
console.log(sum);  // 15

// Note: Cannot break or continue
// Use for...of if you need that
```

---

## map

Creates a new array with transformed elements.

```javascript
const numbers = [1, 2, 3, 4, 5];

// Double each number
const doubled = numbers.map(num => num * 2);
console.log(doubled);  // [2, 4, 6, 8, 10]

// Square each number
const squared = numbers.map(num => num ** 2);
console.log(squared);  // [1, 4, 9, 16, 25]

// Extract property from objects
const users = [
  {name: 'John', age: 30},
  {name: 'Jane', age: 25}
];

const names = users.map(user => user.name);
console.log(names);  // ['John', 'Jane']

// With index
const indexed = numbers.map((num, i) => `${i}: ${num}`);
console.log(indexed);  // ['0: 1', '1: 2', ...]
```

---

## filter

Creates a new array with elements that pass a test.

```javascript
const numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];

// Get even numbers
const evens = numbers.filter(num => num % 2 === 0);
console.log(evens);  // [2, 4, 6, 8, 10]

// Get numbers > 5
const greaterThan5 = numbers.filter(num => num > 5);
console.log(greaterThan5);  // [6, 7, 8, 9, 10]

// Filter objects
const users = [
  {name: 'John', age: 30, active: true},
  {name: 'Jane', age: 25, active: false},
  {name: 'Bob', age: 35, active: true}
];

const activeUsers = users.filter(user => user.active);
console.log(activeUsers);
// [{name: 'John', age: 30, active: true}, {name: 'Bob', age: 35, active: true}]

// Remove duplicates
const arr = [1, 2, 2, 3, 3, 4, 5, 5];
const unique = arr.filter((value, index, self) => {
  return self.indexOf(value) === index;
});
console.log(unique);  // [1, 2, 3, 4, 5]
```

---

## reduce

Reduces array to a single value.

```javascript
const numbers = [1, 2, 3, 4, 5];

// Sum
const sum = numbers.reduce((acc, curr) => acc + curr, 0);
console.log(sum);  // 15

// Product
const product = numbers.reduce((acc, curr) => acc * curr, 1);
console.log(product);  // 120

// Max value
const max = numbers.reduce((acc, curr) => Math.max(acc, curr));
console.log(max);  // 5

// Count occurrences
const fruits = ['apple', 'banana', 'apple', 'orange', 'banana', 'apple'];
const count = fruits.reduce((acc, fruit) => {
  acc[fruit] = (acc[fruit] || 0) + 1;
  return acc;
}, {});
console.log(count);  // {apple: 3, banana: 2, orange: 1}

// Flatten array
const nested = [[1, 2], [3, 4], [5, 6]];
const flattened = nested.reduce((acc, curr) => acc.concat(curr), []);
console.log(flattened);  // [1, 2, 3, 4, 5, 6]

// Group by property
const users = [
  {name: 'John', role: 'admin'},
  {name: 'Jane', role: 'user'},
  {name: 'Bob', role: 'admin'}
];

const grouped = users.reduce((acc, user) => {
  const role = user.role;
  if (!acc[role]) acc[role] = [];
  acc[role].push(user);
  return acc;
}, {});
console.log(grouped);
// {admin: [{...}, {...}], user: [{...}]}
```

---

## find and findIndex

Find first element or index that matches condition.

```javascript
const numbers = [1, 5, 10, 15, 20];

// find: returns first match
const found = numbers.find(num => num > 10);
console.log(found);  // 15

// Returns undefined if not found
const notFound = numbers.find(num => num > 100);
console.log(notFound);  // undefined

// findIndex: returns index
const index = numbers.findIndex(num => num > 10);
console.log(index);  // 3

// Returns -1 if not found
const notFoundIndex = numbers.findIndex(num => num > 100);
console.log(notFoundIndex);  // -1

// Find object
const users = [
  {id: 1, name: 'John'},
  {id: 2, name: 'Jane'},
  {id: 3, name: 'Bob'}
];

const user = users.find(u => u.id === 2);
console.log(user);  // {id: 2, name: 'Jane'}
```

---

## some and every

Check if some or all elements pass a test.

```javascript
const numbers = [1, 2, 3, 4, 5];

// some: at least one passes
const hasEven = numbers.some(num => num % 2 === 0);
console.log(hasEven);  // true

const hasNegative = numbers.some(num => num < 0);
console.log(hasNegative);  // false

// every: all must pass
const allPositive = numbers.every(num => num > 0);
console.log(allPositive);  // true

const allEven = numbers.every(num => num % 2 === 0);
console.log(allEven);  // false

// Practical examples
const users = [
  {name: 'John', age: 30},
  {name: 'Jane', age: 25},
  {name: 'Bob', age: 35}
];

const hasAdult = users.some(user => user.age >= 18);
console.log(hasAdult);  // true

const allAdults = users.every(user => user.age >= 18);
console.log(allAdults);  // true
```

---

## Method Chaining

Combine multiple array methods for powerful transformations.

```javascript
const numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];

// Get sum of squared even numbers
const result = numbers
  .filter(n => n % 2 === 0)     // [2, 4, 6, 8, 10]
  .map(n => n ** 2)             // [4, 16, 36, 64, 100]
  .reduce((sum, n) => sum + n, 0);  // 220

console.log(result);  // 220

// Process user data
const users = [
  {name: 'John', age: 30, active: true},
  {name: 'Jane', age: 25, active: false},
  {name: 'Bob', age: 35, active: true},
  {name: 'Alice', age: 28, active: true}
];

const activeUserNames = users
  .filter(user => user.active)
  .map(user => user.name)
  .sort();

console.log(activeUserNames);  // ['Alice', 'Bob', 'John']

// Average age of active users
const avgAge = users
  .filter(user => user.active)
  .map(user => user.age)
  .reduce((sum, age, _, arr) => sum + age / arr.length, 0);

console.log(avgAge);  // 31
```

---

## ⚠️ Common Mistakes

### 1. Using forEach for Transformation

```javascript
// ❌ Wrong: Using forEach to transform
let doubled = [];
numbers.forEach(n => doubled.push(n * 2));

// ✓ Correct: Use map
let doubled = numbers.map(n => n * 2);
```

### 2. Forgetting to Return in reduce

```javascript
// ❌ Wrong: No return
const sum = numbers.reduce((acc, num) => {
  acc + num;  // Forgot return!
}, 0);

// ✓ Correct
const sum = numbers.reduce((acc, num) => {
  return acc + num;
}, 0);

// ✓ Better: Implicit return
const sum = numbers.reduce((acc, num) => acc + num, 0);
```

### 3. Not Providing Initial Value to reduce

```javascript
// ❌ Risky: No initial value
const sum = numbers.reduce((acc, num) => acc + num);

// ✓ Safe: Provide initial value
const sum = numbers.reduce((acc, num) => acc + num, 0);
```

---

## 💼 Interview Tips

### Q1: What's the difference between map and forEach?

**Answer:**
- `map`: Returns new array with transformed elements
- `forEach`: Executes function, returns undefined

```javascript
const arr = [1, 2, 3];

const doubled = arr.map(n => n * 2);  // [2, 4, 6]
const result = arr.forEach(n => n * 2);  // undefined
```

### Q2: When to use filter vs find?

**Answer:**
- `filter`: Returns array of all matches
- `find`: Returns first match only

```javascript
const arr = [1, 2, 3, 4, 5];

arr.filter(n => n > 2);  // [3, 4, 5]
arr.find(n => n > 2);    // 3
```

### Q3: What's reduce useful for?

**Answer:**
- Summing/multiplying values
- Finding min/max
- Counting occurrences
- Flattening arrays
- Grouping objects
- Any operation that reduces array to single value

---

## Practice Exercises

### Exercise 1: Get Average
Calculate average of numbers.

```javascript
function average(arr) {
  // Your code here using reduce
}

console.log(average([1, 2, 3, 4, 5]));  // 3
```

<details>
<summary>Solution</summary>

```javascript
function average(arr) {
  return arr.reduce((sum, num) => sum + num, 0) / arr.length;
}
```
</details>

### Exercise 2: Filter and Map
Get names of users over 25.

```javascript
const users = [
  {name: 'John', age: 30},
  {name: 'Jane', age: 25},
  {name: 'Bob', age: 35}
];

// Your code here

// Expected: ['John', 'Bob']
```

<details>
<summary>Solution</summary>

```javascript
const names = users
  .filter(user => user.age > 25)
  .map(user => user.name);

console.log(names);  // ['John', 'Bob']
```
</details>

---

**[← Back: Loops](./02-loops.md)** | **[Next: DOM Basics →](../05-dom-manipulation/01-dom-basics.md)**

---

**Made with ❤️ for JavaScript learners**
