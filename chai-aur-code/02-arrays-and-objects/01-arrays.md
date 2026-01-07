# 📚 Arrays in JavaScript

## 📑 Table of Contents
- [Array Basics](#array-basics)
- [Creating Arrays](#creating-arrays)
- [Accessing Elements](#accessing-elements)
- [Modifying Arrays](#modifying-arrays)
- [Array Destructuring](#array-destructuring)
- [Array Length](#array-length)
- [Multidimensional Arrays](#multidimensional-arrays)
- [Array Type Checking](#array-type-checking)
- [Common Mistakes](#-common-mistakes)
- [Interview Tips](#-interview-tips)
- [Practice Exercises](#practice-exercises)

---

## Array Basics

Arrays are ordered collections that can store multiple values of any type. They are one of the most commonly used data structures in JavaScript.

```javascript
// Array with different types
let mixed = [1, "hello", true, null, {name: "John"}, [1, 2, 3]];
console.log(mixed); // [1, "hello", true, null, {name: "John"}, [1, 2, 3]]

// Arrays are objects
console.log(typeof []); // "object"
console.log(Array.isArray([])); // true ✓
```

---

## Creating Arrays

### Array Literal (Most Common)

```javascript
// Empty array
let empty = [];
console.log(empty); // []

// Array with elements
let numbers = [1, 2, 3, 4, 5];
console.log(numbers); // [1, 2, 3, 4, 5]

// Array with different types
let mixed = [1, "two", true, null, undefined];
console.log(mixed);

// Array with trailing comma (allowed)
let fruits = ["apple", "banana", "orange",];
console.log(fruits); // ["apple", "banana", "orange"]
```

### Array Constructor

```javascript
// Empty array
let arr1 = new Array();
console.log(arr1); // []

// Array with length
let arr2 = new Array(5);
console.log(arr2); // [empty × 5]
console.log(arr2.length); // 5

// Array with elements (2 or more arguments)
let arr3 = new Array(1, 2, 3);
console.log(arr3); // [1, 2, 3]

// Common mistake: single number creates length
let mistake = new Array(10);
console.log(mistake); // [empty × 10], not [10]

// Use Array.of() to avoid confusion
let correct = Array.of(10);
console.log(correct); // [10]
```

### Array.from()

```javascript
// From string
let chars = Array.from("Hello");
console.log(chars); // ["H", "e", "l", "l", "o"]

// From array-like object
let arrayLike = {0: "a", 1: "b", 2: "c", length: 3};
let arr = Array.from(arrayLike);
console.log(arr); // ["a", "b", "c"]

// From Set
let set = new Set([1, 2, 3, 3, 4]);
let arrFromSet = Array.from(set);
console.log(arrFromSet); // [1, 2, 3, 4]

// With mapping function
let numbers = Array.from([1, 2, 3], x => x * 2);
console.log(numbers); // [2, 4, 6]

// Create range
let range = Array.from({length: 5}, (_, i) => i);
console.log(range); // [0, 1, 2, 3, 4]

let range2 = Array.from({length: 5}, (_, i) => i + 1);
console.log(range2); // [1, 2, 3, 4, 5]
```

### Array.of()

```javascript
// Creates array from arguments
let arr1 = Array.of(1);
console.log(arr1); // [1]

let arr2 = Array.of(1, 2, 3);
console.log(arr2); // [1, 2, 3]

let arr3 = Array.of(10);
console.log(arr3); // [10] (not [empty × 10])

// Compare with Array constructor
console.log(new Array(3)); // [empty × 3]
console.log(Array.of(3)); // [3]
```

### Spread Operator

```javascript
// Clone array
let original = [1, 2, 3];
let clone = [...original];
console.log(clone); // [1, 2, 3]

// Merge arrays
let arr1 = [1, 2];
let arr2 = [3, 4];
let merged = [...arr1, ...arr2];
console.log(merged); // [1, 2, 3, 4]

// Add elements
let extended = [0, ...arr1, 2.5, ...arr2, 5];
console.log(extended); // [0, 1, 2, 2.5, 3, 4, 5]

// Convert string to array
let str = "Hello";
let charArray = [...str];
console.log(charArray); // ["H", "e", "l", "l", "o"]
```

---

## Accessing Elements

### Index Access

```javascript
let fruits = ["apple", "banana", "orange", "mango"];

// Positive indices (0-based)
console.log(fruits[0]); // "apple"
console.log(fruits[1]); // "banana"
console.log(fruits[3]); // "mango"

// Out of bounds
console.log(fruits[10]); // undefined

// Negative indices (not directly supported, but can calculate)
console.log(fruits[fruits.length - 1]); // "mango" (last element)
console.log(fruits[fruits.length - 2]); // "orange" (second to last)

// at() method (ES2022) - supports negative indices
console.log(fruits.at(0)); // "apple"
console.log(fruits.at(-1)); // "mango" (last)
console.log(fruits.at(-2)); // "orange" (second to last)
```

### First and Last Elements

```javascript
let numbers = [10, 20, 30, 40, 50];

// First element
let first = numbers[0];
console.log(first); // 10

// Last element (multiple ways)
let last1 = numbers[numbers.length - 1];
let last2 = numbers.at(-1);
let last3 = numbers.slice(-1)[0];
console.log(last1, last2, last3); // 50 50 50
```

---

## Modifying Arrays

### Changing Elements

```javascript
let fruits = ["apple", "banana", "orange"];

// Change element
fruits[1] = "grape";
console.log(fruits); // ["apple", "grape", "orange"]

// Add element beyond length (creates sparse array)
fruits[5] = "mango";
console.log(fruits); // ["apple", "grape", "orange", empty × 2, "mango"]
console.log(fruits.length); // 6
console.log(fruits[3]); // undefined
console.log(fruits[4]); // undefined
```

### Adding Elements

```javascript
let arr = [1, 2, 3];

// push() - add to end
arr.push(4);
console.log(arr); // [1, 2, 3, 4]

arr.push(5, 6);
console.log(arr); // [1, 2, 3, 4, 5, 6]

// unshift() - add to beginning
arr.unshift(0);
console.log(arr); // [0, 1, 2, 3, 4, 5, 6]

arr.unshift(-2, -1);
console.log(arr); // [-2, -1, 0, 1, 2, 3, 4, 5, 6]

// Direct assignment
arr[arr.length] = 7;
console.log(arr); // [-2, -1, 0, 1, 2, 3, 4, 5, 6, 7]
```

### Removing Elements

```javascript
let arr = [1, 2, 3, 4, 5];

// pop() - remove from end
let last = arr.pop();
console.log(last); // 5
console.log(arr); // [1, 2, 3, 4]

// shift() - remove from beginning
let first = arr.shift();
console.log(first); // 1
console.log(arr); // [2, 3, 4]

// delete operator (creates hole, not recommended)
delete arr[1];
console.log(arr); // [2, empty, 4]
console.log(arr.length); // 3 (length unchanged!)

// splice() - remove from middle
arr = [1, 2, 3, 4, 5];
let removed = arr.splice(2, 1); // Remove 1 element at index 2
console.log(removed); // [3]
console.log(arr); // [1, 2, 4, 5]
```

### Clearing Arrays

```javascript
let arr = [1, 2, 3, 4, 5];

// Method 1: Set length to 0
arr.length = 0;
console.log(arr); // []

// Method 2: Assign new empty array
arr = [1, 2, 3];
arr = [];
console.log(arr); // []

// Method 3: splice
arr = [1, 2, 3];
arr.splice(0, arr.length);
console.log(arr); // []

// Method 4: pop in loop
arr = [1, 2, 3];
while (arr.length > 0) {
  arr.pop();
}
console.log(arr); // []
```

---

## Array Destructuring

### Basic Destructuring

```javascript
let fruits = ["apple", "banana", "orange"];

// Traditional way
let fruit1 = fruits[0];
let fruit2 = fruits[1];
let fruit3 = fruits[2];

// Destructuring (ES6)
let [a, b, c] = fruits;
console.log(a, b, c); // "apple" "banana" "orange"

// Skip elements
let [first, , third] = fruits;
console.log(first, third); // "apple" "orange"

// Fewer variables than elements
let [x] = fruits;
console.log(x); // "apple"

let [y, z] = fruits;
console.log(y, z); // "apple" "banana"
```

### Default Values

```javascript
let arr = [1];

// Without default
let [a, b] = arr;
console.log(a, b); // 1 undefined

// With default
let [x, y = 10] = arr;
console.log(x, y); // 1 10

// Default is used only if undefined
let arr2 = [1, null];
let [p, q = 10] = arr2;
console.log(p, q); // 1 null (null is not undefined)
```

### Rest Pattern

```javascript
let numbers = [1, 2, 3, 4, 5];

// Rest of elements
let [first, ...rest] = numbers;
console.log(first); // 1
console.log(rest); // [2, 3, 4, 5]

// Skip and rest
let [a, , ...others] = numbers;
console.log(a); // 1
console.log(others); // [3, 4, 5]

// Rest must be last
// let [...rest, last] = numbers; // ❌ SyntaxError
```

### Nested Destructuring

```javascript
let nested = [1, [2, 3], 4];

// Destructure nested array
let [a, [b, c], d] = nested;
console.log(a, b, c, d); // 1 2 3 4

// Mixed
let data = [1, [2, [3, 4]]];
let [x, [y, [z, w]]] = data;
console.log(x, y, z, w); // 1 2 3 4
```

### Swapping Variables

```javascript
let a = 1;
let b = 2;

// Traditional swap (needs temp variable)
let temp = a;
a = b;
b = temp;
console.log(a, b); // 2 1

// Destructuring swap (no temp needed)
[a, b] = [b, a];
console.log(a, b); // 1 2
```

---

## Array Length

### Understanding Length

```javascript
let arr = [1, 2, 3, 4, 5];
console.log(arr.length); // 5

// Length is highest index + 1
arr[10] = 10;
console.log(arr.length); // 11 (not 6!)
console.log(arr); // [1, 2, 3, 4, 5, empty × 5, 10]

// Empty slots don't have values
console.log(arr[7]); // undefined
```

### Modifying Length

```javascript
let arr = [1, 2, 3, 4, 5];

// Truncate array
arr.length = 3;
console.log(arr); // [1, 2, 3]

// Clear array
arr.length = 0;
console.log(arr); // []

// Extend array (creates empty slots)
arr = [1, 2, 3];
arr.length = 5;
console.log(arr); // [1, 2, 3, empty × 2]
console.log(arr[4]); // undefined
```

---

## Multidimensional Arrays

### 2D Arrays (Matrix)

```javascript
// Create 2D array
let matrix = [
  [1, 2, 3],
  [4, 5, 6],
  [7, 8, 9]
];

// Access elements
console.log(matrix[0][0]); // 1
console.log(matrix[1][2]); // 6
console.log(matrix[2][1]); // 8

// Modify elements
matrix[1][1] = 50;
console.log(matrix);
// [[1, 2, 3], [4, 50, 6], [7, 8, 9]]

// Iterate 2D array
for (let i = 0; i < matrix.length; i++) {
  for (let j = 0; j < matrix[i].length; j++) {
    console.log(`matrix[${i}][${j}] = ${matrix[i][j]}`);
  }
}
```

### Create 2D Array Dynamically

```javascript
// Create 3x3 matrix filled with zeros
let rows = 3, cols = 3;
let matrix = Array.from({length: rows}, () => Array(cols).fill(0));
console.log(matrix);
// [[0, 0, 0], [0, 0, 0], [0, 0, 0]]

// Create 2D array with values
let matrix2 = Array.from({length: 3}, (_, i) => 
  Array.from({length: 3}, (_, j) => i * 3 + j + 1)
);
console.log(matrix2);
// [[1, 2, 3], [4, 5, 6], [7, 8, 9]]
```

### 3D Arrays

```javascript
// Tic-tac-toe games (multiple boards)
let games = [
  [["X", "O", "X"], ["O", "X", "O"], ["O", "X", "X"]],
  [["O", "X", "O"], ["X", "O", "X"], ["X", "O", "X"]],
];

console.log(games[0][1][2]); // "O" (game 0, row 1, col 2)
```

---

## Array Type Checking

### Checking if Array

```javascript
let arr = [1, 2, 3];
let obj = {0: 1, 1: 2, length: 2};

// Array.isArray() - most reliable
console.log(Array.isArray(arr)); // true
console.log(Array.isArray(obj)); // false
console.log(Array.isArray("string")); // false

// typeof (not reliable for arrays)
console.log(typeof arr); // "object"
console.log(typeof obj); // "object"

// instanceof
console.log(arr instanceof Array); // true
console.log(obj instanceof Array); // false

// constructor property
console.log(arr.constructor === Array); // true

// Object.prototype.toString
console.log(Object.prototype.toString.call(arr)); // "[object Array]"
```

### Empty Array Check

```javascript
let arr1 = [];
let arr2 = [1, 2, 3];

// Check if array is empty
function isEmpty(arr) {
  return Array.isArray(arr) && arr.length === 0;
}

console.log(isEmpty(arr1)); // true
console.log(isEmpty(arr2)); // false
console.log(isEmpty(null)); // false
console.log(isEmpty(undefined)); // false
```

---

## ⚠️ Common Mistakes

### 1. Modifying Array While Iterating

```javascript
let arr = [1, 2, 3, 4, 5];

// ❌ Wrong: Modifying during iteration
for (let i = 0; i < arr.length; i++) {
  if (arr[i] % 2 === 0) {
    arr.splice(i, 1); // Skips elements!
  }
}

// ✓ Correct: Iterate backwards
arr = [1, 2, 3, 4, 5];
for (let i = arr.length - 1; i >= 0; i--) {
  if (arr[i] % 2 === 0) {
    arr.splice(i, 1);
  }
}
console.log(arr); // [1, 3, 5]

// ✓ Better: Use filter
arr = [1, 2, 3, 4, 5];
arr = arr.filter(x => x % 2 !== 0);
console.log(arr); // [1, 3, 5]
```

### 2. Arrays are Reference Types

```javascript
let arr1 = [1, 2, 3];
let arr2 = arr1; // Reference, not copy!

arr2.push(4);
console.log(arr1); // [1, 2, 3, 4] (modified!)
console.log(arr2); // [1, 2, 3, 4]

// ✓ Correct: Create a copy
let arr3 = [1, 2, 3];
let arr4 = [...arr3]; // or arr3.slice()
arr4.push(4);
console.log(arr3); // [1, 2, 3] (unchanged)
console.log(arr4); // [1, 2, 3, 4]
```

### 3. Array Constructor Gotcha

```javascript
// ❌ Wrong: Single number creates array with length
let wrong = new Array(10);
console.log(wrong); // [empty × 10]

// ✓ Correct: Use Array.of() or literal
let correct1 = Array.of(10);
let correct2 = [10];
console.log(correct1); // [10]
console.log(correct2); // [10]
```

### 4. Checking if Array

```javascript
let arr = [1, 2, 3];

// ❌ Wrong: typeof returns "object"
if (typeof arr === "array") { // Never true!
  console.log("Is array");
}

// ✓ Correct: Use Array.isArray()
if (Array.isArray(arr)) {
  console.log("Is array"); // ✓
}
```

---

## 💼 Interview Tips

### Q1: What are the ways to create an array in JavaScript?

**Answer:**
```javascript
// 1. Array literal (most common)
let arr1 = [1, 2, 3];

// 2. Array constructor
let arr2 = new Array(1, 2, 3);

// 3. Array.of()
let arr3 = Array.of(1, 2, 3);

// 4. Array.from()
let arr4 = Array.from([1, 2, 3]);
let arr5 = Array.from("abc"); // ["a", "b", "c"]

// 5. Spread operator
let arr6 = [...[1, 2, 3]];
```

### Q2: What's the difference between Array.of() and Array() constructor?

**Answer:**
```javascript
// Array() with single number creates array of that length
console.log(new Array(3)); // [empty × 3]

// Array.of() creates array with that element
console.log(Array.of(3)); // [3]

// With multiple arguments, both work the same
console.log(new Array(1, 2, 3)); // [1, 2, 3]
console.log(Array.of(1, 2, 3)); // [1, 2, 3]
```

### Q3: How do you check if a variable is an array?

**Answer:**
```javascript
let arr = [1, 2, 3];

// Best method: Array.isArray()
console.log(Array.isArray(arr)); // true ✓

// Other methods:
console.log(arr instanceof Array); // true
console.log(arr.constructor === Array); // true
console.log(Object.prototype.toString.call(arr) === "[object Array]"); // true

// ❌ typeof doesn't work
console.log(typeof arr); // "object" (not useful)
```

### Q4: How do you clone an array?

**Answer:**
```javascript
let original = [1, 2, 3];

// Method 1: Spread operator
let clone1 = [...original];

// Method 2: slice()
let clone2 = original.slice();

// Method 3: Array.from()
let clone3 = Array.from(original);

// Method 4: concat()
let clone4 = [].concat(original);

// Note: All are shallow copies
let nested = [[1, 2], [3, 4]];
let shallowClone = [...nested];
shallowClone[0][0] = 99;
console.log(nested[0][0]); // 99 (affected!)

// Deep clone
let deepClone = JSON.parse(JSON.stringify(nested));
```

### Q5: What happens when you change array length?

**Answer:**
```javascript
let arr = [1, 2, 3, 4, 5];

// Decrease length: truncates array
arr.length = 3;
console.log(arr); // [1, 2, 3]

// Increase length: adds empty slots
arr.length = 5;
console.log(arr); // [1, 2, 3, empty × 2]
console.log(arr[4]); // undefined

// Set to 0: clears array
arr.length = 0;
console.log(arr); // []
```

---

## Practice Exercises

### Exercise 1: Remove Duplicates
Write a function to remove duplicates from an array.

```javascript
function removeDuplicates(arr) {
  // Your code here
}

console.log(removeDuplicates([1, 2, 2, 3, 4, 4, 5])); // [1, 2, 3, 4, 5]
```

<details>
<summary>Solution</summary>

```javascript
// Method 1: Using Set
function removeDuplicates(arr) {
  return [...new Set(arr)];
}

// Method 2: Using filter
function removeDuplicates2(arr) {
  return arr.filter((item, index) => arr.indexOf(item) === index);
}

// Method 3: Using reduce
function removeDuplicates3(arr) {
  return arr.reduce((acc, item) => {
    if (!acc.includes(item)) {
      acc.push(item);
    }
    return acc;
  }, []);
}
```
</details>

### Exercise 2: Flatten Array
Write a function to flatten a nested array.

```javascript
function flatten(arr) {
  // Your code here
}

console.log(flatten([1, [2, [3, [4]], 5]])); // [1, 2, 3, 4, 5]
```

<details>
<summary>Solution</summary>

```javascript
// Method 1: Using flat() (ES2019)
function flatten(arr) {
  return arr.flat(Infinity);
}

// Method 2: Using recursion
function flatten2(arr) {
  return arr.reduce((acc, item) => {
    if (Array.isArray(item)) {
      return acc.concat(flatten2(item));
    }
    return acc.concat(item);
  }, []);
}

// Method 3: Using toString and split (numbers only)
function flatten3(arr) {
  return arr.toString().split(',').map(Number);
}
```
</details>

### Exercise 3: Chunk Array
Write a function to split an array into chunks of specified size.

```javascript
function chunk(arr, size) {
  // Your code here
}

console.log(chunk([1, 2, 3, 4, 5, 6, 7], 3)); // [[1, 2, 3], [4, 5, 6], [7]]
```

<details>
<summary>Solution</summary>

```javascript
function chunk(arr, size) {
  const result = [];
  for (let i = 0; i < arr.length; i += size) {
    result.push(arr.slice(i, i + size));
  }
  return result;
}

// Alternative using reduce
function chunk2(arr, size) {
  return arr.reduce((acc, _, i) => {
    if (i % size === 0) {
      acc.push(arr.slice(i, i + size));
    }
    return acc;
  }, []);
}
```
</details>

---

**[← Back: Dates](../01-basics/06-dates.md)** | **[Next: Array Methods →](./02-array-methods.md)**

---

**Made with ❤️ for JavaScript learners**
