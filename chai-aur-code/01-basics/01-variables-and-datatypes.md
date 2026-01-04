# 📦 Variables & Data Types

## 📑 Table of Contents
- [Variables in JavaScript](#variables-in-javascript)
- [Data Types](#data-types)
- [Primitive Types](#primitive-types)
- [Reference Types](#reference-types)
- [Type Checking](#type-checking)
- [Common Mistakes](#-common-mistakes)
- [Interview Tips](#-interview-tips)
- [Practice Exercises](#practice-exercises)

---

## Variables in JavaScript

Variables are containers for storing data values. JavaScript provides three ways to declare variables:

### var (Old way - avoid in modern code)

```javascript
var name = "John";
var name = "Jane"; // Can be redeclared ✓
name = "Bob";      // Can be reassigned ✓

// Function scoped
function example() {
  var x = 10;
  if (true) {
    var x = 20;  // Same variable!
    console.log(x); // 20
  }
  console.log(x); // 20 (not 10!)
}

// Hoisted with value undefined
console.log(age); // undefined (not error)
var age = 25;
```

### let (Modern way - use for variables that change)

```javascript
let name = "John";
// let name = "Jane"; // ❌ Cannot be redeclared
name = "Jane";       // ✓ Can be reassigned

// Block scoped
function example() {
  let x = 10;
  if (true) {
    let x = 20;  // Different variable!
    console.log(x); // 20
  }
  console.log(x); // 10
}

// Hoisted but in Temporal Dead Zone
// console.log(age); // ❌ ReferenceError
let age = 25;
```

### const (Modern way - use for constants)

```javascript
const name = "John";
// const name = "Jane"; // ❌ Cannot be redeclared
// name = "Jane";       // ❌ Cannot be reassigned

// Block scoped (like let)
if (true) {
  const x = 10;
  console.log(x); // 10
}
// console.log(x); // ❌ ReferenceError

// Objects and arrays can be modified
const person = { name: "John" };
person.name = "Jane";  // ✓ OK - modifying property
person.age = 30;       // ✓ OK - adding property
// person = {};        // ❌ Cannot reassign

const arr = [1, 2, 3];
arr.push(4);          // ✓ OK - modifying array
// arr = [];          // ❌ Cannot reassign
```

### Comparison Table

| Feature | var | let | const |
|---------|-----|-----|-------|
| Scope | Function | Block | Block |
| Redeclaration | ✓ Yes | ❌ No | ❌ No |
| Reassignment | ✓ Yes | ✓ Yes | ❌ No |
| Hoisting | Yes (initialized undefined) | Yes (TDZ) | Yes (TDZ) |
| When to use | Never | Changing values | Constants & objects |

---

## Data Types

JavaScript has **7 primitive types** and **3 reference types**.

### Primitive Types

Primitive types store a single value and are immutable (cannot be changed).

#### 1. String

```javascript
let str1 = "Hello";          // Double quotes
let str2 = 'World';          // Single quotes  
let str3 = `Hello ${str2}`;  // Template literal (ES6)

console.log(str3);           // "Hello World"

// Strings are immutable
let name = "John";
name[0] = "B";              // Won't work
console.log(name);          // Still "John"
```

#### 2. Number

```javascript
let integer = 42;
let decimal = 3.14;
let negative = -10;
let exponential = 2.5e6;    // 2500000
let binary = 0b1010;        // 10
let octal = 0o744;          // 484
let hex = 0xFF;             // 255

// Special numeric values
let infinity = Infinity;
let negInfinity = -Infinity;
let notANumber = NaN;       // "Not a Number"

console.log(1 / 0);         // Infinity
console.log("abc" / 2);     // NaN

// Safe integer range
Number.MAX_SAFE_INTEGER;    // 9007199254740991
Number.MIN_SAFE_INTEGER;    // -9007199254740991
```

#### 3. BigInt

```javascript
// For integers larger than 2^53 - 1
let bigNum = 1234567890123456789012345678901234567890n;
let bigNum2 = BigInt("9007199254740992");

console.log(bigNum);        // 1234567890123456789012345678901234567890n

// Operations
let sum = 10n + 20n;        // 30n
// let invalid = 10n + 20; // ❌ Cannot mix BigInt and Number
```

#### 4. Boolean

```javascript
let isActive = true;
let isDeleted = false;

// Boolean from comparison
let isGreater = 10 > 5;     // true
let isEqual = 5 === 5;      // true

// Falsy values (everything else is truthy)
Boolean(false);             // false
Boolean(0);                 // false
Boolean("");                // false
Boolean(null);              // false
Boolean(undefined);         // false
Boolean(NaN);               // false
```

#### 5. Undefined

```javascript
let x;                      // Declared but not assigned
console.log(x);             // undefined

let obj = { name: "John" };
console.log(obj.age);       // undefined (property doesn't exist)

function test() {}
console.log(test());        // undefined (no return value)
```

#### 6. Null

```javascript
let empty = null;           // Intentional absence of value

console.log(empty);         // null

// null vs undefined
let x;                      // undefined (unintentional)
let y = null;               // null (intentional)
```

#### 7. Symbol (ES6)

```javascript
// Unique identifier
let id1 = Symbol("id");
let id2 = Symbol("id");

console.log(id1 === id2);   // false (always unique)

// Use case: Unique object keys
let user = {
  name: "John",
  [id1]: 123
};

console.log(user[id1]);     // 123
```

---

### Reference Types

Reference types store references to memory locations.

#### 1. Object

```javascript
let person = {
  name: "John",
  age: 30,
  city: "New York"
};

console.log(person.name);   // "John"
console.log(person["age"]); // 30

// Objects are mutable
person.age = 31;
person.country = "USA";     // Add new property
```

#### 2. Array

```javascript
let numbers = [1, 2, 3, 4, 5];
let mixed = [1, "hello", true, null, { a: 1 }];

console.log(numbers[0]);    // 1
console.log(numbers.length); // 5

// Arrays are mutable
numbers.push(6);            // Add element
numbers[0] = 10;            // Modify element
```

#### 3. Function

```javascript
function greet(name) {
  return `Hello ${name}`;
}

let sayHi = function(name) {
  return `Hi ${name}`;
};

let greeting = (name) => `Hey ${name}`;

console.log(greet("John"));  // "Hello John"
```

---

## Type Checking

### typeof Operator

```javascript
// Primitives
console.log(typeof "hello");      // "string"
console.log(typeof 42);           // "number"
console.log(typeof 42n);          // "bigint"
console.log(typeof true);         // "boolean"
console.log(typeof undefined);    // "undefined"
console.log(typeof Symbol("id")); // "symbol"

// Special case
console.log(typeof null);         // "object" ❌ (JavaScript bug!)

// Reference types
console.log(typeof {});           // "object"
console.log(typeof []);           // "object" (arrays are objects)
console.log(typeof function(){}); // "function"
```

### Better Type Checking Methods

```javascript
// Check for null
let x = null;
console.log(x === null);          // true ✓

// Check for array
let arr = [1, 2, 3];
console.log(Array.isArray(arr));  // true ✓

// Check for NaN
let num = NaN;
console.log(Number.isNaN(num));   // true ✓
console.log(isNaN("hello"));      // true (converts to number first)
console.log(Number.isNaN("hello")); // false (doesn't convert)

// Check object type
let date = new Date();
console.log(date instanceof Date); // true ✓

// Universal method
Object.prototype.toString.call([]);        // "[object Array]"
Object.prototype.toString.call({});        // "[object Object]"
Object.prototype.toString.call(null);      // "[object Null]"
Object.prototype.toString.call(undefined); // "[object Undefined]"
```

---

## ⚠️ Common Mistakes

### 1. Confusing var, let, and const

```javascript
// ❌ Wrong: Using var
var x = 10;
if (true) {
  var x = 20;
}
console.log(x); // 20 (unexpected!)

// ✓ Correct: Using let
let y = 10;
if (true) {
  let y = 20;
}
console.log(y); // 10 (expected)
```

### 2. Not understanding typeof null

```javascript
// ❌ Wrong
if (typeof value === "object") {
  // This includes null!
}

// ✓ Correct
if (typeof value === "object" && value !== null) {
  // Now null is excluded
}
```

### 3. Modifying const objects

```javascript
// ❌ Wrong understanding
const obj = { a: 1 };
// obj = { b: 2 }; // Error ✓ Good!

// ✓ But this works (common confusion)
obj.a = 2;  // OK - modifying property, not variable
console.log(obj); // { a: 2 }
```

### 4. Checking for NaN

```javascript
let num = NaN;

// ❌ Wrong
console.log(num === NaN); // false (NaN !== NaN)

// ✓ Correct
console.log(Number.isNaN(num)); // true
```

---

## 💼 Interview Tips

### Q1: What's the difference between var, let, and const?

**Answer:**
- **var**: Function-scoped, can be redeclared and reassigned, hoisted with undefined
- **let**: Block-scoped, cannot be redeclared, can be reassigned, hoisted but in TDZ
- **const**: Block-scoped, cannot be redeclared or reassigned, hoisted but in TDZ

### Q2: How many data types are there in JavaScript?

**Answer:** 
8 data types total:
- **7 Primitive**: String, Number, BigInt, Boolean, Undefined, Null, Symbol
- **1 Reference**: Object (which includes Array, Function, Date, etc.)

### Q3: What's the difference between null and undefined?

**Answer:**
- **undefined**: Variable declared but not assigned, or property doesn't exist
- **null**: Intentional absence of value, assigned by programmer

```javascript
let x;          // undefined (JavaScript's default)
let y = null;   // null (programmer's intention)
```

### Q4: Why does typeof null return "object"?

**Answer:** 
This is a bug in JavaScript that has been kept for backward compatibility. In the first implementation of JavaScript, values were stored in 32-bit units with type tags. The type tag for objects was 0, and null was represented as all zeros, so typeof null returned "object".

### Q5: What are primitive types and reference types?

**Answer:**
- **Primitive**: Store actual value, immutable, compared by value
- **Reference**: Store reference to memory location, mutable, compared by reference

```javascript
// Primitives - compared by value
let a = 10;
let b = 10;
console.log(a === b); // true

// Reference - compared by reference
let obj1 = { x: 10 };
let obj2 = { x: 10 };
console.log(obj1 === obj2); // false (different references)
```

---

## Practice Exercises

### Exercise 1: Variable Declarations
Create variables using let and const appropriately:
```javascript
// Declare your name as a constant
// Declare your age as a variable
// Declare an empty array for hobbies
// Try to reassign the name (what happens?)
```

<details>
<summary>Solution</summary>

```javascript
const name = "John";
let age = 25;
const hobbies = [];

// name = "Jane"; // ❌ Error: Assignment to constant variable

age = 26; // ✓ OK
hobbies.push("reading"); // ✓ OK - modifying array contents
```
</details>

### Exercise 2: Type Checking
Write code to check the type of various values:
```javascript
// Check types of: 42, "hello", true, null, undefined, [], {}
// Use appropriate methods for accurate checking
```

<details>
<summary>Solution</summary>

```javascript
console.log(typeof 42);                    // "number"
console.log(typeof "hello");               // "string"
console.log(typeof true);                  // "boolean"
console.log(null === null);                // true
console.log(typeof undefined);             // "undefined"
console.log(Array.isArray([]));            // true
console.log(typeof {} === "object");       // true
```
</details>

### Exercise 3: Primitive vs Reference
What will be logged? Explain why:
```javascript
let x = 10;
let y = x;
y = 20;
console.log(x);

let obj1 = { value: 10 };
let obj2 = obj1;
obj2.value = 20;
console.log(obj1.value);
```

<details>
<summary>Solution</summary>

```javascript
console.log(x);           // 10 (primitives are copied by value)
console.log(obj1.value);  // 20 (objects are copied by reference)

// Explanation:
// x and y store separate values
// obj1 and obj2 point to the same object in memory
```
</details>

---

**[← Back to Chai aur Code](../README.md)** | **[Next: Type Conversion →](./02-type-conversion.md)**

---

**Made with ❤️ for JavaScript learners**
