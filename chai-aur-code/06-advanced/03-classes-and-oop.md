# 🏗️ Classes and OOP in JavaScript

## 📑 Table of Contents
- [Class Syntax](#class-syntax)
- [Constructor](#constructor)
- [Methods](#methods)
- [Inheritance](#inheritance)
- [Static Methods](#static-methods)
- [Private Fields](#private-fields)
- [Common Mistakes](#-common-mistakes)
- [Interview Tips](#-interview-tips)

---

## Class Syntax

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

const john = new Person('John', 30);
console.log(john.greet());  // 'Hello, I'm John'
```

---

## Constructor

```javascript
class User {
  constructor(username, email) {
    this.username = username;
    this.email = email;
    this.created = new Date();
  }
  
  getInfo() {
    return `${this.username} (${this.email})`;
  }
}

const user = new User('john', 'john@example.com');
```

---

## Methods

```javascript
class Calculator {
  constructor() {
    this.result = 0;
  }
  
  add(x) {
    this.result += x;
    return this;  // Method chaining
  }
  
  subtract(x) {
    this.result -= x;
    return this;
  }
  
  getResult() {
    return this.result;
  }
}

const calc = new Calculator();
calc.add(5).add(3).subtract(2);
console.log(calc.getResult());  // 6
```

---

## Inheritance

```javascript
class Animal {
  constructor(name) {
    this.name = name;
  }
  
  eat() {
    return `${this.name} is eating`;
  }
}

class Dog extends Animal {
  constructor(name, breed) {
    super(name);  // Call parent constructor
    this.breed = breed;
  }
  
  bark() {
    return 'Woof!';
  }
}

const dog = new Dog('Max', 'Labrador');
console.log(dog.eat());   // 'Max is eating'
console.log(dog.bark());  // 'Woof!'
```

---

## Static Methods

```javascript
class MathUtils {
  static add(a, b) {
    return a + b;
  }
  
  static multiply(a, b) {
    return a * b;
  }
}

// Call on class, not instance
console.log(MathUtils.add(5, 3));      // 8
console.log(MathUtils.multiply(5, 3)); // 15

// const utils = new MathUtils();
// utils.add(5, 3);  // Error
```

---

## Private Fields

```javascript
class BankAccount {
  #balance = 0;  // Private field
  
  constructor(initialBalance) {
    this.#balance = initialBalance;
  }
  
  deposit(amount) {
    this.#balance += amount;
  }
  
  getBalance() {
    return this.#balance;
  }
}

const account = new BankAccount(100);
account.deposit(50);
console.log(account.getBalance());  // 150
// console.log(account.#balance);   // SyntaxError
```

---

## ⚠️ Common Mistakes

```javascript
// ❌ Forgetting 'new'
const person = Person('John');  // undefined or error

// ✓ Use 'new'
const person = new Person('John');

// ❌ Forgetting 'super' in child constructor
class Dog extends Animal {
  constructor(name, breed) {
    // super(name);  // Must call super first!
    this.breed = breed;  // ReferenceError
  }
}
```

---

## 💼 Interview Tips

### Q1: What's the difference between a class and a constructor function?

**Answer:**
Classes are syntactic sugar over constructor functions. They provide cleaner syntax but work similarly under the hood.

### Q2: What is the 'super' keyword?

**Answer:**
`super` calls the parent class constructor or methods.

```javascript
class Child extends Parent {
  constructor() {
    super();  // Call parent constructor
  }
  
  method() {
    super.parentMethod();  // Call parent method
  }
}
```

---

**[← Back: Prototypes](./02-prototypes.md)** | **[Next: Execution Context →](./04-execution-context.md)**

---

**Made with ❤️ for JavaScript learners**
