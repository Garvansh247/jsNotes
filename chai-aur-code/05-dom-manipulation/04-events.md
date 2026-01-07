# 🎪 DOM Events in JavaScript

## 📑 Table of Contents
- [addEventListener](#addeventlistener)
- [Event Object](#event-object)
- [Event Types](#event-types)
- [Event Bubbling](#event-bubbling)
- [Event Delegation](#event-delegation)
- [preventDefault](#preventdefault)
- [Common Mistakes](#-common-mistakes)
- [Interview Tips](#-interview-tips)

---

## addEventListener

```javascript
const button = document.querySelector('button');

// Add event listener
button.addEventListener('click', function() {
  console.log('Button clicked!');
});

// Arrow function
button.addEventListener('click', () => {
  console.log('Clicked!');
});

// Named function
function handleClick() {
  console.log('Clicked!');
}
button.addEventListener('click', handleClick);

// Remove event listener
button.removeEventListener('click', handleClick);

// Add once (auto-removes after first trigger)
button.addEventListener('click', handleClick, {once: true});
```

---

## Event Object

```javascript
button.addEventListener('click', (event) => {
  console.log(event.type);        // 'click'
  console.log(event.target);      // Element clicked
  console.log(event.currentTarget); // Element with listener
  console.log(event.clientX);     // Mouse X
  console.log(event.clientY);     // Mouse Y
  console.log(event.timestamp);   // Time of event
});

// Keyboard event
input.addEventListener('keydown', (e) => {
  console.log(e.key);         // Key pressed
  console.log(e.code);        // Physical key
  console.log(e.shiftKey);    // Is shift pressed?
  console.log(e.ctrlKey);     // Is ctrl pressed?
  console.log(e.altKey);      // Is alt pressed?
});
```

---

## Event Types

```javascript
// Mouse events
elem.addEventListener('click', handler);
elem.addEventListener('dblclick', handler);
elem.addEventListener('mousedown', handler);
elem.addEventListener('mouseup', handler);
elem.addEventListener('mousemove', handler);
elem.addEventListener('mouseenter', handler);
elem.addEventListener('mouseleave', handler);
elem.addEventListener('mouseover', handler);
elem.addEventListener('mouseout', handler);

// Keyboard events
input.addEventListener('keydown', handler);
input.addEventListener('keyup', handler);
input.addEventListener('keypress', handler);  // Deprecated

// Form events
form.addEventListener('submit', handler);
input.addEventListener('input', handler);
input.addEventListener('change', handler);
input.addEventListener('focus', handler);
input.addEventListener('blur', handler);

// Document events
document.addEventListener('DOMContentLoaded', handler);
window.addEventListener('load', handler);
window.addEventListener('resize', handler);
window.addEventListener('scroll', handler);
```

---

## Event Bubbling

```javascript
// Events bubble up from target to ancestors

<div class="outer">
  <div class="inner">
    <button>Click me</button>
  </div>
</div>

document.querySelector('.outer').addEventListener('click', () => {
  console.log('Outer clicked');
});

document.querySelector('.inner').addEventListener('click', () => {
  console.log('Inner clicked');
});

document.querySelector('button').addEventListener('click', () => {
  console.log('Button clicked');
});

// Clicking button logs:
// "Button clicked"
// "Inner clicked"
// "Outer clicked"

// Stop propagation
button.addEventListener('click', (e) => {
  e.stopPropagation();
  console.log('Button clicked');
});
// Now only logs: "Button clicked"
```

---

## Event Delegation

```javascript
// Instead of adding listeners to each item
const items = document.querySelectorAll('.item');
items.forEach(item => {
  item.addEventListener('click', handleClick);
});

// Add single listener to parent (more efficient)
document.querySelector('.list').addEventListener('click', (e) => {
  if (e.target.classList.contains('item')) {
    console.log('Item clicked:', e.target);
  }
});

// Works for dynamically added elements
document.querySelector('.list').addEventListener('click', (e) => {
  const item = e.target.closest('.item');
  if (item) {
    console.log('Item clicked:', item);
  }
});
```

---

## preventDefault

```javascript
// Prevent default form submission
form.addEventListener('submit', (e) => {
  e.preventDefault();
  // Handle form with JavaScript
});

// Prevent default link navigation
link.addEventListener('click', (e) => {
  e.preventDefault();
  // Custom navigation
});

// Prevent context menu
document.addEventListener('contextmenu', (e) => {
  e.preventDefault();
});
```

---

## ⚠️ Common Mistakes

```javascript
// ❌ Forgetting to prevent default
form.addEventListener('submit', () => {
  // Process form
  // Form still submits!
});

// ✓ Prevent default
form.addEventListener('submit', (e) => {
  e.preventDefault();
  // Now form won't submit
});

// ❌ Adding listener in loop
items.forEach(item => {
  item.addEventListener('click', () => {
    // Many listeners!
  });
});

// ✓ Use event delegation
parent.addEventListener('click', (e) => {
  if (e.target.matches('.item')) {
    // Single listener
  }
});
```

---

## 💼 Interview Tips

### Q1: What is event bubbling?

**Answer:**
Events propagate from target element up through ancestors to document root.

```javascript
<div id="parent">
  <button id="child">Click</button>
</div>

// Clicking button triggers:
// 1. button click
// 2. div click
// 3. body click
// 4. document click
```

### Q2: What is event delegation?

**Answer:**
Adding a single event listener to a parent to handle events on multiple children, using event bubbling.

**Benefits:**
- Better performance
- Works with dynamically added elements

```javascript
// Instead of many listeners
list.addEventListener('click', (e) => {
  if (e.target.matches('.item')) {
    // Handle item click
  }
});
```

### Q3: What's the difference between target and currentTarget?

**Answer:**
- `target`: Element that triggered the event
- `currentTarget`: Element with the listener

```javascript
parent.addEventListener('click', (e) => {
  console.log(e.target);        // Clicked element
  console.log(e.currentTarget); // parent
});
```

---

**[← Back: Modifying Elements](./03-modifying-elements.md)** | **[Next: Closures →](../06-advanced/01-closures.md)**

---

**Made with ❤️ for JavaScript learners**
