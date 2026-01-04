# 📊 Array Methods Complete Cheatsheet

Quick reference for all JavaScript array methods with examples.

## 📑 Table of Contents
- [Mutating Methods](#mutating-methods-change-original-array)
- [Non-Mutating Methods](#non-mutating-methods-return-new-arrayvalue)
- [Iteration Methods](#iteration-methods)
- [Searching Methods](#searching-methods)
- [Transformation Methods](#transformation-methods)
- [Static Methods](#static-methods)

---

## Mutating Methods (Change Original Array)

### push()
**Add elements to end, returns new length**
```javascript
let arr = [1, 2, 3];
let length = arr.push(4, 5);
console.log(arr);      // [1, 2, 3, 4, 5]
console.log(length);   // 5
```

### pop()
**Remove last element, returns removed element**
```javascript
let arr = [1, 2, 3];
let removed = arr.pop();
console.log(arr);      // [1, 2]
console.log(removed);  // 3
```

### unshift()
**Add elements to start, returns new length**
```javascript
let arr = [3, 4, 5];
let length = arr.unshift(1, 2);
console.log(arr);      // [1, 2, 3, 4, 5]
console.log(length);   // 5
```

### shift()
**Remove first element, returns removed element**
```javascript
let arr = [1, 2, 3];
let removed = arr.shift();
console.log(arr);      // [2, 3]
console.log(removed);  // 1
```

### splice()
**Add/remove elements at any position**
```javascript
let arr = [1, 2, 3, 4, 5];

// Remove 2 elements from index 1
arr.splice(1, 2);
console.log(arr);      // [1, 4, 5]

// Add elements at index 1
arr.splice(1, 0, 2, 3);
console.log(arr);      // [1, 2, 3, 4, 5]

// Replace element at index 2
arr.splice(2, 1, 99);
console.log(arr);      // [1, 2, 99, 4, 5]
```

### reverse()
**Reverse array in place**
```javascript
let arr = [1, 2, 3, 4, 5];
arr.reverse();
console.log(arr);      // [5, 4, 3, 2, 1]
```

### sort()
**Sort array in place**
```javascript
// Alphabetical (default)
let arr1 = ['c', 'a', 'b'];
arr1.sort();
console.log(arr1);     // ['a', 'b', 'c']

// Numeric sorting
let arr2 = [10, 5, 40, 25];
arr2.sort((a, b) => a - b);  // Ascending
console.log(arr2);     // [5, 10, 25, 40]

arr2.sort((a, b) => b - a);  // Descending
console.log(arr2);     // [40, 25, 10, 5]

// Sort objects
let users = [
  { name: "John", age: 30 },
  { name: "Jane", age: 25 },
  { name: "Bob", age: 35 }
];
users.sort((a, b) => a.age - b.age);
console.log(users);    // Sorted by age ascending
```

### fill()
**Fill all/part of array with static value**
```javascript
let arr = [1, 2, 3, 4, 5];

arr.fill(0);
console.log(arr);      // [0, 0, 0, 0, 0]

arr.fill(7, 2, 4);     // Fill from index 2 to 4
console.log(arr);      // [0, 0, 7, 7, 0]

// Create array of zeros
let zeros = new Array(5).fill(0);  // [0, 0, 0, 0, 0]
```

### copyWithin()
**Copy part of array to another location**
```javascript
let arr = [1, 2, 3, 4, 5];

// Copy elements from index 3 to index 0
arr.copyWithin(0, 3);
console.log(arr);      // [4, 5, 3, 4, 5]

// Copy with start and end
arr = [1, 2, 3, 4, 5];
arr.copyWithin(0, 3, 4);  // Copy index 3-4 to index 0
console.log(arr);      // [4, 2, 3, 4, 5]
```

---

## Non-Mutating Methods (Return New Array/Value)

### slice()
**Extract portion of array**
```javascript
let arr = [1, 2, 3, 4, 5];

console.log(arr.slice(2));       // [3, 4, 5]
console.log(arr.slice(1, 4));    // [2, 3, 4]
console.log(arr.slice(-2));      // [4, 5]
console.log(arr.slice(1, -1));   // [2, 3, 4]

// Shallow copy
let copy = arr.slice();
```

### concat()
**Merge arrays**
```javascript
let arr1 = [1, 2];
let arr2 = [3, 4];
let arr3 = [5, 6];

let merged = arr1.concat(arr2, arr3);
console.log(merged);   // [1, 2, 3, 4, 5, 6]

// Alternative with spread
let merged2 = [...arr1, ...arr2, ...arr3];
```

### join()
**Join array elements into string**
```javascript
let arr = ['Hello', 'World', '!'];

console.log(arr.join());         // "Hello,World,!"
console.log(arr.join(' '));      // "Hello World !"
console.log(arr.join('-'));      // "Hello-World-!"
console.log(arr.join(''));       // "HelloWorld!"
```

### toString()
**Convert array to string**
```javascript
let arr = [1, 2, 3];
console.log(arr.toString());     // "1,2,3"
```

### toLocaleString()
**Convert to localized string**
```javascript
let arr = [1000, 2000, 3000];
console.log(arr.toLocaleString('en-US'));  // "1,000,2,000,3,000"

let dates = [new Date()];
console.log(dates.toLocaleString());  // Localized date format
```

---

## Iteration Methods

### forEach()
**Execute function for each element**
```javascript
let arr = [1, 2, 3, 4, 5];

arr.forEach((item, index, array) => {
  console.log(`Index ${index}: ${item}`);
});

// Index 0: 1
// Index 1: 2
// Index 2: 3
// Index 3: 4
// Index 4: 5

// Note: Cannot break out of forEach
// Use for...of for that
```

### map()
**Transform each element, returns new array**
```javascript
let arr = [1, 2, 3, 4, 5];

let doubled = arr.map(x => x * 2);
console.log(doubled);    // [2, 4, 6, 8, 10]

let squared = arr.map(x => x ** 2);
console.log(squared);    // [1, 4, 9, 16, 25]

// With objects
let users = [
  { name: "John", age: 30 },
  { name: "Jane", age: 25 }
];
let names = users.map(user => user.name);
console.log(names);      // ["John", "Jane"]
```

### filter()
**Filter elements based on condition**
```javascript
let arr = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];

let evens = arr.filter(x => x % 2 === 0);
console.log(evens);      // [2, 4, 6, 8, 10]

let greaterThan5 = arr.filter(x => x > 5);
console.log(greaterThan5);  // [6, 7, 8, 9, 10]

// Filter objects
let users = [
  { name: "John", age: 30 },
  { name: "Jane", age: 25 },
  { name: "Bob", age: 35 }
];
let adults = users.filter(user => user.age >= 30);
console.log(adults);     // [{ name: "John", age: 30 }, { name: "Bob", age: 35 }]
```

### reduce()
**Reduce array to single value**
```javascript
let arr = [1, 2, 3, 4, 5];

// Sum
let sum = arr.reduce((acc, curr) => acc + curr, 0);
console.log(sum);        // 15

// Product
let product = arr.reduce((acc, curr) => acc * curr, 1);
console.log(product);    // 120

// Max value
let max = arr.reduce((acc, curr) => Math.max(acc, curr));
console.log(max);        // 5

// Count occurrences
let fruits = ['apple', 'banana', 'apple', 'orange', 'banana', 'apple'];
let count = fruits.reduce((acc, fruit) => {
  acc[fruit] = (acc[fruit] || 0) + 1;
  return acc;
}, {});
console.log(count);      // { apple: 3, banana: 2, orange: 1 }

// Flatten array
let nested = [[1, 2], [3, 4], [5, 6]];
let flattened = nested.reduce((acc, curr) => acc.concat(curr), []);
console.log(flattened);  // [1, 2, 3, 4, 5, 6]
```

### reduceRight()
**Reduce from right to left**
```javascript
let arr = [1, 2, 3, 4, 5];

let result = arr.reduceRight((acc, curr) => acc + curr);
console.log(result);     // 15

// Order matters for non-commutative operations
let strings = ['a', 'b', 'c'];
let left = strings.reduce((acc, curr) => acc + curr);
console.log(left);       // "abc"
let right = strings.reduceRight((acc, curr) => acc + curr);
console.log(right);      // "cba"
```

### some()
**Test if at least one element passes**
```javascript
let arr = [1, 2, 3, 4, 5];

let hasEven = arr.some(x => x % 2 === 0);
console.log(hasEven);    // true

let hasNegative = arr.some(x => x < 0);
console.log(hasNegative); // false

// With objects
let users = [
  { name: "John", age: 17 },
  { name: "Jane", age: 25 }
];
let hasAdult = users.some(user => user.age >= 18);
console.log(hasAdult);   // true
```

### every()
**Test if all elements pass**
```javascript
let arr = [2, 4, 6, 8, 10];

let allEven = arr.every(x => x % 2 === 0);
console.log(allEven);    // true

let allPositive = arr.every(x => x > 0);
console.log(allPositive); // true

// With objects
let users = [
  { name: "John", age: 30 },
  { name: "Jane", age: 25 }
];
let allAdults = users.every(user => user.age >= 18);
console.log(allAdults);  // true
```

### flat()
**Flatten nested arrays**
```javascript
let arr = [1, 2, [3, 4], [5, [6, 7]]];

console.log(arr.flat());           // [1, 2, 3, 4, 5, [6, 7]]
console.log(arr.flat(2));          // [1, 2, 3, 4, 5, 6, 7]
console.log(arr.flat(Infinity));   // [1, 2, 3, 4, 5, 6, 7]

// Remove empty slots
let sparse = [1, , 3, , 5];
console.log(sparse.flat());        // [1, 3, 5]
```

### flatMap()
**Map then flat (depth 1)**
```javascript
let arr = [1, 2, 3];

// Split each number into [number, number * 2]
let result = arr.flatMap(x => [x, x * 2]);
console.log(result);     // [1, 2, 2, 4, 3, 6]

// Equivalent to:
let result2 = arr.map(x => [x, x * 2]).flat();

// Practical example: split sentences into words
let sentences = ["Hello world", "How are you"];
let words = sentences.flatMap(s => s.split(' '));
console.log(words);      // ["Hello", "world", "How", "are", "you"]
```

---

## Searching Methods

### indexOf()
**Find first index of value**
```javascript
let arr = [1, 2, 3, 2, 1];

console.log(arr.indexOf(2));       // 1
console.log(arr.indexOf(5));       // -1 (not found)
console.log(arr.indexOf(2, 2));    // 3 (search from index 2)
```

### lastIndexOf()
**Find last index of value**
```javascript
let arr = [1, 2, 3, 2, 1];

console.log(arr.lastIndexOf(2));   // 3
console.log(arr.lastIndexOf(5));   // -1
```

### includes()
**Check if value exists**
```javascript
let arr = [1, 2, 3, 4, 5];

console.log(arr.includes(3));      // true
console.log(arr.includes(6));      // false
console.log(arr.includes(3, 3));   // false (search from index 3)

// Works with NaN
let arr2 = [1, NaN, 3];
console.log(arr2.includes(NaN));   // true
```

### find()
**Find first element matching condition**
```javascript
let arr = [1, 2, 3, 4, 5];

let found = arr.find(x => x > 3);
console.log(found);      // 4

let notFound = arr.find(x => x > 10);
console.log(notFound);   // undefined

// With objects
let users = [
  { id: 1, name: "John" },
  { id: 2, name: "Jane" }
];
let user = users.find(u => u.id === 2);
console.log(user);       // { id: 2, name: "Jane" }
```

### findIndex()
**Find index of first element matching condition**
```javascript
let arr = [1, 2, 3, 4, 5];

let index = arr.findIndex(x => x > 3);
console.log(index);      // 3

let notFound = arr.findIndex(x => x > 10);
console.log(notFound);   // -1
```

### findLast()
**Find last element matching condition (ES2023)**
```javascript
let arr = [1, 2, 3, 4, 5];

let found = arr.findLast(x => x > 3);
console.log(found);      // 5
```

### findLastIndex()
**Find index of last element matching condition (ES2023)**
```javascript
let arr = [1, 2, 3, 4, 5];

let index = arr.findLastIndex(x => x > 3);
console.log(index);      // 4
```

---

## Static Methods

### Array.isArray()
**Check if value is array**
```javascript
console.log(Array.isArray([1, 2, 3]));    // true
console.log(Array.isArray({}));           // false
console.log(Array.isArray("hello"));      // false
```

### Array.from()
**Create array from iterable**
```javascript
// From string
let arr1 = Array.from("hello");
console.log(arr1);       // ["h", "e", "l", "l", "o"]

// From NodeList
let divs = document.querySelectorAll('div');
let divsArray = Array.from(divs);

// With mapping function
let arr2 = Array.from([1, 2, 3], x => x * 2);
console.log(arr2);       // [2, 4, 6]

// Create array of length n
let arr3 = Array.from({ length: 5 }, (_, i) => i);
console.log(arr3);       // [0, 1, 2, 3, 4]
```

### Array.of()
**Create array from arguments**
```javascript
let arr1 = Array.of(1, 2, 3);
console.log(arr1);       // [1, 2, 3]

let arr2 = Array.of(5);
console.log(arr2);       // [5]

// Compare with Array constructor
let arr3 = Array(5);
console.log(arr3);       // [empty × 5]

let arr4 = Array(5, 2, 3);
console.log(arr4);       // [5, 2, 3]
```

---

## Method Chaining

```javascript
let users = [
  { name: "John", age: 30, active: true },
  { name: "Jane", age: 25, active: false },
  { name: "Bob", age: 35, active: true },
  { name: "Alice", age: 28, active: true }
];

// Chain multiple methods
let result = users
  .filter(user => user.active)         // Only active users
  .map(user => user.name)              // Get names
  .sort()                               // Sort alphabetically
  .join(', ');                          // Join into string

console.log(result);     // "Alice, Bob, John"

// Complex example
let numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];
let result2 = numbers
  .filter(x => x % 2 === 0)            // Even numbers
  .map(x => x ** 2)                     // Square them
  .reduce((sum, x) => sum + x, 0);     // Sum them

console.log(result2);    // 220 (4 + 16 + 36 + 64 + 100)
```

---

## Quick Reference Table

| Method | Mutates | Returns | Use Case |
|--------|---------|---------|----------|
| push() | ✓ | length | Add to end |
| pop() | ✓ | element | Remove from end |
| unshift() | ✓ | length | Add to start |
| shift() | ✓ | element | Remove from start |
| splice() | ✓ | removed elements | Add/remove anywhere |
| reverse() | ✓ | array | Reverse order |
| sort() | ✓ | array | Sort elements |
| fill() | ✓ | array | Fill with value |
| slice() | ❌ | new array | Extract portion |
| concat() | ❌ | new array | Merge arrays |
| join() | ❌ | string | Join into string |
| map() | ❌ | new array | Transform elements |
| filter() | ❌ | new array | Select elements |
| reduce() | ❌ | any | Aggregate to value |
| forEach() | ❌ | undefined | Iterate |
| find() | ❌ | element | Find first match |
| findIndex() | ❌ | number | Find first index |
| some() | ❌ | boolean | Test if any match |
| every() | ❌ | boolean | Test if all match |
| includes() | ❌ | boolean | Check if exists |
| indexOf() | ❌ | number | Find first index of value |
| flat() | ❌ | new array | Flatten nested |
| flatMap() | ❌ | new array | Map then flat |

---

**[← Back to Quick Reference](./README.md)** | **[Back to Main README](../README.md)**

---

**Made with ❤️ for JavaScript learners**
