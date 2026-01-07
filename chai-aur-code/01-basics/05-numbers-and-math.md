# 🔢 Numbers and Math in JavaScript

## 📑 Table of Contents
- [Number Basics](#number-basics)
- [Number Methods](#number-methods)
- [Number Properties](#number-properties)
- [Math Object](#math-object)
- [Random Numbers](#random-numbers)
- [Number Formatting](#number-formatting)
- [Precision and Rounding](#precision-and-rounding)
- [Common Mistakes](#-common-mistakes)
- [Interview Tips](#-interview-tips)
- [Practice Exercises](#practice-exercises)

---

## Number Basics

JavaScript has only one number type - all numbers are 64-bit floating-point numbers (IEEE 754 standard).

```javascript
// Integer
let int = 42;
console.log(int);              // 42

// Floating-point
let float = 3.14159;
console.log(float);            // 3.14159

// Negative numbers
let negative = -10;
console.log(negative);         // -10

// Scientific notation
let scientific = 2.5e6;
console.log(scientific);       // 2500000

let small = 1.5e-3;
console.log(small);            // 0.0015

// Different number bases
let binary = 0b1010;           // Binary (base 2)
console.log(binary);           // 10

let octal = 0o744;             // Octal (base 8)
console.log(octal);            // 484

let hex = 0xFF;                // Hexadecimal (base 16)
console.log(hex);              // 255
```

### Special Numeric Values

```javascript
// Infinity
console.log(1 / 0);            // Infinity
console.log(-1 / 0);           // -Infinity
console.log(Infinity + 1);     // Infinity
console.log(Infinity * 2);     // Infinity

// NaN (Not a Number)
console.log(0 / 0);            // NaN
console.log("abc" / 2);        // NaN
console.log(Math.sqrt(-1));    // NaN
console.log(NaN + 5);          // NaN (any operation with NaN = NaN)

// NaN is not equal to itself!
console.log(NaN === NaN);      // false
console.log(NaN == NaN);       // false
```

---

## Number Methods

### Converting to Number

```javascript
// Number() constructor
console.log(Number("123"));              // 123
console.log(Number("12.34"));            // 12.34
console.log(Number(""));                 // 0
console.log(Number(" "));                // 0
console.log(Number("abc"));              // NaN
console.log(Number(true));               // 1
console.log(Number(false));              // 0
console.log(Number(null));               // 0
console.log(Number(undefined));          // NaN

// parseInt() - string to integer
console.log(parseInt("123"));            // 123
console.log(parseInt("123.45"));         // 123 (truncates decimal)
console.log(parseInt("123abc"));         // 123 (stops at first non-digit)
console.log(parseInt("abc123"));         // NaN (must start with number)
console.log(parseInt("10", 2));          // 2 (binary)
console.log(parseInt("FF", 16));         // 255 (hexadecimal)

// parseFloat() - string to float
console.log(parseFloat("123.45"));       // 123.45
console.log(parseFloat("123.45.67"));    // 123.45 (stops at second dot)
console.log(parseFloat("3.14abc"));      // 3.14

// Unary plus operator (fastest)
console.log(+"123");                     // 123
console.log(+"12.34");                   // 12.34
console.log(+"abc");                     // NaN
```

### Checking Numbers

```javascript
let num = 42;

// isNaN() - global function (converts to number first)
console.log(isNaN(NaN));                 // true
console.log(isNaN("abc"));               // true (converts "abc" to NaN)
console.log(isNaN("123"));               // false (converts "123" to 123)

// Number.isNaN() - doesn't convert (more reliable)
console.log(Number.isNaN(NaN));          // true
console.log(Number.isNaN("abc"));        // false (doesn't convert)
console.log(Number.isNaN(123));          // false

// isFinite() - checks if finite number
console.log(isFinite(42));               // true
console.log(isFinite(Infinity));         // false
console.log(isFinite(NaN));              // false
console.log(isFinite("42"));             // true (converts string)

// Number.isFinite() - doesn't convert
console.log(Number.isFinite(42));        // true
console.log(Number.isFinite("42"));      // false (doesn't convert)

// Number.isInteger() - checks if integer
console.log(Number.isInteger(42));       // true
console.log(Number.isInteger(42.0));     // true
console.log(Number.isInteger(42.5));     // false
console.log(Number.isInteger("42"));     // false

// Number.isSafeInteger() - checks if within safe range
console.log(Number.isSafeInteger(42));                    // true
console.log(Number.isSafeInteger(9007199254740991));      // true (MAX_SAFE_INTEGER)
console.log(Number.isSafeInteger(9007199254740992));      // false
```

### Formatting Numbers

```javascript
let num = 123.456789;

// toFixed() - fixed decimal places (returns string)
console.log(num.toFixed(2));             // "123.46" (rounds)
console.log(num.toFixed(0));             // "123"
console.log((1.23e-5).toFixed(7));       // "0.0000123"

// toPrecision() - total significant digits (returns string)
console.log(num.toPrecision(4));         // "123.5"
console.log(num.toPrecision(6));         // "123.457"
console.log((123.456).toPrecision(2));   // "1.2e+2"

// toExponential() - exponential notation (returns string)
console.log(num.toExponential(2));       // "1.23e+2"
console.log(num.toExponential(4));       // "1.2346e+2"

// toString() - convert to string with base
console.log(num.toString());             // "123.456789"
console.log((255).toString(16));         // "ff" (hexadecimal)
console.log((10).toString(2));           // "1010" (binary)
console.log((8).toString(8));            // "10" (octal)

// toLocaleString() - locale-specific formatting
let price = 1234567.89;
console.log(price.toLocaleString('en-US')); // "1,234,567.89"
console.log(price.toLocaleString('de-DE')); // "1.234.567,89"
console.log(price.toLocaleString('en-IN')); // "12,34,567.89"
```

---

## Number Properties

```javascript
// Maximum and minimum values
console.log(Number.MAX_VALUE);           // 1.7976931348623157e+308
console.log(Number.MIN_VALUE);           // 5e-324 (smallest positive number)

// Safe integer limits
console.log(Number.MAX_SAFE_INTEGER);    // 9007199254740991 (2^53 - 1)
console.log(Number.MIN_SAFE_INTEGER);    // -9007199254740991

// Special values
console.log(Number.POSITIVE_INFINITY);   // Infinity
console.log(Number.NEGATIVE_INFINITY);   // -Infinity
console.log(Number.NaN);                 // NaN

// Epsilon - smallest difference between two numbers
console.log(Number.EPSILON);             // 2.220446049250313e-16

// Practical use of EPSILON
function areEqual(a, b) {
  return Math.abs(a - b) < Number.EPSILON;
}
console.log(areEqual(0.1 + 0.2, 0.3));   // true (handles floating-point errors)
```

---

## Math Object

The Math object provides mathematical constants and functions.

### Math Constants

```javascript
console.log(Math.PI);                    // 3.141592653589793
console.log(Math.E);                     // 2.718281828459045 (Euler's number)
console.log(Math.LN2);                   // 0.6931471805599453 (ln(2))
console.log(Math.LN10);                  // 2.302585092994046 (ln(10))
console.log(Math.LOG2E);                 // 1.4426950408889634 (log2(e))
console.log(Math.LOG10E);                // 0.4342944819032518 (log10(e))
console.log(Math.SQRT2);                 // 1.4142135623730951 (√2)
console.log(Math.SQRT1_2);               // 0.7071067811865476 (√(1/2))
```

### Rounding Methods

```javascript
let num = 4.7;

// Math.round() - rounds to nearest integer
console.log(Math.round(4.7));            // 5
console.log(Math.round(4.4));            // 4
console.log(Math.round(4.5));            // 5
console.log(Math.round(-4.5));           // -4 (rounds towards positive infinity)

// Math.ceil() - rounds up
console.log(Math.ceil(4.1));             // 5
console.log(Math.ceil(4.9));             // 5
console.log(Math.ceil(-4.1));            // -4

// Math.floor() - rounds down
console.log(Math.floor(4.1));            // 4
console.log(Math.floor(4.9));            // 4
console.log(Math.floor(-4.1));           // -5

// Math.trunc() - removes decimal part (ES6)
console.log(Math.trunc(4.9));            // 4
console.log(Math.trunc(-4.9));           // -4
console.log(Math.trunc(4.1));            // 4

// Rounding to decimal places
function roundToDecimal(num, decimals) {
  const multiplier = Math.pow(10, decimals);
  return Math.round(num * multiplier) / multiplier;
}
console.log(roundToDecimal(4.567, 2));   // 4.57
```

### Power and Root Functions

```javascript
// Math.pow() - exponentiation
console.log(Math.pow(2, 3));             // 8 (2^3)
console.log(Math.pow(4, 0.5));           // 2 (√4)
console.log(Math.pow(8, 1/3));           // 2 (∛8)

// Alternative: ** operator
console.log(2 ** 3);                     // 8
console.log(4 ** 0.5);                   // 2

// Math.sqrt() - square root
console.log(Math.sqrt(16));              // 4
console.log(Math.sqrt(2));               // 1.4142135623730951
console.log(Math.sqrt(-1));              // NaN

// Math.cbrt() - cube root (ES6)
console.log(Math.cbrt(27));              // 3
console.log(Math.cbrt(8));               // 2
```

### Min and Max

```javascript
// Math.min() - minimum value
console.log(Math.min(5, 10, 2, 8));      // 2
console.log(Math.min(-5, -10, -2));      // -10

// Math.max() - maximum value
console.log(Math.max(5, 10, 2, 8));      // 10
console.log(Math.max(-5, -10, -2));      // -2

// With arrays (using spread)
let numbers = [5, 10, 2, 8, 15];
console.log(Math.min(...numbers));       // 2
console.log(Math.max(...numbers));       // 15

// Alternative: apply()
console.log(Math.min.apply(null, numbers)); // 2
```

### Absolute and Sign

```javascript
// Math.abs() - absolute value
console.log(Math.abs(-5));               // 5
console.log(Math.abs(5));                // 5
console.log(Math.abs(-3.14));            // 3.14

// Math.sign() - returns sign of number (ES6)
console.log(Math.sign(5));               // 1 (positive)
console.log(Math.sign(-5));              // -1 (negative)
console.log(Math.sign(0));               // 0
console.log(Math.sign(-0));              // -0
console.log(Math.sign(NaN));             // NaN
```

### Trigonometric Functions

```javascript
// All angles in radians
console.log(Math.sin(Math.PI / 2));      // 1
console.log(Math.cos(Math.PI));          // -1
console.log(Math.tan(Math.PI / 4));      // 1

// Convert degrees to radians
function toRadians(degrees) {
  return degrees * (Math.PI / 180);
}
console.log(Math.sin(toRadians(90)));    // 1

// Inverse functions
console.log(Math.asin(1));               // 1.5707963267948966 (π/2)
console.log(Math.acos(1));               // 0
console.log(Math.atan(1));               // 0.7853981633974483 (π/4)
console.log(Math.atan2(1, 1));           // 0.7853981633974483 (angle from x-axis)

// Hyperbolic functions (ES6)
console.log(Math.sinh(0));               // 0
console.log(Math.cosh(0));               // 1
console.log(Math.tanh(0));               // 0
```

### Logarithmic Functions

```javascript
// Math.log() - natural logarithm (base e)
console.log(Math.log(Math.E));           // 1
console.log(Math.log(10));               // 2.302585092994046

// Math.log10() - base 10 logarithm (ES6)
console.log(Math.log10(100));            // 2
console.log(Math.log10(1000));           // 3

// Math.log2() - base 2 logarithm (ES6)
console.log(Math.log2(8));               // 3
console.log(Math.log2(256));             // 8

// Math.log1p() - log(1 + x) (ES6, more accurate for small x)
console.log(Math.log1p(0));              // 0
console.log(Math.log1p(1));              // 0.6931471805599453

// Math.exp() - e^x
console.log(Math.exp(1));                // 2.718281828459045 (e)
console.log(Math.exp(2));                // 7.38905609893065 (e^2)

// Math.expm1() - e^x - 1 (ES6, more accurate for small x)
console.log(Math.expm1(0));              // 0
console.log(Math.expm1(1));              // 1.718281828459045
```

---

## Random Numbers

### Basic Random Number Generation

```javascript
// Math.random() - random number between 0 (inclusive) and 1 (exclusive)
console.log(Math.random());              // e.g., 0.123456789

// Random integer between 0 and 9
let random = Math.floor(Math.random() * 10);
console.log(random);                     // 0-9

// Random integer between 1 and 10
let dice = Math.floor(Math.random() * 10) + 1;
console.log(dice);                       // 1-10
```

### Random Number Functions

```javascript
// Random integer between min and max (inclusive)
function randomInt(min, max) {
  return Math.floor(Math.random() * (max - min + 1)) + min;
}
console.log(randomInt(1, 6));            // 1-6 (dice roll)
console.log(randomInt(10, 20));          // 10-20

// Random float between min and max
function randomFloat(min, max) {
  return Math.random() * (max - min) + min;
}
console.log(randomFloat(1.5, 5.5));      // e.g., 3.7654

// Random element from array
function randomElement(arr) {
  return arr[Math.floor(Math.random() * arr.length)];
}
let colors = ["red", "green", "blue", "yellow"];
console.log(randomElement(colors));      // random color

// Shuffle array (Fisher-Yates algorithm)
function shuffleArray(arr) {
  let shuffled = [...arr];
  for (let i = shuffled.length - 1; i > 0; i--) {
    let j = Math.floor(Math.random() * (i + 1));
    [shuffled[i], shuffled[j]] = [shuffled[j], shuffled[i]];
  }
  return shuffled;
}
let nums = [1, 2, 3, 4, 5];
console.log(shuffleArray(nums));         // e.g., [3, 1, 5, 2, 4]
```

### Practical Random Examples

```javascript
// Random hex color
function randomHexColor() {
  return '#' + Math.floor(Math.random() * 16777215).toString(16).padStart(6, '0');
}
console.log(randomHexColor());           // e.g., "#a3f2b5"

// Random boolean
function randomBoolean() {
  return Math.random() < 0.5;
}
console.log(randomBoolean());            // true or false

// Random with probability (e.g., 30% chance)
function probability(percent) {
  return Math.random() < percent / 100;
}
console.log(probability(30));            // 30% chance of true
```

---

## Number Formatting

### Currency Formatting

```javascript
let price = 1234.56;

// Using toLocaleString with options
let usd = price.toLocaleString('en-US', {
  style: 'currency',
  currency: 'USD'
});
console.log(usd);                        // "$1,234.56"

let eur = price.toLocaleString('de-DE', {
  style: 'currency',
  currency: 'EUR'
});
console.log(eur);                        // "1.234,56 €"

let inr = price.toLocaleString('en-IN', {
  style: 'currency',
  currency: 'INR'
});
console.log(inr);                        // "₹1,234.56"
```

### Percentage Formatting

```javascript
let percent = 0.756;

let formatted = percent.toLocaleString('en-US', {
  style: 'percent',
  minimumFractionDigits: 1
});
console.log(formatted);                  // "75.6%"
```

### Number with Units

```javascript
let distance = 1234.5;

let km = distance.toLocaleString('en-US', {
  style: 'unit',
  unit: 'kilometer'
});
console.log(km);                         // "1,234.5 km"

let temp = 25;
let celsius = temp.toLocaleString('en-US', {
  style: 'unit',
  unit: 'celsius'
});
console.log(celsius);                    // "25°C"
```

### Compact Notation

```javascript
let big = 1234567;

let compact = big.toLocaleString('en-US', {
  notation: 'compact'
});
console.log(compact);                    // "1.2M"

let scientific = big.toLocaleString('en-US', {
  notation: 'scientific'
});
console.log(scientific);                 // "1.235E6"
```

---

## Precision and Rounding

### Floating-Point Precision Issues

```javascript
// JavaScript uses binary floating-point (can't represent all decimals exactly)
console.log(0.1 + 0.2);                  // 0.30000000000000004 ❌
console.log(0.1 + 0.2 === 0.3);          // false

// Solution 1: Round to fixed decimals
console.log((0.1 + 0.2).toFixed(2));     // "0.30"
console.log(Number((0.1 + 0.2).toFixed(10))); // 0.3

// Solution 2: Use epsilon for comparison
function areEqual(a, b, epsilon = Number.EPSILON) {
  return Math.abs(a - b) < epsilon;
}
console.log(areEqual(0.1 + 0.2, 0.3));   // true ✓

// Solution 3: Work with integers (for money)
let price1 = 10; // $0.10 in cents
let price2 = 20; // $0.20 in cents
let total = price1 + price2; // 30 cents
console.log(total / 100);                // 0.3 ✓
```

### Decimal Rounding Strategies

```javascript
let num = 1.2345;

// Round to 2 decimal places
function round(num, decimals = 2) {
  return Math.round(num * Math.pow(10, decimals)) / Math.pow(10, decimals);
}
console.log(round(num, 2));              // 1.23

// Always round down
function roundDown(num, decimals = 2) {
  return Math.floor(num * Math.pow(10, decimals)) / Math.pow(10, decimals);
}
console.log(roundDown(num, 2));          // 1.23

// Always round up
function roundUp(num, decimals = 2) {
  return Math.ceil(num * Math.pow(10, decimals)) / Math.pow(10, decimals);
}
console.log(roundUp(num, 2));            // 1.24

// Banker's rounding (round to nearest even)
function bankersRound(num) {
  let rounded = Math.round(num);
  if (Math.abs(num - rounded) === 0.5) {
    return rounded % 2 === 0 ? rounded : rounded - Math.sign(num);
  }
  return rounded;
}
console.log(bankersRound(2.5));          // 2
console.log(bankersRound(3.5));          // 4
```

---

## ⚠️ Common Mistakes

### 1. Floating-Point Arithmetic

```javascript
// ❌ Wrong: Expecting exact decimal arithmetic
console.log(0.1 + 0.2 === 0.3);          // false

// ✓ Correct: Use toFixed or epsilon comparison
console.log((0.1 + 0.2).toFixed(1) == 0.3); // true
console.log(Math.abs((0.1 + 0.2) - 0.3) < Number.EPSILON); // true
```

### 2. NaN Comparison

```javascript
let num = NaN;

// ❌ Wrong: Comparing with ===
console.log(num === NaN);                // false (NaN !== NaN)

// ✓ Correct: Use Number.isNaN()
console.log(Number.isNaN(num));          // true
```

### 3. parseInt Without Radix

```javascript
// ❌ Wrong: Missing radix can cause issues
console.log(parseInt("08"));             // 8 (but could be octal in older browsers)

// ✓ Correct: Always specify radix
console.log(parseInt("08", 10));         // 8
console.log(parseInt("FF", 16));         // 255
```

### 4. Using toFixed for Comparison

```javascript
let num = 1.005;

// ❌ Wrong: toFixed returns string
console.log(num.toFixed(2));             // "1.01"
console.log(num.toFixed(2) === 1.01);    // false (string vs number)

// ✓ Correct: Convert back to number
console.log(Number(num.toFixed(2)));     // 1.01
console.log(Number(num.toFixed(2)) === 1.01); // true
```

### 5. Math.random() Range

```javascript
// ❌ Wrong: Off-by-one error
let wrong = Math.floor(Math.random() * 10); // 0-9 (missing 10)

// ✓ Correct: For range 1-10
let correct = Math.floor(Math.random() * 10) + 1; // 1-10
```

---

## 💼 Interview Tips

### Q1: Why does 0.1 + 0.2 !== 0.3 in JavaScript?

**Answer:**
JavaScript uses binary floating-point arithmetic (IEEE 754). Decimal numbers like 0.1 and 0.2 cannot be represented exactly in binary, causing precision errors.

```javascript
console.log(0.1 + 0.2);                  // 0.30000000000000004

// Solutions:
// 1. Use toFixed()
console.log((0.1 + 0.2).toFixed(2));     // "0.30"

// 2. Use epsilon comparison
console.log(Math.abs((0.1 + 0.2) - 0.3) < Number.EPSILON); // true

// 3. Work with integers (for currency)
let cents1 = 10, cents2 = 20;
let total = cents1 + cents2;             // 30 cents = $0.30
```

### Q2: How do you generate a random number in a specific range?

**Answer:**
```javascript
// Random integer between min and max (inclusive)
function randomInt(min, max) {
  return Math.floor(Math.random() * (max - min + 1)) + min;
}

// Examples:
console.log(randomInt(1, 6));            // Dice roll (1-6)
console.log(randomInt(0, 100));          // Percentage (0-100)
```

### Q3: What's the difference between Math.floor() and Math.trunc()?

**Answer:**
- **Math.floor()**: Rounds down to the nearest integer (towards negative infinity)
- **Math.trunc()**: Removes the decimal part (towards zero)

```javascript
console.log(Math.floor(4.9));            // 4
console.log(Math.trunc(4.9));            // 4

console.log(Math.floor(-4.9));           // -5 (down)
console.log(Math.trunc(-4.9));           // -4 (towards zero)
```

### Q4: How do you check if a value is NaN?

**Answer:**
Use `Number.isNaN()`, not the global `isNaN()`:

```javascript
// ❌ Wrong: isNaN converts to number first
console.log(isNaN("abc"));               // true (converts "abc" to NaN)

// ✓ Correct: Number.isNaN doesn't convert
console.log(Number.isNaN(NaN));          // true
console.log(Number.isNaN("abc"));        // false

// NaN is the only value not equal to itself
console.log(NaN === NaN);                // false
```

### Q5: What's the safe integer range in JavaScript?

**Answer:**
Safe integers are between `-(2^53 - 1)` and `2^53 - 1`:

```javascript
console.log(Number.MAX_SAFE_INTEGER);    // 9007199254740991
console.log(Number.MIN_SAFE_INTEGER);    // -9007199254740991

// Check if safe
console.log(Number.isSafeInteger(9007199254740991));  // true
console.log(Number.isSafeInteger(9007199254740992));  // false

// For larger integers, use BigInt
let bigNum = 9007199254740992n;
console.log(typeof bigNum);              // "bigint"
```

---

## Practice Exercises

### Exercise 1: Round to Decimal Places
Write a function that rounds a number to specified decimal places.

```javascript
function roundTo(num, decimals) {
  // Your code here
}

console.log(roundTo(3.14159, 2));        // 3.14
console.log(roundTo(2.5, 0));            // 3
console.log(roundTo(1.005, 2));          // 1.01
```

<details>
<summary>Solution</summary>

```javascript
function roundTo(num, decimals) {
  const multiplier = Math.pow(10, decimals);
  return Math.round(num * multiplier) / multiplier;
}

// Alternative using toFixed
function roundTo2(num, decimals) {
  return Number(num.toFixed(decimals));
}
```
</details>

### Exercise 2: Random Between Range
Create a function that generates a random number between min and max (inclusive).

```javascript
function random(min, max) {
  // Your code here
}

console.log(random(1, 10));              // Random between 1-10
console.log(random(50, 100));            // Random between 50-100
```

<details>
<summary>Solution</summary>

```javascript
function random(min, max) {
  return Math.floor(Math.random() * (max - min + 1)) + min;
}

// For float values
function randomFloat(min, max) {
  return Math.random() * (max - min) + min;
}
```
</details>

### Exercise 3: Calculate Percentage
Write functions to calculate percentage and find what percentage one number is of another.

```javascript
function getPercentage(value, total) {
  // Your code here (e.g., what % is 25 of 200?)
}

function applyPercentage(value, percent) {
  // Your code here (e.g., 20% of 150)
}

console.log(getPercentage(25, 200));     // 12.5
console.log(applyPercentage(150, 20));   // 30
```

<details>
<summary>Solution</summary>

```javascript
function getPercentage(value, total) {
  return (value / total) * 100;
}

function applyPercentage(value, percent) {
  return (value * percent) / 100;
}

// With rounding
function getPercentageRounded(value, total, decimals = 2) {
  return Number(((value / total) * 100).toFixed(decimals));
}
```
</details>

### Exercise 4: Check if Prime
Write a function to check if a number is prime.

```javascript
function isPrime(num) {
  // Your code here
}

console.log(isPrime(7));                 // true
console.log(isPrime(12));                // false
console.log(isPrime(1));                 // false
```

<details>
<summary>Solution</summary>

```javascript
function isPrime(num) {
  if (num <= 1) return false;
  if (num <= 3) return true;
  
  if (num % 2 === 0 || num % 3 === 0) return false;
  
  for (let i = 5; i * i <= num; i += 6) {
    if (num % i === 0 || num % (i + 2) === 0) {
      return false;
    }
  }
  
  return true;
}

// Simple version (less efficient)
function isPrimeSimple(num) {
  if (num <= 1) return false;
  for (let i = 2; i < num; i++) {
    if (num % i === 0) return false;
  }
  return true;
}
```
</details>

---

**[← Back: Strings](./04-strings.md)** | **[Next: Dates →](./06-dates.md)**

---

**Made with ❤️ for JavaScript learners**
