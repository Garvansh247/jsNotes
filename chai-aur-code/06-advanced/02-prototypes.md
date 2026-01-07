# 🧬 Prototypes in JavaScript

## 📑 Table of Contents
- [What is a Prototype?](#what-is-a-prototype)
- [Prototype Chain](#prototype-chain)
- [__proto__ vs prototype](#__proto__-vs-prototype)
- [Prototypal Inheritance](#prototypal-inheritance)
- [Common Mistakes](#-common-mistakes)
- [Interview Tips](#-interview-tips)

---

## What is a Prototype?

Every JavaScript object has a prototype. A prototype is also an object from which other objects inherit properties and methods.

```javascript
const obj = {};
console.log(obj.__proto__);  // Object.prototype
console.log(obj.toString);   // Inherited from Object.prototype

const arr = [];
console.log(arr.__proto__);  // Array.prototype
console.log(arr.push);       // Inherited from Array.prototype
```

---

## Prototype Chain

```javascript
const arr = [1, 2, 3];

// Prototype chain:
// arr -> Array.prototype -> Object.prototype -> null

console.log(arr.toString());  // From Object.prototype
console.log(arr.push);        // From Array.prototype

// Check prototype
console.log(Object.getPrototypeOf(arr) === Array.prototype);  // true
console.log(Object.getPrototypeOf(Array.prototype) === Object.prototype);  // true
```

---

## __proto__ vs prototype

```javascript
function Person(name) {
  this.name = name;
}

// prototype: Property of constructor function
console.log(Person.prototype);  // Object with constructor

// __proto__: Link to prototype
const john = new Person('John');
console.log(john.__proto__ === Person.prototype);  // true

// Add method to prototype
Person.prototype.greet = function() {
  return `Hello, I'm ${this.name}`;
};

console.log(john.greet());  // 'Hello, I'm John'
```

---

## Prototypal Inheritance

```javascript
function Animal(name) {
  this.name = name;
}

Animal.prototype.eat = function() {
  return `${this.name} is eating`;
};

function Dog(name, breed) {
  Animal.call(this, name);  // Call parent constructor
  this.breed = breed;
}

// Set up inheritance
Dog.prototype = Object.create(Animal.prototype);
Dog.prototype.constructor = Dog;

Dog.prototype.bark = function() {
  return 'Woof!';
};

const dog = new Dog('Max', 'Labrador');
console.log(dog.eat());   // 'Max is eating'
console.log(dog.bark());  // 'Woof!'
```

---

## ⚠️ Common Mistakes

```javascript
// ❌ Modifying Object.prototype (dangerous!)
Object.prototype.myMethod = function() {};
// Now ALL objects have this method

// ❌ Incorrect inheritance
Dog.prototype = Animal.prototype;  // Both share same prototype!

// ✓ Correct inheritance
Dog.prototype = Object.create(Animal.prototype);
Dog.prototype.constructor = Dog;
```

---

## 💼 Interview Tips

### Q1: What is prototypal inheritance?

**Answer:**
Objects inherit properties and methods from their prototype, creating a prototype chain.

### Q2: How do you check if an object has a property (not inherited)?

**Answer:**
```javascript
obj.hasOwnProperty('prop');
```

### Q3: What's the difference between __proto__ and prototype?

**Answer:**
- `__proto__`: Link to prototype (on instances)
- `prototype`: Property of constructor function

---

**[← Back: Closures](./01-closures.md)** | **[Next: Classes and OOP →](./03-classes-and-oop.md)**

---

**Made with ❤️ for JavaScript learners**
