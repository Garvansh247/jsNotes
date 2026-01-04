# 🙏 Namaste JavaScript - Deep Dive into JavaScript Internals

This section covers JavaScript internals and how things work under the hood, based on **Akshay Saini's** excellent "Namaste JavaScript" series. Perfect for understanding advanced concepts and acing interviews.

## 🎯 What You'll Learn

- **JavaScript Engine**: How JS code is executed
- **Execution Context**: Call stack, memory allocation, scope chain
- **Advanced Concepts**: Closures, hoisting, event loop deep dive
- **Interview Preparation**: Most asked JavaScript internals questions

## 📚 Course Structure

### [Season 1: Core JavaScript Internals](./season-1/)

Deep dive into how JavaScript works behind the scenes.

| File | Topics Covered |
|------|----------------|
| [01-execution-context.md](./season-1/01-execution-context.md) | What is execution context, components, stack |
| [02-call-stack.md](./season-1/02-call-stack.md) | Call stack mechanics, LIFO, stack overflow |
| [03-hoisting-deep-dive.md](./season-1/03-hoisting-deep-dive.md) | How hoisting really works, TDZ |
| [04-functions-and-variable-environment.md](./season-1/04-functions-and-variable-environment.md) | Variable environment, scope chain |
| [05-window-and-this.md](./season-1/05-window-and-this.md) | Global object, this in global context |
| [06-undefined-vs-not-defined.md](./season-1/06-undefined-vs-not-defined.md) | undefined vs null vs not defined |
| [07-scope-chain-and-lexical-environment.md](./season-1/07-scope-chain-and-lexical-environment.md) | Lexical environment, scope chain lookup |
| [08-let-const-temporal-dead-zone.md](./season-1/08-let-const-temporal-dead-zone.md) | TDZ explained, let vs const vs var |
| [09-block-scope-and-shadowing.md](./season-1/09-block-scope-and-shadowing.md) | Block scope, variable shadowing |
| [10-closures-deep-dive.md](./season-1/10-closures-deep-dive.md) | How closures work internally |
| [11-setTimeout-closures.md](./season-1/11-setTimeout-closures.md) | Famous setTimeout interview questions |
| [12-first-class-functions.md](./season-1/12-first-class-functions.md) | Functions as first-class citizens |
| [13-callback-functions-event-listeners.md](./season-1/13-callback-functions-event-listeners.md) | Callbacks, event listeners, GC |
| [14-event-loop.md](./season-1/14-event-loop.md) | Event loop mechanism, microtasks, macrotasks |
| [15-js-engine-v8.md](./season-1/15-js-engine-v8.md) | V8 engine architecture, JIT compilation |
| [16-higher-order-functions.md](./season-1/16-higher-order-functions.md) | What is HOF, functional programming |
| [17-map-filter-reduce.md](./season-1/17-map-filter-reduce.md) | Deep dive + polyfill implementations |

### [Season 2: Advanced Async & Promises](./season-2/)

Master asynchronous JavaScript and promises.

| File | Topics Covered |
|------|----------------|
| [01-callback-hell.md](./season-2/01-callback-hell.md) | Pyramid of doom, problems with callbacks |
| [02-promises.md](./season-2/02-promises.md) | Promise internals, states, immutability |
| [03-promise-chaining.md](./season-2/03-promise-chaining.md) | Proper chaining patterns, error propagation |
| [04-async-await.md](./season-2/04-async-await.md) | How async/await works behind scenes |
| [05-promise-apis.md](./season-2/05-promise-apis.md) | Promise.all, allSettled, race, any |
| [06-this-keyword-deep-dive.md](./season-2/06-this-keyword-deep-dive.md) | this binding rules, call/apply/bind |

## 🎯 Why This Section is Important

### For Interviews
- Most JavaScript interviews test internals knowledge
- Understanding "how" makes "what" easier
- Demonstrates deep technical understanding

### For Development
- Debug complex issues faster
- Write more efficient code
- Understand framework internals better

## 📺 Original Series

**Namaste JavaScript by Akshay Saini**
- 🔗 [Namaste JavaScript Playlist](https://www.youtube.com/playlist?list=PLlasXeu85E9cQ32gLCvAvr9vNaUccPVNP)
- 🎯 Focus: JavaScript internals with visualizations
- 🌟 Great for: Interview preparation and deep understanding

**🙏 Huge thanks to Akshay Saini for making JavaScript internals accessible!**

## 🚀 Learning Approach

**Recommended Order:**
1. Complete [Chai aur Code](../chai-aur-code/) basics first
2. Watch the videos alongside reading notes
3. Draw diagrams to visualize concepts
4. Practice output-based questions
5. Explain concepts to others

**Pro Tips:**
- 🎨 Draw execution context and call stack
- 🔄 Revisit difficult topics multiple times
- 💡 Relate concepts to real-world scenarios
- 📝 Practice explaining in interviews
- 🎯 Focus on "why" not just "what"

## 🎓 Learning Path

### Week 1: Foundation Internals
- Execution Context & Call Stack
- Hoisting Deep Dive
- Scope Chain & Lexical Environment
- TDZ and Block Scope

### Week 2: Advanced Concepts
- Closures Deep Dive
- First-Class Functions
- Higher Order Functions
- Event Loop & Async

### Week 3: Promises & Modern JS
- Callback Hell
- Promises Internals
- Async/Await
- Promise APIs

## 💡 Interview Focus Topics

**Must Know:**
1. ⭐ Execution Context & Call Stack
2. ⭐ Hoisting (var vs let vs const)
3. ⭐ Closures
4. ⭐ Event Loop
5. ⭐ Promises

**Important:**
6. Scope Chain
7. Temporal Dead Zone
8. this keyword
9. Higher Order Functions
10. Promise APIs

## 🔥 Famous Interview Questions

This section covers the **most asked** JavaScript interview questions:

- How does JavaScript code execute?
- What is the call stack?
- Explain hoisting with examples
- What is closure? (with code)
- How does event loop work?
- Difference between var, let, const (deep dive)
- What is Temporal Dead Zone?
- Explain setTimeout with closures
- How do promises work internally?
- What is the difference between Promise.all and Promise.allSettled?

---

**[← Back to Main README](../README.md)** | **[Start Season 1 →](./season-1/01-execution-context.md)**

---

**Happy Learning! 🙏✨**
