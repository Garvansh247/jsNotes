# 🔁 Loops in JavaScript

## 📑 Table of Contents
- [for Loop](#for-loop)
- [while Loop](#while-loop)
- [do...while Loop](#dowhile-loop)
- [for...of Loop](#forof-loop)
- [for...in Loop](#forin-loop)
- [break and continue](#break-and-continue)
- [Common Mistakes](#-common-mistakes)
- [Interview Tips](#-interview-tips)

---

## for Loop

```javascript
// Basic for loop
for (let i = 0; i < 5; i++) {
  console.log(i);  // 0, 1, 2, 3, 4
}

// Reverse loop
for (let i = 5; i > 0; i--) {
  console.log(i);  // 5, 4, 3, 2, 1
}

// Step by 2
for (let i = 0; i < 10; i += 2) {
  console.log(i);  // 0, 2, 4, 6, 8
}

// Loop through array
const fruits = ['apple', 'banana', 'orange'];
for (let i = 0; i < fruits.length; i++) {
  console.log(fruits[i]);
}

// Nested loops
for (let i = 1; i <= 3; i++) {
  for (let j = 1; j <= 3; j++) {
    console.log(`${i}, ${j}`);
  }
}
```

---

## while Loop

```javascript
// Basic while loop
let i = 0;
while (i < 5) {
  console.log(i);
  i++;
}

// Find first power of 2 greater than 100
let num = 1;
while (num <= 100) {
  num *= 2;
}
console.log(num);  // 128

// Infinite loop (be careful!)
// while (true) {
//   console.log("Infinite");
// }
```

---

## do...while Loop

```javascript
// Executes at least once
let i = 0;
do {
  console.log(i);
  i++;
} while (i < 5);

// Example: menu prompt
let answer;
do {
  answer = prompt("Continue? (yes/no)");
} while (answer !== "yes" && answer !== "no");
```

---

## for...of Loop

```javascript
// Iterate over array values
const fruits = ['apple', 'banana', 'orange'];
for (const fruit of fruits) {
  console.log(fruit);
}

// Iterate over string
const str = "Hello";
for (const char of str) {
  console.log(char);  // H, e, l, l, o
}

// With destructuring
const users = [
  {name: "John", age: 30},
  {name: "Jane", age: 25}
];

for (const {name, age} of users) {
  console.log(`${name} is ${age} years old`);
}
```

---

## for...in Loop

```javascript
// Iterate over object keys
const person = {
  name: "John",
  age: 30,
  city: "New York"
};

for (const key in person) {
  console.log(`${key}: ${person[key]}`);
}

// Arrays (not recommended)
const arr = ['a', 'b', 'c'];
for (const index in arr) {
  console.log(index);  // "0", "1", "2" (strings!)
}
```

---

## break and continue

```javascript
// break: exit loop
for (let i = 0; i < 10; i++) {
  if (i === 5) break;
  console.log(i);  // 0, 1, 2, 3, 4
}

// continue: skip iteration
for (let i = 0; i < 10; i++) {
  if (i % 2 === 0) continue;
  console.log(i);  // 1, 3, 5, 7, 9
}

// Labeled statements
outer: for (let i = 0; i < 3; i++) {
  for (let j = 0; j < 3; j++) {
    if (i === 1 && j === 1) break outer;
    console.log(`${i}, ${j}`);
  }
}
```

---

## ⚠️ Common Mistakes

```javascript
// ❌ Infinite loop
let i = 0;
while (i < 5) {
  console.log(i);
  // Forgot i++
}

// ❌ Using for...in on arrays
const arr = [1, 2, 3];
for (const i in arr) {
  console.log(i);  // "0", "1", "2" (strings!)
}

// ✓ Use for...of for arrays
for (const val of arr) {
  console.log(val);  // 1, 2, 3
}
```

---

## 💼 Interview Tips

### Q1: What's the difference between for...of and for...in?

**Answer:**
- `for...of`: Iterates over iterable values (arrays, strings, etc.)
- `for...in`: Iterates over enumerable properties (object keys)

```javascript
const arr = ['a', 'b', 'c'];
for (const val of arr) console.log(val);  // a, b, c
for (const key in arr) console.log(key);  // 0, 1, 2

const obj = {x: 1, y: 2};
for (const key in obj) console.log(key);  // x, y
// for (const val of obj) {}  // Error: not iterable
```

### Q2: When to use which loop?

**Answer:**
- **for**: Known number of iterations
- **while**: Unknown iterations, condition-based
- **do...while**: Must execute at least once
- **for...of**: Iterate array values
- **for...in**: Iterate object keys

---

**[← Back: Conditionals](./01-conditionals.md)** | **[Next: Iteration Methods →](./03-iteration-methods.md)**

---

**Made with ❤️ for JavaScript learners**
