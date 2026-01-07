# 🌳 DOM Basics in JavaScript

## 📑 Table of Contents
- [What is the DOM?](#what-is-the-dom)
- [DOM Tree Structure](#dom-tree-structure)
- [Document Object](#document-object)
- [Window vs Document](#window-vs-document)
- [Node Types](#node-types)
- [Common Mistakes](#-common-mistakes)
- [Interview Tips](#-interview-tips)

---

## What is the DOM?

The Document Object Model (DOM) is a programming interface for HTML documents. It represents the page as a tree of objects that can be manipulated with JavaScript.

```javascript
// Access the document
console.log(document);

// Get page title
console.log(document.title);

// Get URL
console.log(document.URL);
```

---

## DOM Tree Structure

```
document
  └── html
      ├── head
      │   ├── title
      │   └── meta
      └── body
          ├── h1
          ├── p
          └── div
              ├── span
              └── button
```

```javascript
// Root element
console.log(document.documentElement);  // <html>

// Head and body
console.log(document.head);  // <head>
console.log(document.body);  // <body>
```

---

## Document Object

```javascript
// Get element by ID
const elem = document.getElementById('myId');

// Get elements by class
const elems = document.getElementsByClassName('myClass');

// Query selector
const first = document.querySelector('.myClass');
const all = document.querySelectorAll('.myClass');

// Create element
const div = document.createElement('div');

// Get document info
console.log(document.title);        // Page title
console.log(document.URL);          // Full URL
console.log(document.domain);       // Domain
console.log(document.characterSet); // Character encoding
```

---

## Window vs Document

```javascript
// window: Global object (browser environment)
console.log(window.innerWidth);
console.log(window.innerHeight);
console.log(window.location.href);

// document: HTML document
console.log(document.title);
console.log(document.body);

// document is property of window
console.log(window.document === document);  // true
```

---

## Node Types

```javascript
// Element nodes
const div = document.querySelector('div');
console.log(div.nodeType);  // 1

// Text nodes
const text = div.firstChild;
console.log(text.nodeType);  // 3

// Common node types:
// 1: Element
// 3: Text
// 8: Comment
// 9: Document
```

---

## ⚠️ Common Mistakes

```javascript
// ❌ Accessing DOM before it loads
console.log(document.body);  // null if script in <head>

// ✓ Wait for DOM to load
document.addEventListener('DOMContentLoaded', () => {
  console.log(document.body);  // <body>
});

// ✓ Or put script at end of body
```

---

## 💼 Interview Tips

### Q1: What is the DOM?

**Answer:**
The DOM (Document Object Model) is a programming interface that represents an HTML document as a tree structure of objects. It allows JavaScript to access and manipulate HTML elements, attributes, and content.

### Q2: What's the difference between window and document?

**Answer:**
- `window`: Global object representing browser window, includes all browser APIs
- `document`: Property of window, represents the HTML document

```javascript
window.innerWidth;      // Browser API
document.title;         // Document property
window.document === document;  // true
```

---

**[← Back: Iteration Methods](../04-control-flow/03-iteration-methods.md)** | **[Next: Selecting Elements →](./02-selecting-elements.md)**

---

**Made with ❤️ for JavaScript learners**
