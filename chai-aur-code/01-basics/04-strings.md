# 🔤 Strings in JavaScript

## 📑 Table of Contents
- [String Basics](#string-basics)
- [String Creation](#string-creation)
- [Template Literals](#template-literals)
- [String Properties](#string-properties)
- [String Methods](#string-methods)
- [String Manipulation](#string-manipulation)
- [Escape Characters](#escape-characters)
- [Common Mistakes](#-common-mistakes)
- [Interview Tips](#-interview-tips)
- [Practice Exercises](#practice-exercises)

---

## String Basics

Strings are used to represent text in JavaScript. They are sequences of characters enclosed in quotes.

```javascript
let single = 'Hello';
let double = "World";
let backtick = `JavaScript`;

// All three are valid strings
console.log(single);    // Hello
console.log(double);    // World
console.log(backtick);  // JavaScript
```

### When to Use Which Quotes?

```javascript
// Single quotes - most common
let name = 'John';

// Double quotes - when string contains single quotes
let message = "It's a beautiful day";

// Backticks - for template literals and multiline strings
let greeting = `Hello, ${name}!`;
```

---

## String Creation

### Primitive String vs String Object

```javascript
// Primitive string (recommended)
let str1 = "Hello";
console.log(typeof str1);        // "string"

// String object (avoid)
let str2 = new String("Hello");
console.log(typeof str2);        // "object"

// Comparison
console.log(str1 == str2);       // true (value comparison)
console.log(str1 === str2);      // false (type difference)

// Always use primitive strings
let name = "JavaScript";         // ✓ Correct
// let name = new String("JS");  // ❌ Avoid
```

---

## Template Literals

Template literals (backticks) provide powerful string features introduced in ES6.

### String Interpolation

```javascript
let name = "John";
let age = 30;

// Old way (concatenation)
let message1 = "My name is " + name + " and I am " + age + " years old.";

// New way (template literal)
let message2 = `My name is ${name} and I am ${age} years old.`;

console.log(message2); // My name is John and I am 30 years old.

// Expressions inside ${}
let a = 5, b = 10;
console.log(`Sum: ${a + b}`);           // Sum: 15
console.log(`Product: ${a * b}`);       // Product: 50
console.log(`Is greater: ${a > b}`);    // Is greater: false
```

### Multiline Strings

```javascript
// Old way (difficult)
let oldMultiline = "This is line 1\n" +
                   "This is line 2\n" +
                   "This is line 3";

// New way (easy)
let newMultiline = `This is line 1
This is line 2
This is line 3`;

console.log(newMultiline);
// This is line 1
// This is line 2
// This is line 3

// HTML template example
let html = `
  <div class="card">
    <h2>${name}</h2>
    <p>Age: ${age}</p>
  </div>
`;
```

### Tagged Templates

```javascript
function highlight(strings, ...values) {
  return strings.reduce((result, str, i) => {
    return `${result}${str}<strong>${values[i] || ''}</strong>`;
  }, '');
}

let name = "John";
let age = 30;
let tagged = highlight`Name: ${name}, Age: ${age}`;
console.log(tagged); // Name: <strong>John</strong>, Age: <strong>30</strong>
```

---

## String Properties

### Length Property

```javascript
let text = "Hello World";
console.log(text.length);        // 11

// Empty string
let empty = "";
console.log(empty.length);       // 0

// Spaces count
let spaces = "   ";
console.log(spaces.length);      // 3

// Unicode characters
let emoji = "🚀";
console.log(emoji.length);       // 2 (some emojis are 2 chars)

// String length is read-only
text.length = 5;
console.log(text.length);        // Still 11 (can't change)
```

---

## String Methods

### Accessing Characters

```javascript
let str = "Hello";

// charAt() - get character at index
console.log(str.charAt(0));      // "H"
console.log(str.charAt(4));      // "o"
console.log(str.charAt(10));     // "" (empty string if out of bounds)

// charCodeAt() - get Unicode value
console.log(str.charCodeAt(0));  // 72 (Unicode for 'H')

// Bracket notation (modern)
console.log(str[0]);             // "H"
console.log(str[4]);             // "o"
console.log(str[10]);            // undefined (if out of bounds)
```

### Case Conversion

```javascript
let text = "Hello World";

// toUpperCase()
console.log(text.toUpperCase());  // "HELLO WORLD"

// toLowerCase()
console.log(text.toLowerCase());  // "hello world"

// Original string unchanged (strings are immutable)
console.log(text);                // "Hello World"

// Practical use case: case-insensitive comparison
let input = "JAVASCRIPT";
let correct = "javascript";
console.log(input.toLowerCase() === correct); // true
```

### Searching Strings

```javascript
let str = "JavaScript is awesome. JavaScript is fun!";

// indexOf() - first occurrence
console.log(str.indexOf("JavaScript"));      // 0
console.log(str.indexOf("is"));              // 11
console.log(str.indexOf("Python"));          // -1 (not found)

// indexOf() with start position
console.log(str.indexOf("JavaScript", 1));   // 23 (search from index 1)

// lastIndexOf() - last occurrence
console.log(str.lastIndexOf("JavaScript"));  // 23

// includes() - returns boolean (ES6)
console.log(str.includes("awesome"));        // true
console.log(str.includes("python"));         // false

// startsWith() - check if string starts with (ES6)
console.log(str.startsWith("Java"));         // true
console.log(str.startsWith("Script"));       // false

// endsWith() - check if string ends with (ES6)
console.log(str.endsWith("fun!"));           // true
console.log(str.endsWith("awesome"));        // false
```

### Extracting String Parts

```javascript
let text = "JavaScript Programming";

// slice(start, end) - extracts part of string
console.log(text.slice(0, 10));        // "JavaScript"
console.log(text.slice(11));           // "Programming"
console.log(text.slice(-11));          // "Programming" (negative = from end)
console.log(text.slice(-11, -1));      // "Programmin"

// substring(start, end) - similar to slice
console.log(text.substring(0, 10));    // "JavaScript"
console.log(text.substring(11));       // "Programming"
// Negative values treated as 0
console.log(text.substring(-5));       // "JavaScript Programming"

// substr(start, length) - deprecated, avoid
console.log(text.substr(0, 10));       // "JavaScript"
console.log(text.substr(11, 7));       // "Program"
```

### String Trimming

```javascript
let text = "   Hello World   ";

// trim() - remove whitespace from both ends
console.log(text.trim());              // "Hello World"

// trimStart() / trimLeft() - remove from start
console.log(text.trimStart());         // "Hello World   "

// trimEnd() / trimRight() - remove from end
console.log(text.trimEnd());           // "   Hello World"

// Practical use: user input
let userInput = "  john@email.com  ";
let cleanEmail = userInput.trim().toLowerCase();
console.log(cleanEmail);               // "john@email.com"
```

### Replacing Content

```javascript
let text = "I love JavaScript. JavaScript is great!";

// replace() - replaces first occurrence
console.log(text.replace("JavaScript", "Python"));
// "I love Python. JavaScript is great!"

// replaceAll() - replaces all occurrences (ES2021)
console.log(text.replaceAll("JavaScript", "Python"));
// "I love Python. Python is great!"

// Using regex for case-insensitive replace
console.log(text.replace(/javascript/gi, "Python"));
// "I love Python. Python is great!"

// Replace with function
let greeting = "Hello, NAME!";
let replaced = greeting.replace("NAME", () => "John");
console.log(replaced); // "Hello, John!"
```

### Splitting and Joining

```javascript
// split() - string to array
let csv = "apple,banana,orange";
let fruits = csv.split(",");
console.log(fruits);               // ["apple", "banana", "orange"]

let sentence = "Hello World";
let words = sentence.split(" ");
console.log(words);                // ["Hello", "World"]

// Split into characters
let str = "Hello";
let chars = str.split("");
console.log(chars);                // ["H", "e", "l", "l", "o"]

// Limit split
let limited = "a-b-c-d-e".split("-", 3);
console.log(limited);              // ["a", "b", "c"]

// Practical example: parsing CSV
let data = "John,30,New York";
let [name, age, city] = data.split(",");
console.log(name, age, city);      // John 30 New York
```

### Repeating and Padding

```javascript
// repeat() - repeat string n times
let str = "Ha";
console.log(str.repeat(3));        // "HaHaHa"
console.log("=".repeat(20));       // "===================="

// padStart() - pad from start
let num = "5";
console.log(num.padStart(3, "0")); // "005"
console.log(num.padStart(5, "*")); // "****5"

// padEnd() - pad from end
console.log(num.padEnd(3, "0"));   // "500"

// Practical use: formatting
let price = "19";
console.log(`$${price.padStart(6, " ")}`); // "$    19"
```

### Concatenation

```javascript
// concat() method
let str1 = "Hello";
let str2 = " World";
console.log(str1.concat(str2));    // "Hello World"
console.log(str1.concat(" ", "Beautiful", " ", "World"));
// "Hello Beautiful World"

// Using + operator (more common)
let combined = str1 + str2;
console.log(combined);             // "Hello World"

// Using template literals (modern)
let name = "John";
let greeting = `Hello ${name}`;
console.log(greeting);             // "Hello John"
```

---

## String Manipulation

### Common String Operations

```javascript
// Reverse a string
let str = "Hello";
let reversed = str.split("").reverse().join("");
console.log(reversed);              // "olleH"

// Count occurrences
let text = "JavaScript is great. JavaScript is fun!";
let count = (text.match(/JavaScript/g) || []).length;
console.log(count);                 // 2

// Remove all spaces
let withSpaces = "Hello World";
let noSpaces = withSpaces.replace(/\s/g, "");
console.log(noSpaces);              // "HelloWorld"

// Capitalize first letter
let word = "javascript";
let capitalized = word.charAt(0).toUpperCase() + word.slice(1);
console.log(capitalized);           // "Javascript"

// Title case
let title = "javascript programming";
let titleCase = title.split(" ")
  .map(word => word.charAt(0).toUpperCase() + word.slice(1))
  .join(" ");
console.log(titleCase);             // "Javascript Programming"
```

---

## Escape Characters

Special characters that need escaping in strings.

```javascript
// Backslash \\
let path = "C:\\Users\\John\\Documents";
console.log(path);                  // C:\Users\John\Documents

// Single quote \'
let quote1 = 'It\'s a beautiful day';
console.log(quote1);                // It's a beautiful day

// Double quote \"
let quote2 = "He said \"Hello\"";
console.log(quote2);                // He said "Hello"

// Newline \n
let multiline = "Line 1\nLine 2\nLine 3";
console.log(multiline);
// Line 1
// Line 2
// Line 3

// Tab \t
let tabbed = "Name:\tJohn\nAge:\t30";
console.log(tabbed);
// Name:	John
// Age:	30

// Carriage return \r
let cr = "Hello\rWorld";
console.log(cr);                    // World (overwrites Hello in some consoles)

// Unicode escape \uXXXX
let heart = "\u2764";
console.log(heart);                 // ❤

// Hex escape \xXX
let smiley = "\x3A\x29";
console.log(smiley);                // :)
```

---

## ⚠️ Common Mistakes

### 1. String Immutability

```javascript
// ❌ Wrong: Trying to modify string
let str = "Hello";
str[0] = "J";
console.log(str);                   // Still "Hello" (unchanged)

// ✓ Correct: Create new string
str = "J" + str.slice(1);
console.log(str);                   // "Jello"
```

### 2. Comparing Strings

```javascript
// ❌ Wrong: Case-sensitive comparison
let input = "JAVASCRIPT";
console.log(input === "javascript"); // false

// ✓ Correct: Convert to same case
console.log(input.toLowerCase() === "javascript"); // true
```

### 3. indexOf vs includes

```javascript
let str = "Hello World";

// ❌ Wrong: Using indexOf in boolean context
if (str.indexOf("World")) {          // 6 is truthy
  console.log("Found");              // This runs
}

if (str.indexOf("Hello")) {          // 0 is falsy!
  console.log("Found");              // This doesn't run!
}

// ✓ Correct: Check for -1 or use includes
if (str.indexOf("Hello") !== -1) {
  console.log("Found");              // ✓ Correct
}

if (str.includes("Hello")) {
  console.log("Found");              // ✓ Better
}
```

### 4. String vs Number Concatenation

```javascript
// ❌ Wrong: Unintended string concatenation
let result = "5" + 3;
console.log(result);                 // "53" (string)

// ✓ Correct: Convert to number first
let num1 = Number("5");
let num2 = 3;
console.log(num1 + num2);           // 8 (number)
```

---

## 💼 Interview Tips

### Q1: What's the difference between slice, substring, and substr?

**Answer:**
- **slice(start, end)**: Extracts from start to end (not included). Accepts negative indices.
- **substring(start, end)**: Similar to slice, but negative values treated as 0. Swaps arguments if start > end.
- **substr(start, length)**: Extracts 'length' characters from start. Deprecated.

```javascript
let str = "JavaScript";
console.log(str.slice(0, 4));       // "Java"
console.log(str.slice(-6));         // "Script"
console.log(str.substring(0, 4));   // "Java"
console.log(str.substring(-5));     // "JavaScript" (treats -5 as 0)
console.log(str.substr(0, 4));      // "Java" (deprecated)
```

### Q2: How do you reverse a string in JavaScript?

**Answer:**
```javascript
let str = "Hello";

// Method 1: Using array methods
let reversed1 = str.split("").reverse().join("");

// Method 2: Using loop
let reversed2 = "";
for (let i = str.length - 1; i >= 0; i--) {
  reversed2 += str[i];
}

// Method 3: Using spread operator
let reversed3 = [...str].reverse().join("");

console.log(reversed1); // "olleH"
```

### Q3: What are template literals and their benefits?

**Answer:**
Template literals (backticks) provide:
1. String interpolation with `${expression}`
2. Multiline strings without \n
3. Tagged templates for custom processing
4. Better readability

```javascript
let name = "John";
let age = 30;

// Old way
let old = "Name: " + name + ", Age: " + age;

// New way
let modern = `Name: ${name}, Age: ${age}`;

// Multiline
let multiline = `
  Line 1
  Line 2
`;
```

### Q4: How do you check if a string contains a substring?

**Answer:**
Multiple methods:
```javascript
let str = "JavaScript Programming";

// Method 1: includes() - modern, returns boolean
console.log(str.includes("Java"));          // true

// Method 2: indexOf() - older, returns index or -1
console.log(str.indexOf("Java") !== -1);    // true

// Method 3: search() - with regex support
console.log(str.search("Java") !== -1);     // true

// Method 4: match() - for regex patterns
console.log(str.match(/Java/) !== null);    // true

// Method 5: startsWith() / endsWith()
console.log(str.startsWith("Java"));        // true
console.log(str.endsWith("ming"));          // true
```

### Q5: Are strings mutable or immutable in JavaScript?

**Answer:**
Strings are **immutable** in JavaScript. You cannot change individual characters. String methods always return new strings.

```javascript
let str = "Hello";
str[0] = "J";           // Doesn't work
console.log(str);       // Still "Hello"

// Must create new string
str = "J" + str.slice(1);
console.log(str);       // "Jello"
```

---

## Practice Exercises

### Exercise 1: String Manipulation
Write a function that takes a string and returns it with the first letter capitalized and the rest lowercase.

```javascript
function capitalizeFirst(str) {
  // Your code here
}

console.log(capitalizeFirst("javaScript"));  // "Javascript"
console.log(capitalizeFirst("HELLO"));       // "Hello"
```

<details>
<summary>Solution</summary>

```javascript
function capitalizeFirst(str) {
  if (!str) return "";
  return str.charAt(0).toUpperCase() + str.slice(1).toLowerCase();
}

// Alternative using destructuring
function capitalizeFirst2(str) {
  if (!str) return "";
  const [first, ...rest] = str;
  return first.toUpperCase() + rest.join("").toLowerCase();
}
```
</details>

### Exercise 2: Count Vowels
Write a function that counts the number of vowels in a string.

```javascript
function countVowels(str) {
  // Your code here
}

console.log(countVowels("Hello World"));     // 3
console.log(countVowels("JavaScript"));      // 3
```

<details>
<summary>Solution</summary>

```javascript
function countVowels(str) {
  const vowels = "aeiouAEIOU";
  let count = 0;
  
  for (let char of str) {
    if (vowels.includes(char)) {
      count++;
    }
  }
  
  return count;
}

// Alternative using regex
function countVowels2(str) {
  const matches = str.match(/[aeiou]/gi);
  return matches ? matches.length : 0;
}
```
</details>

### Exercise 3: Palindrome Check
Write a function to check if a string is a palindrome (reads same forwards and backwards).

```javascript
function isPalindrome(str) {
  // Your code here
}

console.log(isPalindrome("racecar"));        // true
console.log(isPalindrome("hello"));          // false
console.log(isPalindrome("A man a plan a canal Panama")); // true (ignore spaces/case)
```

<details>
<summary>Solution</summary>

```javascript
function isPalindrome(str) {
  // Remove non-alphanumeric and convert to lowercase
  const cleaned = str.toLowerCase().replace(/[^a-z0-9]/g, "");
  const reversed = cleaned.split("").reverse().join("");
  return cleaned === reversed;
}

// Alternative: two-pointer approach
function isPalindrome2(str) {
  const cleaned = str.toLowerCase().replace(/[^a-z0-9]/g, "");
  let left = 0;
  let right = cleaned.length - 1;
  
  while (left < right) {
    if (cleaned[left] !== cleaned[right]) {
      return false;
    }
    left++;
    right--;
  }
  
  return true;
}
```
</details>

### Exercise 4: URL Slug Generator
Create a function that converts a title into a URL-friendly slug.

```javascript
function createSlug(title) {
  // Your code here
}

console.log(createSlug("JavaScript Programming Tips"));
// "javascript-programming-tips"

console.log(createSlug("10 Ways to Learn JS!"));
// "10-ways-to-learn-js"
```

<details>
<summary>Solution</summary>

```javascript
function createSlug(title) {
  return title
    .toLowerCase()
    .trim()
    .replace(/[^a-z0-9\s-]/g, "")  // Remove special chars
    .replace(/\s+/g, "-")           // Replace spaces with -
    .replace(/-+/g, "-");           // Replace multiple - with single -
}
```
</details>

---

**[← Back: Operators](./03-operators.md)** | **[Next: Numbers and Math →](./05-numbers-and-math.md)**

---

**Made with ❤️ for JavaScript learners**
