# 🔄 Event Loop - The Heart of JavaScript

## 📑 Table of Contents
- [Introduction](#introduction)
- [JavaScript Runtime Environment](#javascript-runtime-environment)
- [Call Stack](#call-stack)
- [Web APIs](#web-apis)
- [Callback Queue (Task Queue)](#callback-queue-task-queue)
- [Microtask Queue](#microtask-queue)
- [Event Loop Mechanism](#event-loop-mechanism)
- [Execution Priority](#execution-priority)
- [Practical Examples](#practical-examples)
- [Starvation](#starvation)
- [Interview Questions](#-interview-questions)
- [Visual Diagrams](#visual-diagrams)

---

## Introduction

The **Event Loop** is the mechanism that allows JavaScript to perform non-blocking operations despite being single-threaded. Understanding the event loop is crucial for:
- Writing asynchronous code
- Debugging timing issues
- Acing JavaScript interviews
- Understanding how JavaScript really works

**Key Concept:** JavaScript is **single-threaded** but can handle **asynchronous operations** efficiently through the event loop.

---

## JavaScript Runtime Environment

JavaScript runtime consists of several components:

```
┌─────────────────────────────────────────┐
│      JavaScript Runtime Environment      │
├─────────────────────────────────────────┤
│  ┌───────────────┐  ┌──────────────┐   │
│  │   Call Stack  │  │   Web APIs   │   │
│  └───────────────┘  └──────────────┘   │
│  ┌───────────────┐  ┌──────────────┐   │
│  │ Microtask Q   │  │ Callback Q   │   │
│  └───────────────┘  └──────────────┘   │
│         ┌──────────────┐                │
│         │  Event Loop  │                │
│         └──────────────┘                │
└─────────────────────────────────────────┘
```

### Components:

1. **Heap**: Memory allocation
2. **Call Stack**: Tracks function execution
3. **Web APIs**: Browser-provided APIs (setTimeout, fetch, DOM, etc.)
4. **Callback Queue**: Holds callback functions (macrotasks)
5. **Microtask Queue**: Holds microtasks (promises, mutation observers)
6. **Event Loop**: Coordinates execution between stack and queues

---

## Call Stack

The call stack is a **LIFO (Last In, First Out)** data structure that tracks function execution.

```javascript
function first() {
  console.log("First");
  second();
  console.log("First again");
}

function second() {
  console.log("Second");
  third();
}

function third() {
  console.log("Third");
}

first();
```

**Call Stack Visualization:**

```
Step 1: Global Execution Context
┌────────────┐
│  Global EC │
└────────────┘

Step 2: first() called
┌────────────┐
│  first()   │
├────────────┤
│  Global EC │
└────────────┘

Step 3: second() called
┌────────────┐
│  second()  │
├────────────┤
│  first()   │
├────────────┤
│  Global EC │
└────────────┘

Step 4: third() called
┌────────────┐
│  third()   │
├────────────┤
│  second()  │
├────────────┤
│  first()   │
├────────────┤
│  Global EC │
└────────────┘

Then functions pop off as they complete...
```

**Output:**
```
First
Second
Third
First again
```

---

## Web APIs

Web APIs are browser-provided features that run **outside the JavaScript engine**:

- **Timers**: `setTimeout`, `setInterval`
- **DOM**: `document`, `addEventListener`
- **Network**: `fetch`, `XMLHttpRequest`
- **Console**: `console.log`
- **Others**: `localStorage`, `IndexedDB`, etc.

```javascript
console.log("Start");

setTimeout(() => {
  console.log("Timeout");
}, 0);

console.log("End");
```

**What happens:**
1. "Start" logs immediately
2. `setTimeout` is handed off to Web API
3. "End" logs immediately
4. After 0ms, callback moves to Callback Queue
5. Event loop pushes callback to call stack
6. "Timeout" logs

**Output:**
```
Start
End
Timeout
```

**Why?** Even with 0ms delay, `setTimeout` callback goes through the Callback Queue and waits for the call stack to be empty.

---

## Callback Queue (Task Queue)

The **Callback Queue** (also called Task Queue or Macrotask Queue) holds callbacks from:
- `setTimeout`
- `setInterval`
- `setImmediate` (Node.js)
- DOM events
- I/O operations

**Characteristics:**
- FIFO (First In, First Out)
- Lower priority than Microtask Queue
- One task executes per event loop tick

---

## Microtask Queue

The **Microtask Queue** holds callbacks from:
- Promise `.then()`, `.catch()`, `.finally()`
- `queueMicrotask()`
- `MutationObserver`
- `process.nextTick()` (Node.js - even higher priority)

**Characteristics:**
- FIFO (First In, First Out)
- **Higher priority** than Callback Queue
- **All microtasks** execute before any macrotask

```javascript
console.log("Start");

setTimeout(() => {
  console.log("Timeout");
}, 0);

Promise.resolve().then(() => {
  console.log("Promise");
});

console.log("End");
```

**Output:**
```
Start
End
Promise
Timeout
```

**Why?** Promise microtask executes before setTimeout macrotask.

---

## Event Loop Mechanism

The **Event Loop** continuously checks:

1. **Is the Call Stack empty?**
2. **Are there microtasks?** → Execute ALL microtasks
3. **Are there macrotasks?** → Execute ONE macrotask
4. **Repeat**

**Algorithm:**

```
while (true) {
  // Execute all microtasks
  while (microtaskQueue.hasTask()) {
    task = microtaskQueue.dequeue();
    execute(task);
  }
  
  // Execute ONE macrotask
  if (callbackQueue.hasTask()) {
    task = callbackQueue.dequeue();
    execute(task);
  }
  
  // Render if needed (60fps)
  if (shouldRender()) {
    render();
  }
}
```

---

## Execution Priority

**Priority Order (Highest to Lowest):**

1. **Call Stack** (synchronous code)
2. **Microtask Queue** (promises, queueMicrotask)
3. **Callback Queue** (setTimeout, setInterval)

```javascript
console.log("1"); // Call Stack

setTimeout(() => {
  console.log("2"); // Callback Queue
}, 0);

Promise.resolve().then(() => {
  console.log("3"); // Microtask Queue
});

Promise.resolve().then(() => {
  console.log("4"); // Microtask Queue
});

setTimeout(() => {
  console.log("5"); // Callback Queue
}, 0);

console.log("6"); // Call Stack
```

**Output:**
```
1
6
3
4
2
5
```

**Explanation:**
1. Synchronous code executes first: `1`, `6`
2. All microtasks execute: `3`, `4`
3. Macrotasks execute one by one: `2`, `5`

---

## Practical Examples

### Example 1: Mixing Promises and Timeouts

```javascript
console.log("Start");

setTimeout(() => {
  console.log("Timeout 1");
}, 0);

Promise.resolve().then(() => {
  console.log("Promise 1");
  
  setTimeout(() => {
    console.log("Timeout 2");
  }, 0);
  
  Promise.resolve().then(() => {
    console.log("Promise 2");
  });
});

setTimeout(() => {
  console.log("Timeout 3");
}, 0);

console.log("End");
```

**Output:**
```
Start
End
Promise 1
Promise 2
Timeout 1
Timeout 3
Timeout 2
```

**Step-by-step:**
1. `Start`, `End` → Call Stack
2. `Promise 1` → Microtask Queue (executes)
3. `Promise 2` → Microtask Queue (executes immediately)
4. `Timeout 1` → Callback Queue (waits)
5. `Timeout 3` → Callback Queue (waits)
6. `Timeout 2` → Callback Queue (added after Promise 1)
7. Timeouts execute in order: 1, 3, 2

---

### Example 2: Nested Promises

```javascript
Promise.resolve().then(() => {
  console.log("Promise 1");
  
  Promise.resolve().then(() => {
    console.log("Promise 2");
    
    Promise.resolve().then(() => {
      console.log("Promise 3");
    });
  });
  
  Promise.resolve().then(() => {
    console.log("Promise 4");
  });
});

Promise.resolve().then(() => {
  console.log("Promise 5");
});
```

**Output:**
```
Promise 1
Promise 5
Promise 2
Promise 4
Promise 3
```

**Why?** Microtasks added during microtask execution are added to the end of the current microtask queue.

---

### Example 3: Async/Await

```javascript
async function async1() {
  console.log("Async 1 start");
  await async2();
  console.log("Async 1 end");
}

async function async2() {
  console.log("Async 2");
}

console.log("Start");

setTimeout(() => {
  console.log("Timeout");
}, 0);

async1();

Promise.resolve().then(() => {
  console.log("Promise");
});

console.log("End");
```

**Output:**
```
Start
Async 1 start
Async 2
End
Async 1 end
Promise
Timeout
```

**Key Point:** `await` creates a promise, so code after `await` goes to Microtask Queue.

---

## Starvation

**Microtask Queue Starvation:** If microtasks keep adding more microtasks, macrotasks will never execute.

```javascript
function recursiveMicrotask() {
  Promise.resolve().then(() => {
    console.log("Microtask");
    recursiveMicrotask(); // Adds another microtask
  });
}

recursiveMicrotask();

setTimeout(() => {
  console.log("This will NEVER run!"); // Starved
}, 0);
```

**Solution:** Be careful with infinite microtask loops. Use macrotasks when appropriate.

---

## 💼 Interview Questions

### Q1: Explain the Event Loop.

**Answer:**
The Event Loop is a mechanism that allows JavaScript to perform non-blocking operations despite being single-threaded. It continuously monitors the Call Stack and Task Queues:

1. Executes synchronous code on the Call Stack
2. When Call Stack is empty, processes **all microtasks** (promises)
3. Then processes **one macrotask** (setTimeout)
4. Repeats

**Key Point:** Microtasks have higher priority than macrotasks.

---

### Q2: What's the difference between Microtasks and Macrotasks?

**Answer:**

| Feature | Microtasks | Macrotasks |
|---------|------------|------------|
| Source | Promises, queueMicrotask | setTimeout, setInterval, I/O |
| Priority | Higher | Lower |
| Execution | ALL before next macrotask | ONE per event loop cycle |
| Examples | `.then()`, `.catch()` | `setTimeout`, DOM events |

---

### Q3: Predict the output:

```javascript
console.log("1");

setTimeout(() => console.log("2"), 0);

Promise.resolve().then(() => console.log("3"));

console.log("4");
```

**Answer:**
```
1
4
3
2
```

**Explanation:**
- `1`, `4` → Synchronous (Call Stack)
- `3` → Microtask (Promise)
- `2` → Macrotask (setTimeout)

---

### Q4: What is the Call Stack?

**Answer:**
The Call Stack is a LIFO data structure that tracks function execution. When a function is called, it's pushed onto the stack. When it returns, it's popped off. The Call Stack has limited size; exceeding it causes a "Stack Overflow" error.

---

### Q5: Why is setTimeout(fn, 0) not immediate?

**Answer:**
Even with 0ms delay, `setTimeout` callback:
1. Goes to Web API
2. Moves to Callback Queue after delay
3. Waits for Call Stack to be empty
4. Waits for all Microtasks to complete
5. Only then executes

This is why it's not truly "immediate."

---

## Visual Diagrams

### Event Loop Flow

```
┌─────────────────────────────┐
│      Synchronous Code       │
│     (Call Stack)            │
└─────────────┬───────────────┘
              │
              ▼
┌─────────────────────────────┐
│   All Microtasks Execute    │
│   (Promise callbacks)        │
└─────────────┬───────────────┘
              │
              ▼
┌─────────────────────────────┐
│   One Macrotask Executes    │
│   (setTimeout callback)      │
└─────────────┬───────────────┘
              │
              ▼
          Repeat ↻
```

---

### Complete Example Timeline

```javascript
console.log("A");
setTimeout(() => console.log("B"), 0);
Promise.resolve().then(() => console.log("C"));
console.log("D");
```

**Timeline:**

```
Time 0ms:
├─ Call Stack: [Global EC]
├─ Execute: console.log("A") → Output: A
├─ setTimeout → Web API (starts 0ms timer)
├─ Promise.resolve() → Microtask Queue: [C]
├─ Execute: console.log("D") → Output: D
└─ Call Stack: Empty

Time 0ms (immediately after):
├─ Call Stack: Empty
├─ Microtask Queue: [C]
├─ Execute microtask: console.log("C") → Output: C
├─ Microtask Queue: Empty
└─ setTimeout callback → Callback Queue: [B]

Time 0ms (after microtasks):
├─ Call Stack: Empty
├─ Microtask Queue: Empty
├─ Callback Queue: [B]
├─ Execute macrotask: console.log("B") → Output: B
└─ Done

Final Output: A D C B
```

---

**[← Previous: Callback Functions](./13-callback-functions-event-listeners.md)** | **[Next: JS Engine →](./15-js-engine-v8.md)**

---

**Made with ❤️ for JavaScript learners**
