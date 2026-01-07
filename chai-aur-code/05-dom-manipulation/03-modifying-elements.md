# ✏️ Modifying DOM Elements in JavaScript

## 📑 Table of Contents
- [Changing Content](#changing-content)
- [Attributes](#attributes)
- [Classes](#classes)
- [Styles](#styles)
- [Creating and Removing Elements](#creating-and-removing-elements)
- [Common Mistakes](#-common-mistakes)
- [Interview Tips](#-interview-tips)

---

## Changing Content

```javascript
const elem = document.querySelector('#myDiv');

// innerHTML: HTML content
elem.innerHTML = '<p>New <strong>HTML</strong> content</p>';

// textContent: Plain text
elem.textContent = 'Plain text content';

// innerText: Visible text
elem.innerText = 'Visible text';

// Difference:
// textContent: All text including hidden
// innerText: Only visible text
```

---

## Attributes

```javascript
const img = document.querySelector('img');

// Get attribute
console.log(img.getAttribute('src'));
console.log(img.src);  // Direct property access

// Set attribute
img.setAttribute('src', 'new-image.jpg');
img.src = 'new-image.jpg';  // Direct property

// Remove attribute
img.removeAttribute('alt');

// Check if has attribute
if (img.hasAttribute('data-id')) {
  console.log('Has data-id');
}

// Data attributes
elem.setAttribute('data-user-id', '123');
console.log(elem.dataset.userId);  // '123'
elem.dataset.userName = 'John';
console.log(elem.getAttribute('data-user-name'));  // 'John'
```

---

## Classes

```javascript
const elem = document.querySelector('.box');

// Add class
elem.classList.add('active');
elem.classList.add('highlight', 'selected');  // Multiple

// Remove class
elem.classList.remove('old-class');

// Toggle class
elem.classList.toggle('active');  // Add if absent, remove if present

// Check if has class
if (elem.classList.contains('active')) {
  console.log('Element is active');
}

// Replace class
elem.classList.replace('old', 'new');

// Get all classes
console.log(elem.classList);  // DOMTokenList
console.log(elem.className);  // String: "box active highlight"
```

---

## Styles

```javascript
const elem = document.querySelector('.box');

// Set inline style
elem.style.color = 'red';
elem.style.backgroundColor = 'blue';
elem.style.fontSize = '20px';

// Get computed style
const styles = window.getComputedStyle(elem);
console.log(styles.color);
console.log(styles.width);

// Remove style
elem.style.color = '';

// Set multiple styles
Object.assign(elem.style, {
  color: 'red',
  backgroundColor: 'blue',
  padding: '10px'
});

// Using cssText
elem.style.cssText = 'color: red; background: blue; padding: 10px;';
```

---

## Creating and Removing Elements

### Creating

```javascript
// createElement
const div = document.createElement('div');
div.textContent = 'New div';
div.className = 'box';
div.id = 'myDiv';

// Append to document
document.body.appendChild(div);

// insertBefore
const parent = document.querySelector('.container');
const reference = document.querySelector('.item:first-child');
parent.insertBefore(div, reference);

// insertAdjacentHTML
elem.insertAdjacentHTML('beforebegin', '<p>Before</p>');
elem.insertAdjacentHTML('afterbegin', '<p>First child</p>');
elem.insertAdjacentHTML('beforeend', '<p>Last child</p>');
elem.insertAdjacentHTML('afterend', '<p>After</p>');

// insertAdjacentElement
const newElem = document.createElement('div');
elem.insertAdjacentElement('beforeend', newElem);
```

### Removing

```javascript
// remove()
const elem = document.querySelector('.remove-me');
elem.remove();

// removeChild()
const parent = document.querySelector('.parent');
const child = document.querySelector('.child');
parent.removeChild(child);

// Remove all children
parent.innerHTML = '';

// Better: remove all children
while (parent.firstChild) {
  parent.removeChild(parent.firstChild);
}
```

### Cloning

```javascript
const original = document.querySelector('.original');

// Shallow clone
const clone = original.cloneNode();

// Deep clone (includes children)
const deepClone = original.cloneNode(true);

// Append clone
document.body.appendChild(deepClone);
```

---

## ⚠️ Common Mistakes

```javascript
// ❌ innerHTML with user input (XSS risk)
elem.innerHTML = userInput;

// ✓ Use textContent for text
elem.textContent = userInput;

// ❌ Setting style properties incorrectly
elem.style['background-color'] = 'red';  // Won't work

// ✓ Use camelCase
elem.style.backgroundColor = 'red';
```

---

## 💼 Interview Tips

### Q1: What's the difference between innerHTML and textContent?

**Answer:**
- `innerHTML`: Parses HTML, can be security risk
- `textContent`: Plain text only, safer

```javascript
elem.innerHTML = '<strong>Bold</strong>';  // Renders HTML
elem.textContent = '<strong>Bold</strong>';  // Shows as text
```

### Q2: How do you safely insert user content?

**Answer:**
Use `textContent` for plain text, or sanitize HTML if needed.

```javascript
// Safe for text
elem.textContent = userInput;

// For HTML, use library like DOMPurify
elem.innerHTML = DOMPurify.sanitize(userHTML);
```

---

**[← Back: Selecting Elements](./02-selecting-elements.md)** | **[Next: Events →](./04-events.md)**

---

**Made with ❤️ for JavaScript learners**
