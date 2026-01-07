# 🔧 Object Methods in JavaScript

## 📑 Table of Contents
- [Object.keys()](#objectkeys)
- [Object.values()](#objectvalues)
- [Object.entries()](#objectentries)
- [Object.assign()](#objectassign)
- [Object.freeze()](#objectfreeze)
- [Object.seal()](#objectseal)
- [Object Methods Reference](#object-methods-reference)
- [Spread Operator](#spread-operator)
- [Common Mistakes](#-common-mistakes)
- [Interview Tips](#-interview-tips)
- [Practice Exercises](#practice-exercises)

---

## Object.keys()

Returns an array of object's own property names.

```javascript
let person = {
  name: "John",
  age: 30,
  city: "New York"
};

let keys = Object.keys(person);
console.log(keys);  // ["name", "age", "city"]

// Iterate over keys
Object.keys(person).forEach(key => {
  console.log(`${key}: ${person[key]}`);
});
// name: John
// age: 30
// city: New York

// Count properties
console.log(Object.keys(person).length);  // 3
```

---

## Object.values()

Returns an array of object's own property values.

```javascript
let person = {
  name: "John",
  age: 30,
  city: "New York"
};

let values = Object.values(person);
console.log(values);  // ["John", 30, "New York"]

// Sum numeric values
let scores = {math: 90, english: 85, science: 95};
let total = Object.values(scores).reduce((sum, score) => sum + score, 0);
console.log(total);  // 270
```

---

## Object.entries()

Returns an array of [key, value] pairs.

```javascript
let person = {
  name: "John",
  age: 30,
  city: "New York"
};

let entries = Object.entries(person);
console.log(entries);
// [["name", "John"], ["age", 30], ["city", "New York"]]

// Iterate with destructuring
Object.entries(person).forEach(([key, value]) => {
  console.log(`${key}: ${value}`);
});

// Convert to Map
let map = new Map(Object.entries(person));
console.log(map.get("name"));  // "John"

// Filter and reconstruct object
let filtered = Object.fromEntries(
  Object.entries(person).filter(([key, value]) => typeof value === "string")
);
console.log(filtered);  // {name: "John", city: "New York"}
```

---

## Object.assign()

Copies properties from source objects to target object.

```javascript
let target = {a: 1, b: 2};
let source = {b: 3, c: 4};

Object.assign(target, source);
console.log(target);  // {a: 1, b: 3, c: 4}

// Clone object (shallow)
let original = {x: 1, y: 2};
let clone = Object.assign({}, original);
console.log(clone);  // {x: 1, y: 2}

// Merge multiple objects
let obj1 = {a: 1};
let obj2 = {b: 2};
let obj3 = {c: 3};
let merged = Object.assign({}, obj1, obj2, obj3);
console.log(merged);  // {a: 1, b: 2, c: 3}

// Default options pattern
function createConfig(options) {
  let defaults = {
    timeout: 5000,
    retries: 3,
    verbose: false
  };
  return Object.assign({}, defaults, options);
}

console.log(createConfig({timeout: 10000}));
// {timeout: 10000, retries: 3, verbose: false}
```

---

## Object.freeze()

Makes object immutable (cannot add, delete, or modify properties).

```javascript
let person = {
  name: "John",
  age: 30
};

Object.freeze(person);

// Try to modify
person.age = 31;           // Silently fails (throws error in strict mode)
person.city = "New York";  // Silently fails
delete person.name;        // Silently fails

console.log(person);       // {name: "John", age: 30} (unchanged)

// Check if frozen
console.log(Object.isFrozen(person));  // true

// Note: Shallow freeze (nested objects not frozen)
let user = {
  name: "John",
  address: {city: "NY"}
};
Object.freeze(user);
user.address.city = "LA";  // Works! (nested object not frozen)
console.log(user.address.city);  // "LA"

// Deep freeze function
function deepFreeze(obj) {
  Object.freeze(obj);
  Object.keys(obj).forEach(key => {
    if (typeof obj[key] === 'object' && obj[key] !== null) {
      deepFreeze(obj[key]);
    }
  });
  return obj;
}
```

---

## Object.seal()

Prevents adding/deleting properties, but allows modifying existing ones.

```javascript
let person = {
  name: "John",
  age: 30
};

Object.seal(person);

// Can modify
person.age = 31;
console.log(person.age);   // 31 ✓

// Cannot add
person.city = "New York";
console.log(person.city);  // undefined

// Cannot delete
delete person.name;
console.log(person.name);  // "John"

// Check if sealed
console.log(Object.isSealed(person));  // true
```

---

## Object Methods Reference

### Object.fromEntries()

Creates object from key-value pairs.

```javascript
let entries = [["name", "John"], ["age", 30]];
let obj = Object.fromEntries(entries);
console.log(obj);  // {name: "John", age: 30}

// From Map
let map = new Map([["a", 1], ["b", 2]]);
let obj2 = Object.fromEntries(map);
console.log(obj2);  // {a: 1, b: 2}

// Transform object
let prices = {apple: 10, banana: 5, orange: 8};
let discounted = Object.fromEntries(
  Object.entries(prices).map(([fruit, price]) => [fruit, price * 0.9])
);
console.log(discounted);  // {apple: 9, banana: 4.5, orange: 7.2}
```

### Object.getOwnPropertyNames()

Returns all property names (including non-enumerable).

```javascript
let obj = {a: 1, b: 2};
Object.defineProperty(obj, 'c', {
  value: 3,
  enumerable: false
});

console.log(Object.keys(obj));  // ["a", "b"]
console.log(Object.getOwnPropertyNames(obj));  // ["a", "b", "c"]
```

### Object.hasOwn() / Object.hasOwnProperty()

Checks if object has own property.

```javascript
let obj = {name: "John"};

console.log(Object.hasOwn(obj, "name"));  // true (ES2022)
console.log(obj.hasOwnProperty("name"));  // true
console.log("name" in obj);               // true

// Inherited properties
console.log(Object.hasOwn(obj, "toString"));  // false
console.log("toString" in obj);               // true (inherited)
```

### Object.is()

Compares two values for strict equality.

```javascript
console.log(Object.is(25, 25));     // true
console.log(Object.is('foo', 'foo'));  // true
console.log(Object.is(NaN, NaN));   // true (unlike ===)
console.log(Object.is(0, -0));      // false (unlike ===)
console.log(Object.is(+0, -0));     // false

// Compare with ===
console.log(NaN === NaN);           // false
console.log(Object.is(NaN, NaN));   // true
```

---

## Spread Operator

### Clone Object

```javascript
let original = {a: 1, b: 2, c: 3};
let clone = {...original};
console.log(clone);  // {a: 1, b: 2, c: 3}

// Shallow clone
let obj = {x: 1, nested: {y: 2}};
let copy = {...obj};
copy.nested.y = 3;
console.log(obj.nested.y);  // 3 (affected!)
```

### Merge Objects

```javascript
let obj1 = {a: 1, b: 2};
let obj2 = {c: 3, d: 4};
let merged = {...obj1, ...obj2};
console.log(merged);  // {a: 1, b: 2, c: 3, d: 4}

// Override properties
let defaults = {theme: 'light', lang: 'en'};
let custom = {theme: 'dark'};
let config = {...defaults, ...custom};
console.log(config);  // {theme: 'dark', lang: 'en'}
```

### Add/Update Properties

```javascript
let user = {name: "John", age: 30};

// Add property
let updated = {...user, city: "New York"};
console.log(updated);  // {name: "John", age: 30, city: "New York"}

// Update property
let modified = {...user, age: 31};
console.log(modified);  // {name: "John", age: 31}
```

---

## ⚠️ Common Mistakes

### 1. Object.assign() is Shallow

```javascript
let obj = {a: 1, nested: {b: 2}};
let copy = Object.assign({}, obj);

copy.nested.b = 3;
console.log(obj.nested.b);  // 3 (affected!)
```

### 2. freeze() is Shallow

```javascript
let obj = {x: 1, nested: {y: 2}};
Object.freeze(obj);

obj.nested.y = 3;  // Works! (nested not frozen)
console.log(obj.nested.y);  // 3
```

### 3. Iterating Over Properties

```javascript
let obj = {a: 1, b: 2};
Object.prototype.inherited = 3;

// ❌ Wrong: includes inherited
for (let key in obj) {
  console.log(key);  // a, b, inherited
}

// ✓ Correct: own properties only
for (let key in obj) {
  if (obj.hasOwnProperty(key)) {
    console.log(key);  // a, b
  }
}

// ✓ Better: Object.keys()
Object.keys(obj).forEach(key => {
  console.log(key);  // a, b
});
```

---

## 💼 Interview Tips

### Q1: What's the difference between Object.freeze() and Object.seal()?

**Answer:**
- **freeze()**: Cannot add, delete, or modify properties (fully immutable)
- **seal()**: Cannot add or delete, but can modify existing properties

```javascript
let frozen = {a: 1};
Object.freeze(frozen);
frozen.a = 2;  // Doesn't work
console.log(frozen.a);  // 1

let sealed = {a: 1};
Object.seal(sealed);
sealed.a = 2;  // Works!
console.log(sealed.a);  // 2
```

### Q2: How do you clone an object in JavaScript?

**Answer:**
```javascript
// Shallow clones
let obj = {a: 1, b: 2};
let clone1 = {...obj};
let clone2 = Object.assign({}, obj);
let clone3 = JSON.parse(JSON.stringify(obj));  // Deep but has limitations

// Deep clone (structuredClone - modern browsers)
let deep = structuredClone(obj);
```

### Q3: What's the difference between Object.keys() and for...in?

**Answer:**
- **Object.keys()**: Returns array of own enumerable properties
- **for...in**: Iterates over own and inherited enumerable properties

```javascript
let obj = {a: 1};
Object.prototype.inherited = 2;

console.log(Object.keys(obj));  // ["a"]

for (let key in obj) {
  console.log(key);  // "a", "inherited"
}
```

---

## Practice Exercises

### Exercise 1: Invert Object
Swap keys and values.

```javascript
function invertObject(obj) {
  // Your code here
}

console.log(invertObject({a: 1, b: 2, c: 3}));
// {1: 'a', 2: 'b', 3: 'c'}
```

<details>
<summary>Solution</summary>

```javascript
function invertObject(obj) {
  return Object.fromEntries(
    Object.entries(obj).map(([key, value]) => [value, key])
  );
}
```
</details>

### Exercise 2: Pick Properties
Create new object with only specified properties.

```javascript
function pick(obj, keys) {
  // Your code here
}

let user = {name: "John", age: 30, city: "NY", country: "USA"};
console.log(pick(user, ["name", "age"]));
// {name: "John", age: 30}
```

<details>
<summary>Solution</summary>

```javascript
function pick(obj, keys) {
  return Object.fromEntries(
    Object.entries(obj).filter(([key]) => keys.includes(key))
  );
}
```
</details>

---

**[← Back: Objects](./03-objects.md)** | **[Next: Functions →](../03-functions/01-function-basics.md)**

---

**Made with ❤️ for JavaScript learners**
