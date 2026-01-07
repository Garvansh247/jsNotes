# 🔷 Objects in JavaScript

## 📑 Table of Contents
- [Object Basics](#object-basics)
- [Creating Objects](#creating-objects)
- [Accessing Properties](#accessing-properties)
- [Modifying Objects](#modifying-objects)
- [Nested Objects](#nested-objects)
- [Object Destructuring](#object-destructuring)
- [Object References](#object-references)
- [Common Mistakes](#-common-mistakes)
- [Interview Tips](#-interview-tips)
- [Practice Exercises](#practice-exercises)

---

## Object Basics

Objects are collections of key-value pairs. They are the fundamental building blocks in JavaScript.

```javascript
//Simple object
let person = {
  name: "John",
  age: 30,
  city: "New York"
};

console.log(person);  // {name: "John", age: 30, city: "New York"}
console.log(typeof person);  // "object"
```

---

## Creating Objects

### Object Literal (Most Common)

```javascript
// Empty object
let emptyObj = {};

// Object with properties
let user = {
  name: "John",
  age: 30,
  email: "john@example.com",
  isActive: true
};

// Property names can be strings
let obj = {
  "first name": "John",  // Space in key requires quotes
  "last-name": "Doe"     // Hyphen requires quotes
};

// Computed property names (ES6)
let propName = "age";
let person = {
  name: "John",
  [propName]: 30,        // age: 30
  ["is" + "Active"]: true  // isActive: true
};
```

### Object Constructor

```javascript
// Using new Object()
let person = new Object();
person.name = "John";
person.age = 30;

// Equivalent to object literal
let person2 = {
  name: "John",
  age: 30
};
```

### Object.create()

```javascript
// Create object with specific prototype
let personProto = {
  greet() {
    return `Hello, I'm ${this.name}`;
  }
};

let person = Object.create(personProto);
person.name = "John";
console.log(person.greet());  // "Hello, I'm John"

// Create object with null prototype (no inherited properties)
let pureObj = Object.create(null);
pureObj.name = "John";
console.log(pureObj.toString);  // undefined (no inherited methods)
```

### Constructor Function

```javascript
function Person(name, age) {
  this.name = name;
  this.age = age;
  this.greet = function() {
    return `Hello, I'm ${this.name}`;
  };
}

let person1 = new Person("John", 30);
let person2 = new Person("Jane", 25);

console.log(person1.name);     // "John"
console.log(person2.greet());  // "Hello, I'm Jane"
```

### Class Syntax (ES6)

```javascript
class Person {
  constructor(name, age) {
    this.name = name;
    this.age = age;
  }
  
  greet() {
    return `Hello, I'm ${this.name}`;
  }
}

let person = new Person("John", 30);
console.log(person.greet());  // "Hello, I'm John"
```

---

## Accessing Properties

### Dot Notation

```javascript
let person = {
  name: "John",
  age: 30,
  city: "New York"
};

console.log(person.name);   // "John"
console.log(person.age);    // 30
console.log(person.city);   // "New York"

// Accessing non-existent property
console.log(person.salary); // undefined
```

### Bracket Notation

```javascript
let person = {
  name: "John",
  age: 30,
  "first name": "John",  // Key with space
  "last-name": "Doe"     // Key with hyphen
};

console.log(person["name"]);        // "John"
console.log(person["age"]);         // 30
console.log(person["first name"]);  // "John"
console.log(person["last-name"]);   // "Doe"

// Dynamic property access
let prop = "age";
console.log(person[prop]);          // 30

// Computed keys
let key = "city";
person[key] = "New York";
console.log(person.city);           // "New York"
```

### Optional Chaining (?.)

```javascript
let user = {
  name: "John",
  address: {
    city: "New York"
  }
};

// Without optional chaining
console.log(user.address.city);           // "New York"
// console.log(user.profile.bio);        // Error: Cannot read property 'bio' of undefined

// With optional chaining (ES2020)
console.log(user.profile?.bio);           // undefined (no error)
console.log(user.address?.city);          // "New York"
console.log(user.address?.country?.name); // undefined

// With methods
console.log(user.greet?.());              // undefined (method doesn't exist)

// With arrays
console.log(user.hobbies?.[0]);           // undefined
```

---

## Modifying Objects

### Adding Properties

```javascript
let person = {
  name: "John"
};

// Add property using dot notation
person.age = 30;

// Add property using bracket notation
person["city"] = "New York";

// Add method
person.greet = function() {
  return `Hello, I'm ${this.name}`;
};

console.log(person);
// {name: "John", age: 30, city: "New York", greet: ƒ}
```

### Updating Properties

```javascript
let person = {
  name: "John",
  age: 30
};

person.age = 31;           // Update using dot notation
person["name"] = "Johnny"; // Update using bracket notation

console.log(person);       // {name: "Johnny", age: 31}
```

### Deleting Properties

```javascript
let person = {
  name: "John",
  age: 30,
  city: "New York"
};

delete person.age;
console.log(person);       // {name: "John", city: "New York"}

delete person["city"];
console.log(person);       // {name: "John"}

// delete returns true if successful
let result = delete person.name;
console.log(result);       // true
console.log(person);       // {}
```

### Property Existence Check

```javascript
let person = {
  name: "John",
  age: 30,
  salary: undefined
};

// Using in operator
console.log("name" in person);     // true
console.log("email" in person);    // false
console.log("salary" in person);   // true (even though undefined)

// Using hasOwnProperty()
console.log(person.hasOwnProperty("name"));  // true
console.log(person.hasOwnProperty("email")); // false

// Checking for undefined (not always reliable)
console.log(person.name !== undefined);      // true
console.log(person.salary !== undefined);    // false (property exists but is undefined!)
```

---

## Nested Objects

### Creating Nested Objects

```javascript
let user = {
  name: "John",
  age: 30,
  address: {
    street: "123 Main St",
    city: "New York",
    country: "USA",
    zip: {
      code: "10001",
      ext: "1234"
    }
  },
  hobbies: ["reading", "coding", "gaming"]
};

// Access nested properties
console.log(user.address.city);           // "New York"
console.log(user.address.zip.code);       // "10001"
console.log(user.hobbies[0]);             // "reading"
```

### Modifying Nested Objects

```javascript
let user = {
  name: "John",
  address: {
    city: "New York"
  }
};

// Update nested property
user.address.city = "Los Angeles";

// Add nested property
user.address.country = "USA";

// Add nested object
user.contact = {
  email: "john@example.com",
  phone: "123-456-7890"
};

console.log(user);
```

### Deep Copy vs Shallow Copy

```javascript
let original = {
  name: "John",
  address: {
    city: "New York"
  }
};

// Shallow copy (only top level)
let shallow = {...original};
shallow.address.city = "LA";
console.log(original.address.city);  // "LA" (affected!)

// Deep copy
let deep = JSON.parse(JSON.stringify(original));
deep.address.city = "Chicago";
console.log(original.address.city);  // "LA" (not affected)

// Note: JSON method has limitations (functions, dates, etc.)
```

---

## Object Destructuring

### Basic Destructuring

```javascript
let person = {
  name: "John",
  age: 30,
  city: "New York"
};

// Traditional way
let name = person.name;
let age = person.age;

// Destructuring (ES6)
let {name, age, city} = person;
console.log(name, age, city);  // "John" 30 "New York"

// Select specific properties
let {name, city} = person;
console.log(name, city);       // "John" "New York"
```

### Renaming Variables

```javascript
let person = {
  name: "John",
  age: 30
};

// Rename during destructuring
let {name: personName, age: personAge} = person;
console.log(personName);       // "John"
console.log(personAge);        // 30
```

### Default Values

```javascript
let person = {
  name: "John"
};

// With default values
let {name, age = 25, city = "Unknown"} = person;
console.log(name);             // "John"
console.log(age);              // 25 (default)
console.log(city);             // "Unknown" (default)
```

### Nested Destructuring

```javascript
let user = {
  name: "John",
  address: {
    city: "New York",
    country: "USA"
  }
};

// Destructure nested object
let {address: {city, country}} = user;
console.log(city, country);    // "New York" "USA"

// With renaming
let {address: {city: userCity}} = user;
console.log(userCity);         // "New York"
```

### Rest in Destructuring

```javascript
let person = {
  name: "John",
  age: 30,
  city: "New York",
  country: "USA"
};

// Rest of properties
let {name, age, ...rest} = person;
console.log(name, age);        // "John" 30
console.log(rest);             // {city: "New York", country: "USA"}
```

### Function Parameters

```javascript
// Destructuring in function parameters
function greet({name, age}) {
  return `Hello ${name}, you are ${age} years old`;
}

let person = {name: "John", age: 30};
console.log(greet(person));    // "Hello John, you are 30 years old"

// With defaults
function introduce({name = "Guest", age = 0} = {}) {
  return `${name} is ${age} years old`;
}

console.log(introduce({name: "John", age: 30}));  // "John is 30 years old"
console.log(introduce({name: "Jane"}));           // "Jane is 0 years old"
console.log(introduce());                         // "Guest is 0 years old"
```

---

## Object References

### Pass by Reference

```javascript
let obj1 = {name: "John"};
let obj2 = obj1;  // Reference, not copy!

obj2.name = "Jane";
console.log(obj1.name);  // "Jane" (affected!)
console.log(obj1 === obj2);  // true (same reference)

// Create actual copy
let obj3 = {...obj1};  // Shallow copy
obj3.name = "Bob";
console.log(obj1.name);  // "Jane" (not affected)
console.log(obj1 === obj3);  // false (different references)
```

### Comparing Objects

```javascript
let obj1 = {name: "John"};
let obj2 = {name: "John"};
let obj3 = obj1;

// Comparison by reference
console.log(obj1 == obj2);   // false (different objects)
console.log(obj1 === obj2);  // false (different objects)
console.log(obj1 === obj3);  // true (same reference)

// Compare values (manual)
function isEqual(obj1, obj2) {
  return JSON.stringify(obj1) === JSON.stringify(obj2);
}
console.log(isEqual(obj1, obj2));  // true
```

---

## ⚠️ Common Mistakes

### 1. Mutating Objects Unintentionally

```javascript
let original = {name: "John", age: 30};

// ❌ Wrong: Creates reference, not copy
let copy = original;
copy.age = 31;
console.log(original.age);  // 31 (affected!)

// ✓ Correct: Create actual copy
let copy2 = {...original};
copy2.age = 32;
console.log(original.age);  // 31 (not affected)
```

### 2. Property Names with Special Characters

```javascript
// ❌ Wrong: Can't use dot notation
let obj = {
  first-name: "John"  // SyntaxError
};

// ✓ Correct: Use quotes and bracket notation
let obj2 = {
  "first-name": "John"
};
console.log(obj2["first-name"]);  // "John"
```

### 3. Deleting vs Setting to undefined

```javascript
let obj = {a: 1, b: 2, c: 3};

// Setting to undefined
obj.b = undefined;
console.log("b" in obj);     // true (property exists)
console.log(obj.b);          // undefined

// Deleting property
delete obj.c;
console.log("c" in obj);     // false (property doesn't exist)
console.log(obj.c);          // undefined
```

---

## 💼 Interview Tips

### Q1: What are the ways to create an object?

**Answer:**
1. Object literal: `let obj = {}`
2. Object constructor: `let obj = new Object()`
3. Object.create(): `let obj = Object.create(proto)`
4. Constructor function: `function Obj() {}; let obj = new Obj()`
5. Class syntax: `class Obj {}; let obj = new Obj()`

### Q2: What's the difference between dot and bracket notation?

**Answer:**
- **Dot notation**: Cleaner, but property name must be valid identifier
- **Bracket notation**: Works with any string, allows dynamic property access

```javascript
let obj = {"first-name": "John"};
// obj.first-name  // ❌ Error
obj["first-name"]  // ✓ Works

let prop = "age";
obj[prop] = 30;    // ✓ Dynamic access
```

### Q3: How do you check if a property exists?

**Answer:**
```javascript
let obj = {name: "John", age: undefined};

// Method 1: in operator
console.log("name" in obj);  // true

// Method 2: hasOwnProperty
console.log(obj.hasOwnProperty("name"));  // true

// Method 3: !== undefined (not reliable)
console.log(obj.age !== undefined);  // false (but property exists!)
```

### Q4: What's the difference between shallow and deep copy?

**Answer:**
- **Shallow copy**: Copies only top-level properties, nested objects are still referenced
- **Deep copy**: Recursively copies all levels

```javascript
let obj = {name: "John", address: {city: "NY"}};

// Shallow
let shallow = {...obj};
shallow.address.city = "LA";
console.log(obj.address.city);  // "LA" (affected!)

// Deep
let deep = JSON.parse(JSON.stringify(obj));
deep.address.city = "SF";
console.log(obj.address.city);  // "LA" (not affected)
```

---

## Practice Exercises

### Exercise 1: Merge Objects
Write a function to deeply merge two objects.

```javascript
function mergeObjects(obj1, obj2) {
  // Your code here
}

let a = {x: 1, y: {z: 2}};
let b = {y: {w: 3}, p: 4};
console.log(mergeObjects(a, b));
// {x: 1, y: {z: 2, w: 3}, p: 4}
```

<details>
<summary>Solution</summary>

```javascript
function mergeObjects(obj1, obj2) {
  let result = {...obj1};
  
  for (let key in obj2) {
    if (obj2.hasOwnProperty(key)) {
      if (typeof obj2[key] === 'object' && !Array.isArray(obj2[key])) {
        result[key] = mergeObjects(result[key] || {}, obj2[key]);
      } else {
        result[key] = obj2[key];
      }
    }
  }
  
  return result;
}
```
</details>

### Exercise 2: Get Nested Property
Write a function to safely get nested property value.

```javascript
function getNestedProperty(obj, path) {
  // Your code here
  // path: "address.city.name"
}

let user = {address: {city: {name: "NY"}}};
console.log(getNestedProperty(user, "address.city.name"));  // "NY"
console.log(getNestedProperty(user, "address.country"));     // undefined
```

<details>
<summary>Solution</summary>

```javascript
function getNestedProperty(obj, path) {
  return path.split('.').reduce((current, key) => {
    return current?.[key];
  }, obj);
}
```
</details>

---

**[← Back: Array Methods](./02-array-methods.md)** | **[Next: Object Methods →](./04-object-methods.md)**

---

**Made with ❤️ for JavaScript learners**
