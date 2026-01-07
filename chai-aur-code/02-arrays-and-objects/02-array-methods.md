# 🛠️ Array Methods in JavaScript

## 📑 Table of Contents
- [Mutating Methods](#mutating-methods)
- [Non-Mutating Methods](#non-mutating-methods)
- [Iteration Methods](#iteration-methods)
- [Search Methods](#search-methods)
- [Transformation Methods](#transformation-methods)
- [Method Chaining](#method-chaining)
- [Common Mistakes](#-common-mistakes)
- [Interview Tips](#-interview-tips)
- [Practice Exercises](#practice-exercises)

---

## Mutating Methods

These methods modify the original array.

### push() - Add to End

```javascript
let arr = [1, 2, 3];
let newLength = arr.push(4);
console.log(arr);        // [1, 2, 3, 4]
console.log(newLength);  // 4

// Add multiple elements
arr.push(5, 6, 7);
console.log(arr);        // [1, 2, 3, 4, 5, 6, 7]
```

### pop() - Remove from End

```javascript
let arr = [1, 2, 3, 4];
let removed = arr.pop();
console.log(removed);    // 4
console.log(arr);        // [1, 2, 3]
```

### unshift() - Add to Beginning

```javascript
let arr = [3, 4, 5];
let newLength = arr.unshift(1, 2);
console.log(arr);        // [1, 2, 3, 4, 5]
console.log(newLength);  // 5
```

### shift() - Remove from Beginning

```javascript
let arr = [1, 2, 3, 4];
let removed = arr.shift();
console.log(removed);    // 1
console.log(arr);        // [2, 3, 4]
```

### splice() - Add/Remove at Any Position

```javascript
let arr = [1, 2, 3, 4, 5];

// Remove elements
let removed = arr.splice(2, 2);  // Start at index 2, remove 2 elements
console.log(removed);            // [3, 4]
console.log(arr);                // [1, 2, 5]

// Insert elements
arr = [1, 2, 5];
arr.splice(2, 0, 3, 4);         // Start at index 2, remove 0, insert 3, 4
console.log(arr);                // [1, 2, 3, 4, 5]

// Replace elements
arr = [1, 2, 3, 4, 5];
arr.splice(1, 2, 'a', 'b', 'c'); // Remove 2 elements, insert 3
console.log(arr);                // [1, 'a', 'b', 'c', 4, 5]
```

### reverse() - Reverse Array

```javascript
let arr = [1, 2, 3, 4, 5];
arr.reverse();
console.log(arr);        // [5, 4, 3, 2, 1]
```

### sort() - Sort Array

```javascript
let arr = [3, 1, 4, 1, 5, 9];
arr.sort();
console.log(arr);        // [1, 1, 3, 4, 5, 9]

// String sorting (default)
let words = ['banana', 'apple', 'cherry'];
words.sort();
console.log(words);      // ['apple', 'banana', 'cherry']

// Number sorting (need compare function)
let nums = [10, 5, 40, 25, 1000];
nums.sort((a, b) => a - b);  // Ascending
console.log(nums);           // [5, 10, 25, 40, 1000]

nums.sort((a, b) => b - a);  // Descending
console.log(nums);           // [1000, 40, 25, 10, 5]

// Sort objects
let users = [
  {name: 'John', age: 30},
  {name: 'Jane', age: 25},
  {name: 'Bob', age: 35}
];
users.sort((a, b) => a.age - b.age);
console.log(users);  // Sorted by age
```

### fill() - Fill with Value

```javascript
let arr = [1, 2, 3, 4, 5];
arr.fill(0);
console.log(arr);        // [0, 0, 0, 0, 0]

// Fill with range
arr = [1, 2, 3, 4, 5];
arr.fill(0, 2, 4);      // Fill from index 2 to 4 (not inclusive)
console.log(arr);        // [1, 2, 0, 0, 5]

// Create and fill
let zeros = new Array(5).fill(0);
console.log(zeros);      // [0, 0, 0, 0, 0]
```

### copyWithin() - Copy Part of Array

```javascript
let arr = [1, 2, 3, 4, 5];
arr.copyWithin(0, 3);    // Copy from index 3 to index 0
console.log(arr);        // [4, 5, 3, 4, 5]

arr = [1, 2, 3, 4, 5];
arr.copyWithin(0, 3, 4); // Copy from index 3-4 to index 0
console.log(arr);        // [4, 2, 3, 4, 5]
```

---

## Non-Mutating Methods

These methods return new arrays without modifying the original.

### concat() - Merge Arrays

```javascript
let arr1 = [1, 2];
let arr2 = [3, 4];
let arr3 = [5, 6];

let merged = arr1.concat(arr2, arr3);
console.log(merged);     // [1, 2, 3, 4, 5, 6]
console.log(arr1);       // [1, 2] (unchanged)

// With spread (alternative)
let merged2 = [...arr1, ...arr2, ...arr3];
console.log(merged2);    // [1, 2, 3, 4, 5, 6]
```

### slice() - Extract Portion

```javascript
let arr = [1, 2, 3, 4, 5];

let sliced = arr.slice(1, 4);  // From index 1 to 4 (not inclusive)
console.log(sliced);           // [2, 3, 4]

let fromIndex = arr.slice(2);  // From index 2 to end
console.log(fromIndex);        // [3, 4, 5]

let lastTwo = arr.slice(-2);   // Last 2 elements
console.log(lastTwo);          // [4, 5]

// Shallow copy
let copy = arr.slice();
console.log(copy);             // [1, 2, 3, 4, 5]
```

### flat() - Flatten Nested Arrays

```javascript
let nested = [1, [2, 3], [4, [5, 6]]];

let flat1 = nested.flat();     // Flatten 1 level (default)
console.log(flat1);            // [1, 2, 3, 4, [5, 6]]

let flat2 = nested.flat(2);    // Flatten 2 levels
console.log(flat2);            // [1, 2, 3, 4, 5, 6]

let flatAll = nested.flat(Infinity);  // Flatten all levels
console.log(flatAll);          // [1, 2, 3, 4, 5, 6]
```

### flatMap() - Map then Flatten

```javascript
let arr = [1, 2, 3];

let result = arr.flatMap(x => [x, x * 2]);
console.log(result);           // [1, 2, 2, 4, 3, 6]

// Equivalent to
let result2 = arr.map(x => [x, x * 2]).flat();
console.log(result2);          // [1, 2, 2, 4, 3, 6]
```

### join() - Array to String

```javascript
let arr = ['Hello', 'World', '!'];

let str1 = arr.join();         // Default separator: comma
console.log(str1);             // "Hello,World,!"

let str2 = arr.join(' ');      // Space separator
console.log(str2);             // "Hello World !"

let str3 = arr.join('');       // No separator
console.log(str3);             // "HelloWorld!"
```

### toString() / toLocaleString()

```javascript
let arr = [1, 2, 3];
console.log(arr.toString());   // "1,2,3"

let dates = [new Date('2024-01-01'), new Date('2024-12-31')];
console.log(dates.toString());
console.log(dates.toLocaleString('en-US'));
```

---

## Iteration Methods

### forEach() - Execute Function on Each Element

```javascript
let arr = [1, 2, 3, 4, 5];

arr.forEach((element, index, array) => {
  console.log(`arr[${index}] = ${element}`);
});
// arr[0] = 1
// arr[1] = 2
// ...

// Practical example: sum
let sum = 0;
arr.forEach(num => sum += num);
console.log(sum);              // 15

// Note: Cannot break/continue, use for...of if needed
```

### map() - Transform Each Element

```javascript
let numbers = [1, 2, 3, 4, 5];

let doubled = numbers.map(x => x * 2);
console.log(doubled);          // [2, 4, 6, 8, 10]

let squared = numbers.map(x => x ** 2);
console.log(squared);          // [1, 4, 9, 16, 25]

// With objects
let users = [{name: 'John', age: 30}, {name: 'Jane', age: 25}];
let names = users.map(user => user.name);
console.log(names);            // ['John', 'Jane']
```

### filter() - Filter Elements

```javascript
let numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];

let evens = numbers.filter(x => x % 2 === 0);
console.log(evens);            // [2, 4, 6, 8, 10]

let greaterThan5 = numbers.filter(x => x > 5);
console.log(greaterThan5);     // [6, 7, 8, 9, 10]

// Filter objects
let users = [
  {name: 'John', age: 30},
  {name: 'Jane', age: 25},
  {name: 'Bob', age: 35}
];
let adults = users.filter(user => user.age >= 30);
console.log(adults);           // [{name: 'John', age: 30}, {name: 'Bob', age: 35}]
```

### reduce() - Reduce to Single Value

```javascript
let numbers = [1, 2, 3, 4, 5];

// Sum
let sum = numbers.reduce((acc, curr) => acc + curr, 0);
console.log(sum);              // 15

// Product
let product = numbers.reduce((acc, curr) => acc * curr, 1);
console.log(product);          // 120

// Max value
let max = numbers.reduce((acc, curr) => Math.max(acc, curr));
console.log(max);              // 5

// Count occurrences
let fruits = ['apple', 'banana', 'apple', 'orange', 'banana', 'apple'];
let count = fruits.reduce((acc, fruit) => {
  acc[fruit] = (acc[fruit] || 0) + 1;
  return acc;
}, {});
console.log(count);            // {apple: 3, banana: 2, orange: 1}

// Flatten array
let nested = [[1, 2], [3, 4], [5, 6]];
let flattened = nested.reduce((acc, curr) => acc.concat(curr), []);
console.log(flattened);        // [1, 2, 3, 4, 5, 6]
```

### reduceRight() - Reduce from Right

```javascript
let arr = ['a', 'b', 'c', 'd'];
let result = arr.reduceRight((acc, curr) => acc + curr);
console.log(result);           // "dcba"
```

---

## Search Methods

### find() - Find First Match

```javascript
let numbers = [1, 5, 10, 15, 20];

let found = numbers.find(x => x > 10);
console.log(found);            // 15 (first element > 10)

// Returns undefined if not found
let notFound = numbers.find(x => x > 100);
console.log(notFound);         // undefined

// With objects
let users = [{id: 1, name: 'John'}, {id: 2, name: 'Jane'}];
let user = users.find(u => u.id === 2);
console.log(user);             // {id: 2, name: 'Jane'}
```

### findIndex() - Find First Match Index

```javascript
let numbers = [1, 5, 10, 15, 20];

let index = numbers.findIndex(x => x > 10);
console.log(index);            // 3

// Returns -1 if not found
let notFound = numbers.findIndex(x => x > 100);
console.log(notFound);         // -1
```

### findLast() / findLastIndex() - ES2023

```javascript
let numbers = [1, 5, 10, 15, 20];

let last = numbers.findLast(x => x > 10);
console.log(last);             // 20 (last element > 10)

let lastIndex = numbers.findLastIndex(x => x > 10);
console.log(lastIndex);        // 4
```

### indexOf() - Find Index of Element

```javascript
let arr = ['apple', 'banana', 'orange', 'banana'];

console.log(arr.indexOf('banana'));        // 1 (first occurrence)
console.log(arr.indexOf('grape'));         // -1 (not found)
console.log(arr.indexOf('banana', 2));     // 3 (search from index 2)
```

### lastIndexOf() - Find Last Index

```javascript
let arr = ['apple', 'banana', 'orange', 'banana'];

console.log(arr.lastIndexOf('banana'));    // 3 (last occurrence)
```

### includes() - Check if Contains

```javascript
let arr = [1, 2, 3, 4, 5];

console.log(arr.includes(3));              // true
console.log(arr.includes(10));             // false
console.log(arr.includes(3, 3));           // false (search from index 3)

// Works with NaN
let arrWithNaN = [1, 2, NaN, 4];
console.log(arrWithNaN.includes(NaN));     // true
console.log(arrWithNaN.indexOf(NaN));      // -1 (indexOf can't find NaN)
```

### some() - Check if Any Match

```javascript
let numbers = [1, 2, 3, 4, 5];

let hasEven = numbers.some(x => x % 2 === 0);
console.log(hasEven);          // true

let hasNegative = numbers.some(x => x < 0);
console.log(hasNegative);      // false
```

### every() - Check if All Match

```javascript
let numbers = [2, 4, 6, 8, 10];

let allEven = numbers.every(x => x % 2 === 0);
console.log(allEven);          // true

let allPositive = numbers.every(x => x > 0);
console.log(allPositive);      // true

let allGreaterThan5 = numbers.every(x => x > 5);
console.log(allGreaterThan5);  // false
```

---

## Transformation Methods

### Array.from()

```javascript
// String to array
let str = "Hello";
let chars = Array.from(str);
console.log(chars);            // ['H', 'e', 'l', 'l', 'o']

// With mapping
let numbers = Array.from([1, 2, 3], x => x * 2);
console.log(numbers);          // [2, 4, 6]

// Create range
let range = Array.from({length: 5}, (_, i) => i + 1);
console.log(range);            // [1, 2, 3, 4, 5]
```

### Array.of()

```javascript
let arr = Array.of(1, 2, 3);
console.log(arr);              // [1, 2, 3]
```

### Spread Operator

```javascript
let arr1 = [1, 2, 3];
let arr2 = [...arr1, 4, 5];
console.log(arr2);             // [1, 2, 3, 4, 5]
```

---

## Method Chaining

Combine multiple array methods for powerful transformations.

```javascript
let numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];

// Get sum of doubled even numbers
let result = numbers
  .filter(x => x % 2 === 0)    // [2, 4, 6, 8, 10]
  .map(x => x * 2)             // [4, 8, 12, 16, 20]
  .reduce((sum, x) => sum + x, 0);  // 60
console.log(result);           // 60

// Complex example: process user data
let users = [
  {name: 'John', age: 30, active: true},
  {name: 'Jane', age: 25, active: false},
  {name: 'Bob', age: 35, active: true},
  {name: 'Alice', age: 28, active: true}
];

let activeUserNames = users
  .filter(user => user.active)
  .map(user => user.name)
  .sort();
console.log(activeUserNames);  // ['Alice', 'Bob', 'John']

// Average age of active users
let avgAge = users
  .filter(user => user.active)
  .map(user => user.age)
  .reduce((sum, age, _, arr) => sum + age / arr.length, 0);
console.log(avgAge);           // 31
```

---

## ⚠️ Common Mistakes

### 1. forEach Cannot Break

```javascript
let arr = [1, 2, 3, 4, 5];

// ❌ Cannot break
arr.forEach(x => {
  if (x === 3) break;  // SyntaxError
});

// ✓ Use for...of instead
for (let x of arr) {
  if (x === 3) break;
  console.log(x);
}
```

### 2. map() vs forEach()

```javascript
let numbers = [1, 2, 3];

// ❌ Using forEach to transform (wrong tool)
let doubled = [];
numbers.forEach(x => doubled.push(x * 2));

// ✓ Use map for transformations
let doubled2 = numbers.map(x => x * 2);
```

### 3. sort() Default Behavior

```javascript
let numbers = [10, 5, 40, 25, 1000];

// ❌ Wrong: sorts as strings
numbers.sort();
console.log(numbers);  // [10, 1000, 25, 40, 5]

// ✓ Correct: use compare function
numbers.sort((a, b) => a - b);
console.log(numbers);  // [5, 10, 25, 40, 1000]
```

---

## 💼 Interview Tips

### Q1: What's the difference between map() and forEach()?

**Answer:**
- `map()` returns a new array with transformed elements
- `forEach()` executes a function on each element but returns undefined
- Use `map()` for transformations, `forEach()` for side effects

```javascript
let arr = [1, 2, 3];

let doubled = arr.map(x => x * 2);
console.log(doubled);  // [2, 4, 6]

arr.forEach(x => console.log(x * 2));  // Just logs, returns undefined
```

### Q2: When to use reduce()?

**Answer:**
Use `reduce()` when you need to transform an array into a single value or different structure:
- Sum, product, average
- Find min/max
- Count occurrences
- Flatten arrays
- Group objects

### Q3: What's the difference between slice() and splice()?

**Answer:**
- `slice()`: Non-mutating, extracts portion, returns new array
- `splice()`: Mutating, adds/removes elements, modifies original

```javascript
let arr = [1, 2, 3, 4, 5];
arr.slice(1, 3);   // [2, 3], original unchanged
arr.splice(1, 2);  // [2, 3], original is [1, 4, 5]
```

---

## Practice Exercises

### Exercise 1: Find Average
Calculate average of numbers in array.

```javascript
function average(arr) {
  // Your code here
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

### Exercise 2: Group By Property
Group array of objects by a property.

```javascript
function groupBy(arr, key) {
  // Your code here
}

let users = [
  {name: 'John', role: 'admin'},
  {name: 'Jane', role: 'user'},
  {name: 'Bob', role: 'admin'}
];
console.log(groupBy(users, 'role'));
// {admin: [{...}, {...}], user: [{...}]}
```

<details>
<summary>Solution</summary>

```javascript
function groupBy(arr, key) {
  return arr.reduce((acc, obj) => {
    const keyValue = obj[key];
    if (!acc[keyValue]) {
      acc[keyValue] = [];
    }
    acc[keyValue].push(obj);
    return acc;
  }, {});
}
```
</details>

---

**[← Back: Arrays](./01-arrays.md)** | **[Next: Objects →](./03-objects.md)**

---

**Made with ❤️ for JavaScript learners**
