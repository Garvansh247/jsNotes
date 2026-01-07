# 🔀 Conditionals in JavaScript

## 📑 Table of Contents
- [if Statement](#if-statement)
- [if...else Statement](#ifelse-statement)
- [else if Statement](#else-if-statement)
- [switch Statement](#switch-statement)
- [Ternary Operator](#ternary-operator)
- [Short-Circuit Evaluation](#short-circuit-evaluation)
- [Nullish Coalescing](#nullish-coalescing)
- [Common Mistakes](#-common-mistakes)
- [Interview Tips](#-interview-tips)
- [Practice Exercises](#practice-exercises)

---

## if Statement

```javascript
let age = 18;

if (age >= 18) {
  console.log("You are an adult");
}

// Without braces (single statement)
if (age >= 18)
  console.log("Adult");

// Multiple conditions
if (age >= 18 && age < 65) {
  console.log("Working age");
}
```

---

## if...else Statement

```javascript
let age = 15;

if (age >= 18) {
  console.log("Adult");
} else {
  console.log("Minor");
}

// Nested if-else
let score = 85;

if (score >= 90) {
  console.log("A");
} else {
  if (score >= 80) {
    console.log("B");
  } else {
    console.log("C");
  }
}
```

---

## else if Statement

```javascript
let score = 85;

if (score >= 90) {
  console.log("Grade: A");
} else if (score >= 80) {
  console.log("Grade: B");
} else if (score >= 70) {
  console.log("Grade: C");
} else if (score >= 60) {
  console.log("Grade: D");
} else {
  console.log("Grade: F");
}
```

---

## switch Statement

```javascript
let day = 3;

switch (day) {
  case 1:
    console.log("Monday");
    break;
  case 2:
    console.log("Tuesday");
    break;
  case 3:
    console.log("Wednesday");
    break;
  case 4:
    console.log("Thursday");
    break;
  case 5:
    console.log("Friday");
    break;
  case 6:
  case 7:
    console.log("Weekend");
    break;
  default:
    console.log("Invalid day");
}

// Multiple cases
let fruit = "apple";

switch (fruit) {
  case "apple":
  case "orange":
  case "banana":
    console.log("Common fruit");
    break;
  case "mango":
  case "papaya":
    console.log("Tropical fruit");
    break;
  default:
    console.log("Unknown fruit");
}
```

---

## Ternary Operator

```javascript
// Syntax: condition ? valueIfTrue : valueIfFalse

let age = 20;
let status = age >= 18 ? "Adult" : "Minor";
console.log(status);  // "Adult"

// Nested ternary
let score = 85;
let grade = score >= 90 ? "A" :
            score >= 80 ? "B" :
            score >= 70 ? "C" : "F";

// In expressions
let price = 100;
let total = price * (age >= 65 ? 0.8 : 1);  // Senior discount
```

---

## Short-Circuit Evaluation

### && (AND)

```javascript
// Returns first falsy value or last value
true && true;          // true
false && true;         // false
"hello" && "world";    // "world"
null && "hello";       // null

// Practical use: conditional execution
let user = {name: "John"};
user && console.log(user.name);  // Logs "John"

// Default parameter alternative
function greet(name) {
  name = name && name.toUpperCase();
  console.log(name || "GUEST");
}
```

### || (OR)

```javascript
// Returns first truthy value or last value
true || false;         // true
false || true;         // true
"hello" || "world";    // "hello"
null || "default";     // "default"

// Practical use: default values
let userName = null;
let display = userName || "Guest";
console.log(display);  // "Guest"

function greet(name) {
  name = name || "Guest";
  console.log(`Hello, ${name}`);
}
greet();        // "Hello, Guest"
greet("John");  // "Hello, John"
```

---

## Nullish Coalescing

```javascript
// ?? returns right operand when left is null/undefined only
let x = 0 ?? 10;        // 0 (0 is not nullish)
let y = null ?? 10;     // 10
let z = undefined ?? 10; // 10
let a = "" ?? "default";  // "" (empty string is not nullish)

// Compare with ||
0 || 10;        // 10 (0 is falsy)
0 ?? 10;        // 0 (0 is not nullish)

"" || "default";  // "default"
"" ?? "default";  // ""

// Practical use
let count = 0;
let display = count || 10;   // 10 (wrong!)
let display2 = count ?? 10;  // 0 (correct!)

// With optional chaining
let user = null;
let name = user?.name ?? "Guest";
```

---

## ⚠️ Common Mistakes

### Forgetting break in switch

```javascript
// ❌ Wrong: Falls through
let x = 2;
switch (x) {
  case 1:
    console.log("One");
  case 2:
    console.log("Two");  // Executes
  case 3:
    console.log("Three");  // Also executes!
}

// ✓ Correct
switch (x) {
  case 1:
    console.log("One");
    break;
  case 2:
    console.log("Two");
    break;
  case 3:
    console.log("Three");
    break;
}
```

### Assignment vs Comparison

```javascript
let x = 5;

// ❌ Wrong: Assignment
if (x = 10) {  // Assigns 10 to x
  console.log("True");  // Always executes
}

// ✓ Correct
if (x === 10) {
  console.log("Equal");
}
```

---

## 💼 Interview Tips

### Q1: What's the difference between == and ===?

**Answer:**
- `==`: Loose equality (type coercion)
- `===`: Strict equality (no type coercion)

```javascript
5 == "5";   // true
5 === "5";  // false
```

### Q2: What's the difference between || and ??

**Answer:**
- `||`: Returns right operand if left is falsy
- `??`: Returns right operand if left is null/undefined only

```javascript
0 || 10;   // 10
0 ?? 10;   // 0

"" || "default";   // "default"
"" ?? "default";   // ""
```

### Q3: When to use switch vs if-else?

**Answer:**
- **switch**: Multiple exact value comparisons
- **if-else**: Complex conditions, ranges, boolean logic

---

## Practice Exercises

### Exercise 1: Grade Calculator
Write a function to return grade based on score.

```javascript
function getGrade(score) {
  // Your code here
}

console.log(getGrade(95));  // "A"
console.log(getGrade(85));  // "B"
```

<details>
<summary>Solution</summary>

```javascript
function getGrade(score) {
  if (score >= 90) return "A";
  if (score >= 80) return "B";
  if (score >= 70) return "C";
  if (score >= 60) return "D";
  return "F";
}

// Or using ternary
function getGrade(score) {
  return score >= 90 ? "A" :
         score >= 80 ? "B" :
         score >= 70 ? "C" :
         score >= 60 ? "D" : "F";
}
```
</details>

---

**[← Back: This Keyword](../03-functions/04-this-keyword.md)** | **[Next: Loops →](./02-loops.md)**

---

**Made with ❤️ for JavaScript learners**
