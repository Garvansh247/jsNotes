# ⚙️ JavaScript Operators

## 📑 Table of Contents
- [Arithmetic Operators](#arithmetic-operators)
- [Assignment Operators](#assignment-operators)
- [Comparison Operators](#comparison-operators)
- [Logical Operators](#logical-operators)
- [Bitwise Operators](#bitwise-operators)
- [String Operators](#string-operators)
- [Special Operators](#special-operators)
- [Operator Precedence](#operator-precedence)
- [Common Mistakes](#-common-mistakes)
- [Interview Tips](#-interview-tips)
- [Practice Exercises](#practice-exercises)

---

## Arithmetic Operators

Used to perform mathematical operations.

```javascript
let a = 10, b = 3;

// Addition
console.log(a + b);      // 13

// Subtraction
console.log(a - b);      // 7

// Multiplication
console.log(a * b);      // 30

// Division
console.log(a / b);      // 3.333...

// Modulus (Remainder)
console.log(a % b);      // 1

// Exponentiation (ES2016)
console.log(a ** b);     // 1000 (10^3)

// Increment
let x = 5;
console.log(++x);        // 6 (pre-increment: increment then return)
console.log(x++);        // 6 (post-increment: return then increment)
console.log(x);          // 7

// Decrement
let y = 5;
console.log(--y);        // 4 (pre-decrement)
console.log(y--);        // 4 (post-decrement)
console.log(y);          // 3

// Unary plus/minus
console.log(+"5");       // 5 (converts to number)
console.log(-"5");       // -5
console.log(+true);      // 1
console.log(+false);     // 0
```

---

## Assignment Operators

Used to assign values to variables.

```javascript
let x = 10;

// Simple assignment
x = 5;               // x = 5

// Addition assignment
x += 3;              // x = x + 3 → x = 8

// Subtraction assignment
x -= 2;              // x = x - 2 → x = 6

// Multiplication assignment
x *= 4;              // x = x * 4 → x = 24

// Division assignment
x /= 3;              // x = x / 3 → x = 8

// Modulus assignment
x %= 5;              // x = x % 5 → x = 3

// Exponentiation assignment
x **= 2;             // x = x ** 2 → x = 9

// Logical AND assignment (ES2021)
let a = 1;
a &&= 2;             // a = a && 2 → a = 2 (if a is truthy)

let b = 0;
b &&= 2;             // b = 0 (b is falsy, no assignment)

// Logical OR assignment (ES2021)
let c = null;
c ||= "default";     // c = c || "default" → c = "default"

let d = "existing";
d ||= "default";     // d = "existing" (already truthy)

// Nullish coalescing assignment (ES2021)
let e = null;
e ??= "default";     // e = e ?? "default" → e = "default"

let f = 0;
f ??= 10;            // f = 0 (0 is not null/undefined)
```

---

## Comparison Operators

Used to compare two values and return a boolean.

```javascript
// Equality (loose) - performs type coercion
console.log(5 == "5");       // true
console.log(1 == true);      // true
console.log(0 == false);     // true
console.log(null == undefined); // true

// Inequality (loose)
console.log(5 != "5");       // false

// Strict equality - NO type coercion
console.log(5 === "5");      // false
console.log(5 === 5);        // true
console.log(1 === true);     // false

// Strict inequality
console.log(5 !== "5");      // true
console.log(5 !== 5);        // false

// Greater than
console.log(10 > 5);         // true
console.log(5 > 5);          // false

// Greater than or equal
console.log(10 >= 10);       // true
console.log(5 >= 10);        // false

// Less than
console.log(5 < 10);         // true
console.log(10 < 5);         // false

// Less than or equal
console.log(5 <= 5);         // true
console.log(10 <= 5);        // false

// Special comparisons
console.log(NaN == NaN);     // false (NaN is not equal to anything)
console.log(NaN === NaN);    // false
console.log(null == 0);      // false
console.log(undefined == 0); // false
```

**Best Practice:** Always use `===` and `!==` for comparisons to avoid unexpected type coercion bugs.

---

## Logical Operators

Used to combine or invert boolean values.

```javascript
// Logical AND (&&) - returns first falsy value or last value
console.log(true && true);     // true
console.log(true && false);    // false
console.log(5 && 10);          // 10 (both truthy, returns last)
console.log(0 && 10);          // 0 (first falsy)
console.log("" && "hello");    // "" (first falsy)

// Logical OR (||) - returns first truthy value or last value
console.log(true || false);    // true
console.log(false || true);    // true
console.log(0 || 10);          // 10 (first truthy)
console.log(null || "default"); // "default"
console.log("" || 0 || "hi");  // "hi" (first truthy)

// Logical NOT (!) - inverts boolean value
console.log(!true);            // false
console.log(!false);           // true
console.log(!0);               // true
console.log(!"hello");         // false
console.log(!!0);              // false (double NOT converts to boolean)
console.log(!!"hello");        // true

// Short-circuit evaluation
let user = null;
let name = user && user.name;  // null (doesn't try to access .name)

let defaultName = userName || "Guest";  // Use "Guest" if userName is falsy

// Chaining
console.log(true && true && false);  // false
console.log(false || false || true); // true
```

---

## Special Operators

### Ternary Operator

```javascript
// Syntax: condition ? expressionIfTrue : expressionIfFalse
let age = 18;
let status = age >= 18 ? "adult" : "minor";
console.log(status);  // "adult"

// Nested ternary
let score = 85;
let grade = score >= 90 ? "A" : score >= 80 ? "B" : score >= 70 ? "C" : "F";
console.log(grade);  // "B"

// With function calls
let result = isValid ? processData() : showError();
```

### Nullish Coalescing Operator (??)

```javascript
// Returns right operand when left is null or undefined
// (unlike || which checks for any falsy value)

let value1 = null ?? "default";      // "default"
let value2 = undefined ?? "default"; // "default"
let value3 = 0 ?? "default";         // 0 (0 is not null/undefined)
let value4 = "" ?? "default";        // "" (empty string is not null/undefined)
let value5 = false ?? "default";     // false

// Useful for default values when 0 or "" are valid
let count = 0;
let result1 = count || 10;    // 10 (wrong! 0 is falsy)
let result2 = count ?? 10;    // 0 (correct!)

let name = "";
let displayName1 = name || "Anonymous";  // "Anonymous" (wrong! "" is falsy)
let displayName2 = name ?? "Anonymous";  // "" (correct!)
```

### Optional Chaining Operator (?.)

```javascript
// Safely access nested properties
let user = {
  name: "John",
  address: {
    city: "NYC"
  }
};

// Without optional chaining
let city1 = user && user.address && user.address.city;  // "NYC"

// With optional chaining
let city2 = user?.address?.city;  // "NYC"

// If property doesn't exist
let user2 = null;
let city3 = user2?.address?.city;  // undefined (no error!)

// With arrays
let arr = null;
console.log(arr?.[0]);  // undefined (no error)

// With functions
let obj = {};
console.log(obj.method?.());  // undefined (no error if method doesn't exist)

// Practical example
function getUsername(user) {
  return user?.profile?.name ?? "Anonymous";
}

console.log(getUsername({ profile: { name: "John" } }));  // "John"
console.log(getUsername(null));  // "Anonymous"
```

### Spread Operator (...)

```javascript
// Arrays
let arr1 = [1, 2, 3];
let arr2 = [...arr1, 4, 5];  // [1, 2, 3, 4, 5]

// Objects
let obj1 = { a: 1, b: 2 };
let obj2 = { ...obj1, c: 3 };  // { a: 1, b: 2, c: 3 }

// Function arguments
function sum(a, b, c) {
  return a + b + c;
}
let numbers = [1, 2, 3];
console.log(sum(...numbers));  // 6

// Copying
let original = [1, 2, 3];
let copy = [...original];  // Shallow copy
```

### Comma Operator

```javascript
// Evaluates each expression and returns the last one
let x = (1, 2, 3);
console.log(x);  // 3

// In for loops
for (let i = 0, j = 10; i < 5; i++, j--) {
  console.log(i, j);  // 0 10, 1 9, 2 8, 3 7, 4 6
}

// In expressions (rarely used)
let y = (console.log("Hello"), 5 + 5);  // Logs "Hello", returns 10
```

### typeof Operator

```javascript
console.log(typeof "hello");      // "string"
console.log(typeof 42);           // "number"
console.log(typeof true);         // "boolean"
console.log(typeof undefined);    // "undefined"
console.log(typeof null);         // "object" (bug!)
console.log(typeof {});           // "object"
console.log(typeof []);           // "object"
console.log(typeof function(){}); // "function"
```

### instanceof Operator

```javascript
// Check if object is instance of a class/constructor
let arr = [1, 2, 3];
console.log(arr instanceof Array);   // true
console.log(arr instanceof Object);  // true

let date = new Date();
console.log(date instanceof Date);   // true

class Person {}
let john = new Person();
console.log(john instanceof Person); // true
```

### delete Operator

```javascript
// Delete object property
let obj = { a: 1, b: 2, c: 3 };
delete obj.b;
console.log(obj);  // { a: 1, c: 3 }

// Cannot delete variables
let x = 10;
delete x;  // false (doesn't work)
console.log(x);  // 10

// Cannot delete array elements properly (leaves empty slot)
let arr = [1, 2, 3];
delete arr[1];
console.log(arr);  // [1, empty, 3]
console.log(arr.length);  // 3 (length unchanged)

// Use splice instead for arrays
arr.splice(1, 1);  // Better way
```

---

## Operator Precedence

Operators are evaluated in order of precedence (highest to lowest):

| Precedence | Operator | Description |
|------------|----------|-------------|
| 20 | `()` | Grouping |
| 19 | `.` `[]` | Member access |
| 18 | `()` | Function call |
| 17 | `new` | new with arguments |
| 16 | `++` `--` | Postfix increment/decrement |
| 15 | `!` `~` `+` `-` `++` `--` `typeof` | Unary operators |
| 14 | `**` | Exponentiation |
| 13 | `*` `/` `%` | Multiplication, Division, Modulus |
| 12 | `+` `-` | Addition, Subtraction |
| 11 | `<<` `>>` `>>>` | Bitwise shift |
| 10 | `<` `<=` `>` `>=` | Comparison |
| 9 | `==` `!=` `===` `!==` | Equality |
| 8 | `&` | Bitwise AND |
| 7 | `^` | Bitwise XOR |
| 6 | `|` | Bitwise OR |
| 5 | `&&` | Logical AND |
| 4 | `||` | Logical OR |
| 3 | `??` | Nullish coalescing |
| 2 | `? :` | Ternary |
| 1 | `=` `+=` etc. | Assignment |

```javascript
// Examples
console.log(2 + 3 * 4);        // 14 (not 20, * before +)
console.log((2 + 3) * 4);      // 20 (parentheses change order)

console.log(10 - 5 - 2);       // 3 (left-to-right for same precedence)
console.log(2 ** 3 ** 2);      // 512 (right-to-left for **)

console.log(true || false && false);  // true (&& before ||)
console.log((true || false) && false); // false (parentheses change order)
```

---

## ⚠️ Common Mistakes

### Mistake 1: Comparing with = instead of ==

```javascript
// ❌ Wrong
if (x = 5) {  // Assignment, not comparison!
  console.log("Always true");
}

// ✓ Correct
if (x == 5) {  // Or better, x === 5
  console.log("Equal");
}
```

### Mistake 2: Using == instead of ===

```javascript
// ❌ Wrong
if (value == 0) {  // matches 0, "0", false, "", [], etc.
  // Unexpected matches
}

// ✓ Correct
if (value === 0) {  // Only matches number 0
  // Expected match
}
```

### Mistake 3: Confusing || with ??

```javascript
let count = 0;

// ❌ Wrong
let result = count || 10;  // 10 (0 is falsy, but it's a valid value!)

// ✓ Correct
let result = count ?? 10;  // 0 (only null/undefined are replaced)
```

### Mistake 4: Post vs Pre Increment

```javascript
let x = 5;

// Post-increment
console.log(x++);  // 5 (returns current value, then increments)
console.log(x);    // 6

let y = 5;

// Pre-increment
console.log(++y);  // 6 (increments first, then returns)
console.log(y);    // 6
```

---

## 💼 Interview Tips

### Q1: What's the difference between == and ===?

**Answer:**
- `==` (loose equality): Performs type coercion before comparison
- `===` (strict equality): No type coercion, types must match

Always prefer `===` unless you specifically need type coercion.

### Q2: What is operator precedence?

**Answer:** Operator precedence determines the order in which operators are evaluated in an expression. Operators with higher precedence are evaluated first.

Example: `2 + 3 * 4` equals `14` because `*` has higher precedence than `+`.

### Q3: What is short-circuit evaluation?

**Answer:** Logical operators `&&` and `||` short-circuit, meaning they stop evaluating as soon as the result is determined.

```javascript
false && expensiveFunction();  // expensiveFunction() never called
true || expensiveFunction();   // expensiveFunction() never called
```

### Q4: What does the ?? operator do?

**Answer:** The nullish coalescing operator (`??`) returns the right operand when the left operand is `null` or `undefined`, unlike `||` which returns the right operand for any falsy value.

### Q5: Explain the ternary operator.

**Answer:** The ternary operator is a shorthand for if-else statements.

Syntax: `condition ? expressionIfTrue : expressionIfFalse`

---

## Practice Exercises

### Exercise 1: Predict the Output
```javascript
console.log(10 + "5");
console.log(10 - "5");
console.log(10 == "10");
console.log(10 === "10");
console.log(0 || "hello");
console.log(0 ?? "hello");
```

<details>
<summary>Solution</summary>

```javascript
console.log(10 + "5");      // "105" (string concatenation)
console.log(10 - "5");      // 5 (numeric subtraction)
console.log(10 == "10");    // true (loose equality with coercion)
console.log(10 === "10");   // false (strict equality, different types)
console.log(0 || "hello");  // "hello" (0 is falsy)
console.log(0 ?? "hello");  // 0 (0 is not null/undefined)
```
</details>

### Exercise 2: Rewrite using ternary
```javascript
let age = 25;
let category;
if (age >= 18) {
  category = "adult";
} else {
  category = "minor";
}
```

<details>
<summary>Solution</summary>

```javascript
let age = 25;
let category = age >= 18 ? "adult" : "minor";
```
</details>

---

**[← Previous: Type Conversion](./02-type-conversion.md)** | **[Next: Strings →](./04-strings.md)**

---

**Made with ❤️ for JavaScript learners**
