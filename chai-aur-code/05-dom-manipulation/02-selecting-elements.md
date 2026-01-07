# 🎯 Selecting DOM Elements in JavaScript

## 📑 Table of Contents
- [getElementById](#getelementbyid)
- [querySelector](#queryselector)
- [getElementsByClassName](#getelementsbyclassname)
- [getElementsByTagName](#getelementsbytagname)
- [Traversing the DOM](#traversing-the-dom)
- [Common Mistakes](#-common-mistakes)
- [Interview Tips](#-interview-tips)

---

## getElementById

```javascript
// Get element by ID
const header = document.getElementById('header');
console.log(header);

// Returns null if not found
const notFound = document.getElementById('nonexistent');
console.log(notFound);  // null

// ID must be unique
const elem = document.getElementById('myId');
elem.textContent = 'Updated!';
```

---

## querySelector

```javascript
// Get first element matching CSS selector
const first = document.querySelector('.myClass');
const byId = document.querySelector('#myId');
const byTag = document.querySelector('div');

// Complex selectors
const nested = document.querySelector('.container .item');
const attribute = document.querySelector('[data-id="123"]');
const pseudo = document.querySelector('li:first-child');

// querySelectorAll: get all matches
const all = document.querySelectorAll('.myClass');
console.log(all);  // NodeList

// Convert to array
const array = Array.from(all);
const array2 = [...all];

// Iterate
all.forEach(elem => {
  console.log(elem.textContent);
});
```

---

## getElementsByClassName

```javascript
// Get elements by class (returns HTMLCollection)
const items = document.getElementsByClassName('item');
console.log(items);  // HTMLCollection

// Access by index
console.log(items[0]);
console.log(items.length);

// Convert to array
const array = Array.from(items);

// Live collection (updates automatically)
const divs = document.getElementsByClassName('box');
console.log(divs.length);  // e.g., 3

document.querySelector('.box').remove();
console.log(divs.length);  // 2 (automatically updated)
```

---

## getElementsByTagName

```javascript
// Get elements by tag name
const paragraphs = document.getElementsByTagName('p');
const divs = document.getElementsByTagName('div');

// Get all elements
const allElements = document.getElementsByTagName('*');

// Iterate
for (let p of paragraphs) {
  console.log(p.textContent);
}
```

---

## Traversing the DOM

### Parent, Children, Siblings

```javascript
const elem = document.querySelector('.child');

// Parent
console.log(elem.parentElement);
console.log(elem.parentNode);

// Children
const parent = document.querySelector('.parent');
console.log(parent.children);        // HTMLCollection
console.log(parent.childNodes);      // NodeList (includes text nodes)
console.log(parent.firstElementChild);
console.log(parent.lastElementChild);

// Siblings
console.log(elem.nextElementSibling);
console.log(elem.previousElementSibling);

// Example: get all siblings
function getSiblings(elem) {
  return Array.from(elem.parentElement.children)
    .filter(child => child !== elem);
}
```

### Closest (Traverse Up)

```javascript
// Find closest ancestor matching selector
const button = document.querySelector('button');
const card = button.closest('.card');
const container = button.closest('.container');

// Useful for event delegation
document.querySelector('.list').addEventListener('click', (e) => {
  const item = e.target.closest('.item');
  if (item) {
    console.log('Item clicked:', item);
  }
});
```

---

## ⚠️ Common Mistakes

```javascript
// ❌ querySelector returns first match only
const items = document.querySelector('.item');  // Only first!

// ✓ Use querySelectorAll for all
const items = document.querySelectorAll('.item');

// ❌ HTMLCollection is not an array
const divs = document.getElementsByClassName('box');
// divs.map()  // Error: map is not a function

// ✓ Convert to array first
const array = Array.from(divs);
array.map(div => div.textContent);
```

---

## 💼 Interview Tips

### Q1: What's the difference between querySelector and getElementById?

**Answer:**
- `getElementById`: Faster, only selects by ID
- `querySelector`: More flexible, uses CSS selectors

```javascript
document.getElementById('myId');      // Faster
document.querySelector('#myId');      // More flexible
document.querySelector('.class > p'); // Can do complex selectors
```

### Q2: What's the difference between HTMLCollection and NodeList?

**Answer:**
- **HTMLCollection**: Live, only element nodes, from getElementsBy* methods
- **NodeList**: Can be live or static, all node types, from querySelectorAll (static)

```javascript
const live = document.getElementsByClassName('box');  // Live
const static = document.querySelectorAll('.box');     // Static

// Add new element
document.body.appendChild(newBox);

console.log(live.length);    // Increases
console.log(static.length);  // Unchanged
```

---

**[← Back: DOM Basics](./01-dom-basics.md)** | **[Next: Modifying Elements →](./03-modifying-elements.md)**

---

**Made with ❤️ for JavaScript learners**
