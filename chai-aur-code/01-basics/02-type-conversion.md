# 🔄 Type Conversion in JavaScript

## 📑 Table of Contents
- [Introduction](#introduction)
- [Implicit Conversion (Coercion)](#implicit-conversion-coercion)
- [Explicit Conversion](#explicit-conversion)
- [Truthy and Falsy Values](#truthy-and-falsy-values)
- [Common Gotchas](#common-gotchas)
- [Common Mistakes](#-common-mistakes)
- [Interview Tips](#-interview-tips)
- [Practice Exercises](#practice-exercises)

---

## Introduction

Type conversion (also called type casting) is the process of converting a value from one data type to another. JavaScript performs conversions in two ways:

1. **Implicit Conversion (Coercion)**: JavaScript automatically converts types
2. **Explicit Conversion**: Programmer manually converts types

---

## Implicit Conversion (Coercion)

JavaScript automatically converts types when needed.

### String Coercion

```javascript
// Number to String with + operator
let result = "The answer is " + 42;
console.log(result);           // "The answer is 42"
console.log(typeof result);    // "string"

// Boolean to String
console.log("Value: " + true); // "Value: true"

// Object to String
console.log("Object: " + {});  // "Object: [object Object]"
console.log("Array: " + [1,2]); // "Array: 1,2"
```

### Number Coercion

```javascript
// String to Number with arithmetic operators (except +)
console.log("10" - 5);         // 5
console.log("10" * 2);         // 20
console.log("10" / 2);         // 5
console.log("10" % 3);         // 1

// Boolean to Number
console.log(true + 1);         // 2
console.log(false + 1);        // 1

// + operator (unary)
console.log(+"42");            // 42
console.log(+true);            // 1
console.log(+false);           // 0
console.log(+"");              // 0
console.log(+"hello");         // NaN
```

### Boolean Coercion

```javascript
// In conditional statements
if ("hello") {
  console.log("Truthy");       // Executes
}

if (0) {
  console.log("Truthy");       // Doesn't execute
}

// With logical operators
console.log(!0);               // true
console.log(!!1);              // true
console.log(!!"");             // false
```

### Comparison Coercion

```javascript
// Loose equality (==) performs coercion
console.log(5 == "5");         // true (string converted to number)
console.log(true == 1);        // true (boolean converted to number)
console.log(false == 0);       // true
console.log(null == undefined); // true (special case)

// Strict equality (===) does NOT perform coercion
console.log(5 === "5");        // false
console.log(true === 1);       // false
console.log(null === undefined); // false
```

---

## Explicit Conversion

### Converting to String

```javascript
// String() function
let num = 42;
let str1 = String(num);
console.log(str1);             // "42"
console.log(typeof str1);      // "string"

// toString() method
let str2 = num.toString();
console.log(str2);             // "42"

// Template literal
let str3 = `${num}`;
console.log(str3);             // "42"

// Concatenation with empty string
let str4 = num + "";
console.log(str4);             // "42"

// Examples
String(true);                  // "true"
String(false);                 // "false"
String(null);                  // "null"
String(undefined);             // "undefined"
String([1, 2, 3]);             // "1,2,3"
String({ a: 1 });              // "[object Object]"
```

### Converting to Number

```javascript
// Number() function
let str = "42";
let num1 = Number(str);
console.log(num1);             // 42
console.log(typeof num1);      // "number"

// parseInt() - converts to integer
let num2 = parseInt("42");
console.log(num2);             // 42
parseInt("42.99");             // 42 (removes decimals)
parseInt("42px");              // 42 (stops at non-numeric)
parseInt("px42");              // NaN (must start with number)
parseInt("1010", 2);           // 10 (binary to decimal)
parseInt("FF", 16);            // 255 (hex to decimal)

// parseFloat() - converts to floating point
let num3 = parseFloat("42.99");
console.log(num3);             // 42.99
parseFloat("42.99.99");        // 42.99 (stops at second dot)

// Unary + operator
let num4 = +"42";
console.log(num4);             // 42

// Examples
Number("42");                  // 42
Number("42.99");               // 42.99
Number("");                    // 0 ⚠️
Number("  ");                  // 0 ⚠️
Number("42px");                // NaN
Number(true);                  // 1
Number(false);                 // 0
Number(null);                  // 0 ⚠️
Number(undefined);             // NaN
Number([]);                    // 0 ⚠️
Number([1]);                   // 1
Number([1, 2]);                // NaN
Number({});                    // NaN
```

### Converting to Boolean

```javascript
// Boolean() function
let bool1 = Boolean(1);
console.log(bool1);            // true

// Double NOT operator
let bool2 = !!1;
console.log(bool2);            // true

// Falsy values (convert to false)
Boolean(false);                // false
Boolean(0);                    // false
Boolean(-0);                   // false
Boolean(0n);                   // false (BigInt zero)
Boolean("");                   // false
Boolean(null);                 // false
Boolean(undefined);            // false
Boolean(NaN);                  // false

// Truthy values (convert to true) - everything else!
Boolean(true);                 // true
Boolean(1);                    // true
Boolean(-1);                   // true
Boolean("0");                  // true ⚠️
Boolean("false");              // true ⚠️
Boolean([]);                   // true ⚠️
Boolean({});                   // true ⚠️
Boolean(function(){});         // true
```

---

## Truthy and Falsy Values

### All 8 Falsy Values

```javascript
// These are the ONLY falsy values in JavaScript
if (false) {}         // ❌ false
if (0) {}             // ❌ false
if (-0) {}            // ❌ false
if (0n) {}            // ❌ false (BigInt zero)
if ("") {}            // ❌ false (empty string)
if (null) {}          // ❌ false
if (undefined) {}     // ❌ false
if (NaN) {}           // ❌ false

// Everything else is truthy!
```

### Truthy Value Examples

```javascript
// These are all truthy
if (true) {}          // ✓ true
if (1) {}             // ✓ true
if (-1) {}            // ✓ true
if ("0") {}           // ✓ true (string "0", not number 0)
if ("false") {}       // ✓ true (string "false", not boolean false)
if ([]) {}            // ✓ true (empty array)
if ({}) {}            // ✓ true (empty object)
if (function(){}) {}  // ✓ true

// Common mistakes
if ("0") {
  console.log("This runs!"); // ✓ Runs (string "0" is truthy)
}

if ([]) {
  console.log("This runs!"); // ✓ Runs (empty array is truthy)
}
```

### Practical Uses

```javascript
// Default values with ||
let username = inputName || "Guest";
// If inputName is falsy, use "Guest"

// Optional parameters
function greet(name) {
  name = name || "Guest";
  return `Hello ${name}`;
}

// Nullish coalescing (??) - only null/undefined
let count = 0;
let result1 = count || 10;    // 10 (0 is falsy)
let result2 = count ?? 10;    // 0 (0 is not null/undefined) ✓ Better!

// Checking if value exists
if (value) {
  // value is truthy
} else {
  // value is falsy
}

// Better: check specific condition
if (value !== null && value !== undefined) {
  // value exists
}
```

---

## Common Gotchas

### Gotcha 1: Empty String vs String "0"

```javascript
console.log(Boolean(""));      // false (empty string is falsy)
console.log(Boolean("0"));     // true (non-empty string is truthy) ⚠️

// In conditions
if ("0") {
  console.log("Runs!");        // ✓ Runs
}

if (Number("0")) {
  console.log("Doesn't run");  // ❌ Doesn't run
}
```

### Gotcha 2: Array and Object Coercion

```javascript
// Empty array to number
console.log(Number([]));       // 0 ⚠️
console.log(Number([1]));      // 1 ⚠️
console.log(Number([1, 2]));   // NaN

// Array to string to number
console.log([] + []);          // "" (empty string) ⚠️
console.log([] + {});          // "[object Object]"
console.log({} + []);          // "[object Object]" or 0 (varies) ⚠️

// Comparison with arrays
console.log([] == false);      // true ⚠️
console.log([] == 0);          // true ⚠️
console.log([] == ![]);        // true ⚠️ (very confusing!)
```

### Gotcha 3: null and undefined Conversion

```javascript
// null to number
console.log(Number(null));     // 0 ⚠️
console.log(+null);            // 0 ⚠️

// undefined to number
console.log(Number(undefined)); // NaN ✓
console.log(+undefined);       // NaN ✓

// Special equality
console.log(null == undefined); // true ⚠️
console.log(null === undefined); // false ✓
```

### Gotcha 4: String + Number

```javascript
// + operator with strings
console.log("5" + 3);          // "53" (string concatenation) ⚠️
console.log(5 + "3");          // "53"
console.log("5" + "3");        // "53"

// Other operators
console.log("5" - 3);          // 2 (numeric subtraction) ✓
console.log("5" * 3);          // 15
console.log("5" / 3);          // 1.6666...

// Order matters!
console.log(1 + 2 + "3");      // "33" (1+2=3, then "3"+"3")
console.log("1" + 2 + 3);      // "123" ("1"+"2"="12", "12"+"3"="123")
```

---

## ⚠️ Common Mistakes

### Mistake 1: Using == Instead of ===

```javascript
// ❌ Wrong: Loose equality
console.log(0 == "");          // true (unexpected!)
console.log(0 == false);       // true (unexpected!)
console.log(null == undefined); // true (unexpected!)

// ✓ Correct: Strict equality
console.log(0 === "");         // false
console.log(0 === false);      // false
console.log(null === undefined); // false
```

### Mistake 2: Forgetting Empty String is Falsy

```javascript
let input = "";

// ❌ Wrong
if (input) {
  console.log("User entered:", input); // Doesn't run!
}

// ✓ Correct
if (input !== undefined && input !== null) {
  console.log("User entered:", input); // Runs!
}
```

### Mistake 3: Assuming Number() Always Works

```javascript
// ❌ Wrong
let num = Number("42px");
console.log(num);              // NaN (not 42!)

// ✓ Correct: Use parseInt/parseFloat for partial numbers
let num2 = parseInt("42px");
console.log(num2);             // 42
```

### Mistake 4: Using + for Number Conversion with Variables

```javascript
let x = "5";
let y = "10";

// ❌ Wrong
console.log(x + y);            // "510" (string concatenation)

// ✓ Correct
console.log(Number(x) + Number(y)); // 15
console.log(+x + +y);          // 15
console.log(parseInt(x) + parseInt(y)); // 15
```

---

## 💼 Interview Tips

### Q1: What's the difference between implicit and explicit type conversion?

**Answer:**
- **Implicit**: JavaScript automatically converts types (coercion)
- **Explicit**: Programmer manually converts using functions like String(), Number(), Boolean()

```javascript
// Implicit
console.log("5" + 1);          // "51" (number to string)

// Explicit
console.log(String(5) + 1);    // "51"
console.log(Number("5") + 1);  // 6
```

### Q2: What are all the falsy values in JavaScript?

**Answer:** There are exactly 8 falsy values:
1. `false`
2. `0`
3. `-0`
4. `0n` (BigInt zero)
5. `""` (empty string)
6. `null`
7. `undefined`
8. `NaN`

Everything else is truthy!

### Q3: Difference between == and ===?

**Answer:**
- `==` (loose equality): Performs type coercion before comparison
- `===` (strict equality): No type coercion, types must match

```javascript
console.log(5 == "5");         // true (string "5" converted to number)
console.log(5 === "5");        // false (different types)
```

Always prefer `===` unless you specifically need type coercion.

### Q4: What's the output of [] + {} and {} + []?

**Answer:**
```javascript
console.log([] + {});          // "[object Object]"
// [] becomes "", {} becomes "[object Object]"

console.log({} + []);          // "[object Object]" or 0 (context-dependent)
// In some contexts, {} is treated as a block, not an object
```

### Q5: Why does Number("") return 0?

**Answer:** This is a design decision in JavaScript. Empty strings, when converted to numbers, become 0. Similarly:
```javascript
Number("");                    // 0
Number(" ");                   // 0
Number(null);                  // 0
Number([]);                    // 0
```

This can cause bugs, so always validate input!

---

## Practice Exercises

### Exercise 1: Predict the Output
```javascript
console.log("5" + 3);
console.log("5" - 3);
console.log(true + true);
console.log(false + 10);
console.log("5" * "2");
console.log("hello" - 1);
```

<details>
<summary>Solution</summary>

```javascript
console.log("5" + 3);          // "53"
console.log("5" - 3);          // 2
console.log(true + true);      // 2
console.log(false + 10);       // 10
console.log("5" * "2");        // 10
console.log("hello" - 1);      // NaN
```
</details>

### Exercise 2: Type Conversion Practice
Convert the following to different types:
```javascript
// Convert "123" to number
// Convert 456 to string
// Convert "" to boolean
// Convert "0" to boolean
```

<details>
<summary>Solution</summary>

```javascript
Number("123");                 // 123
String(456);                   // "456"
Boolean("");                   // false
Boolean("0");                  // true (non-empty string!)
```
</details>

### Exercise 3: Find the Bug
```javascript
function add(a, b) {
  return a + b;
}

console.log(add(5, "10"));     // Expected: 15, Got: "510"
```

<details>
<summary>Solution</summary>

```javascript
// Bug: "10" is a string, so + concatenates instead of adding

// Fix 1: Convert explicitly
function add(a, b) {
  return Number(a) + Number(b);
}

// Fix 2: Use unary +
function add(a, b) {
  return +a + +b;
}

console.log(add(5, "10"));     // 15
```
</details>

---

**[← Previous: Variables & Data Types](./01-variables-and-datatypes.md)** | **[Next: Operators →](./03-operators.md)**

---

**Made with ❤️ for JavaScript learners**
