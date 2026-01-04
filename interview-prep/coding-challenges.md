# 💻 JavaScript Coding Challenges

25 practical coding problems with step-by-step solutions commonly asked in JavaScript interviews.

## 📑 Table of Contents
- [String Manipulation](#string-manipulation)
- [Array Operations](#array-operations)
- [Algorithm Problems](#algorithm-problems)
- [Utility Functions](#utility-functions)
- [Polyfill Implementations](#polyfill-implementations)

---

## String Manipulation

### 1. Reverse a String

**Problem:** Reverse the given string.

```javascript
// Input: "hello"
// Output: "olleh"
```

**Solutions:**

```javascript
// Solution 1: Using built-in methods
function reverseString1(str) {
  return str.split('').reverse().join('');
}

// Solution 2: Using loop
function reverseString2(str) {
  let reversed = '';
  for (let i = str.length - 1; i >= 0; i--) {
    reversed += str[i];
  }
  return reversed;
}

// Solution 3: Using reduce
function reverseString3(str) {
  return str.split('').reduce((rev, char) => char + rev, '');
}

// Solution 4: Recursive
function reverseString4(str) {
  if (str === "") return "";
  return reverseString4(str.substr(1)) + str[0];
}

// Test
console.log(reverseString1("hello"));  // "olleh"
```

**Time Complexity:** O(n)  
**Space Complexity:** O(n)

---

### 2. Palindrome Check

**Problem:** Check if a string is a palindrome (reads the same forwards and backwards).

```javascript
// Input: "racecar"
// Output: true

// Input: "hello"
// Output: false
```

**Solutions:**

```javascript
// Solution 1: Reverse and compare
function isPalindrome1(str) {
  const cleaned = str.toLowerCase().replace(/[^a-z0-9]/g, '');
  const reversed = cleaned.split('').reverse().join('');
  return cleaned === reversed;
}

// Solution 2: Two pointers
function isPalindrome2(str) {
  const cleaned = str.toLowerCase().replace(/[^a-z0-9]/g, '');
  let left = 0;
  let right = cleaned.length - 1;
  
  while (left < right) {
    if (cleaned[left] !== cleaned[right]) {
      return false;
    }
    left++;
    right--;
  }
  return true;
}

// Solution 3: Recursive
function isPalindrome3(str) {
  const cleaned = str.toLowerCase().replace(/[^a-z0-9]/g, '');
  
  if (cleaned.length <= 1) return true;
  if (cleaned[0] !== cleaned[cleaned.length - 1]) return false;
  
  return isPalindrome3(cleaned.slice(1, -1));
}

// Test
console.log(isPalindrome1("A man, a plan, a canal: Panama"));  // true
console.log(isPalindrome1("race a car"));  // false
```

**Time Complexity:** O(n)  
**Space Complexity:** O(n)

---

### 3. Count Vowels

**Problem:** Count the number of vowels in a string.

```javascript
// Input: "hello world"
// Output: 3 (e, o, o)
```

**Solutions:**

```javascript
// Solution 1: Using match with regex
function countVowels1(str) {
  const matches = str.match(/[aeiou]/gi);
  return matches ? matches.length : 0;
}

// Solution 2: Using filter
function countVowels2(str) {
  const vowels = ['a', 'e', 'i', 'o', 'u'];
  return str.toLowerCase().split('').filter(char => vowels.includes(char)).length;
}

// Solution 3: Using reduce
function countVowels3(str) {
  const vowels = 'aeiouAEIOU';
  return str.split('').reduce((count, char) => 
    vowels.includes(char) ? count + 1 : count, 0
  );
}

// Test
console.log(countVowels1("hello world"));  // 3
console.log(countVowels1("JavaScript"));   // 3
```

**Time Complexity:** O(n)  
**Space Complexity:** O(1)

---

## Array Operations

### 4. FizzBuzz

**Problem:** Print numbers from 1 to n. For multiples of 3, print "Fizz". For multiples of 5, print "Buzz". For multiples of both, print "FizzBuzz".

```javascript
// Input: 15
// Output: [1, 2, "Fizz", 4, "Buzz", "Fizz", 7, 8, "Fizz", "Buzz", 11, "Fizz", 13, 14, "FizzBuzz"]
```

**Solution:**

```javascript
function fizzBuzz(n) {
  const result = [];
  
  for (let i = 1; i <= n; i++) {
    if (i % 15 === 0) {
      result.push("FizzBuzz");
    } else if (i % 3 === 0) {
      result.push("Fizz");
    } else if (i % 5 === 0) {
      result.push("Buzz");
    } else {
      result.push(i);
    }
  }
  
  return result;
}

// Cleaner version
function fizzBuzz2(n) {
  return Array.from({ length: n }, (_, i) => {
    const num = i + 1;
    if (num % 15 === 0) return "FizzBuzz";
    if (num % 3 === 0) return "Fizz";
    if (num % 5 === 0) return "Buzz";
    return num;
  });
}

// Test
console.log(fizzBuzz(15));
```

**Time Complexity:** O(n)  
**Space Complexity:** O(n)

---

### 5. Find Duplicates in Array

**Problem:** Find all duplicate elements in an array.

```javascript
// Input: [1, 2, 3, 2, 4, 5, 5, 6]
// Output: [2, 5]
```

**Solutions:**

```javascript
// Solution 1: Using Set and filter
function findDuplicates1(arr) {
  const seen = new Set();
  const duplicates = new Set();
  
  arr.forEach(item => {
    if (seen.has(item)) {
      duplicates.add(item);
    } else {
      seen.add(item);
    }
  });
  
  return [...duplicates];
}

// Solution 2: Using reduce
function findDuplicates2(arr) {
  const counts = arr.reduce((acc, item) => {
    acc[item] = (acc[item] || 0) + 1;
    return acc;
  }, {});
  
  return Object.keys(counts).filter(key => counts[key] > 1).map(Number);
}

// Solution 3: Using filter
function findDuplicates3(arr) {
  return arr.filter((item, index) => arr.indexOf(item) !== index && arr.indexOf(item) === arr.lastIndexOf(item));
}

// Test
console.log(findDuplicates1([1, 2, 3, 2, 4, 5, 5, 6]));  // [2, 5]
```

**Time Complexity:** O(n)  
**Space Complexity:** O(n)

---

### 6. Remove Duplicates from Array

**Problem:** Remove all duplicate elements from an array.

```javascript
// Input: [1, 2, 2, 3, 4, 4, 5]
// Output: [1, 2, 3, 4, 5]
```

**Solutions:**

```javascript
// Solution 1: Using Set (easiest)
function removeDuplicates1(arr) {
  return [...new Set(arr)];
}

// Solution 2: Using filter
function removeDuplicates2(arr) {
  return arr.filter((item, index) => arr.indexOf(item) === index);
}

// Solution 3: Using reduce
function removeDuplicates3(arr) {
  return arr.reduce((unique, item) => 
    unique.includes(item) ? unique : [...unique, item], []
  );
}

// Solution 4: Using Map
function removeDuplicates4(arr) {
  const map = new Map();
  arr.forEach(item => map.set(item, true));
  return [...map.keys()];
}

// Test
console.log(removeDuplicates1([1, 2, 2, 3, 4, 4, 5]));  // [1, 2, 3, 4, 5]
```

**Time Complexity:** O(n)  
**Space Complexity:** O(n)

---

### 7. Flatten Nested Array

**Problem:** Flatten a nested array to a single level.

```javascript
// Input: [1, [2, [3, [4]], 5]]
// Output: [1, 2, 3, 4, 5]
```

**Solutions:**

```javascript
// Solution 1: Using flat() (ES2019)
function flatten1(arr) {
  return arr.flat(Infinity);
}

// Solution 2: Recursive
function flatten2(arr) {
  const result = [];
  
  arr.forEach(item => {
    if (Array.isArray(item)) {
      result.push(...flatten2(item));
    } else {
      result.push(item);
    }
  });
  
  return result;
}

// Solution 3: Using reduce
function flatten3(arr) {
  return arr.reduce((flat, item) => 
    flat.concat(Array.isArray(item) ? flatten3(item) : item), []
  );
}

// Solution 4: Using stack (iterative)
function flatten4(arr) {
  const stack = [...arr];
  const result = [];
  
  while (stack.length) {
    const item = stack.pop();
    if (Array.isArray(item)) {
      stack.push(...item);
    } else {
      result.unshift(item);
    }
  }
  
  return result;
}

// Test
console.log(flatten2([1, [2, [3, [4]], 5]]));  // [1, 2, 3, 4, 5]
```

**Time Complexity:** O(n)  
**Space Complexity:** O(n)

---

### 8. Chunk Array

**Problem:** Split array into chunks of specified size.

```javascript
// Input: ([1, 2, 3, 4, 5, 6, 7, 8], 3)
// Output: [[1, 2, 3], [4, 5, 6], [7, 8]]
```

**Solutions:**

```javascript
// Solution 1: Using slice
function chunk1(arr, size) {
  const result = [];
  for (let i = 0; i < arr.length; i += size) {
    result.push(arr.slice(i, i + size));
  }
  return result;
}

// Solution 2: Using reduce
function chunk2(arr, size) {
  return arr.reduce((chunks, item, index) => {
    if (index % size === 0) {
      chunks.push([item]);
    } else {
      chunks[chunks.length - 1].push(item);
    }
    return chunks;
  }, []);
}

// Solution 3: Using splice (mutates original)
function chunk3(arr, size) {
  const result = [];
  const copy = [...arr];
  while (copy.length) {
    result.push(copy.splice(0, size));
  }
  return result;
}

// Test
console.log(chunk1([1, 2, 3, 4, 5, 6, 7, 8], 3));
// [[1, 2, 3], [4, 5, 6], [7, 8]]
```

**Time Complexity:** O(n)  
**Space Complexity:** O(n)

---

## Utility Functions

### 9. Debounce Function

**Problem:** Create a debounce function that delays execution until after a wait period.

```javascript
// Usage: debounce(fn, 300) - fn executes only after 300ms of no calls
```

**Solution:**

```javascript
function debounce(func, wait) {
  let timeout;
  
  return function executedFunction(...args) {
    const later = () => {
      clearTimeout(timeout);
      func(...args);
    };
    
    clearTimeout(timeout);
    timeout = setTimeout(later, wait);
  };
}

// With immediate option
function debounce2(func, wait, immediate = false) {
  let timeout;
  
  return function executedFunction(...args) {
    const callNow = immediate && !timeout;
    
    clearTimeout(timeout);
    timeout = setTimeout(() => {
      timeout = null;
      if (!immediate) func(...args);
    }, wait);
    
    if (callNow) func(...args);
  };
}

// Test
const searchAPI = debounce((query) => {
  console.log("Searching for:", query);
}, 500);

// These calls are debounced
searchAPI("a");
searchAPI("ab");
searchAPI("abc");  // Only this executes after 500ms
```

**Use Case:** Search input, window resize, scroll events

---

### 10. Throttle Function

**Problem:** Create a throttle function that executes at most once per specified time period.

```javascript
// Usage: throttle(fn, 300) - fn executes at most once every 300ms
```

**Solution:**

```javascript
function throttle(func, limit) {
  let inThrottle;
  
  return function executedFunction(...args) {
    if (!inThrottle) {
      func(...args);
      inThrottle = true;
      setTimeout(() => inThrottle = false, limit);
    }
  };
}

// Advanced version with trailing call
function throttle2(func, limit) {
  let inThrottle, lastFunc, lastRan;
  
  return function executedFunction(...args) {
    if (!inThrottle) {
      func(...args);
      lastRan = Date.now();
      inThrottle = true;
    } else {
      clearTimeout(lastFunc);
      lastFunc = setTimeout(() => {
        if (Date.now() - lastRan >= limit) {
          func(...args);
          lastRan = Date.now();
        }
      }, Math.max(limit - (Date.now() - lastRan), 0));
    }
  };
}

// Test
const handleScroll = throttle(() => {
  console.log("Scroll event handled");
}, 1000);

window.addEventListener('scroll', handleScroll);
```

**Use Case:** Scroll events, API rate limiting, button clicks

---

### 11. Deep Clone Object

**Problem:** Create a deep copy of an object (including nested objects).

```javascript
// Input: { a: 1, b: { c: 2 } }
// Output: { a: 1, b: { c: 2 } } (new reference)
```

**Solutions:**

```javascript
// Solution 1: Using JSON (limitations: no functions, dates become strings)
function deepClone1(obj) {
  return JSON.parse(JSON.stringify(obj));
}

// Solution 2: Recursive (handles functions, dates)
function deepClone2(obj, hash = new WeakMap()) {
  // Handle primitives
  if (obj === null || typeof obj !== 'object') return obj;
  
  // Handle circular references
  if (hash.has(obj)) return hash.get(obj);
  
  // Handle Date
  if (obj instanceof Date) return new Date(obj);
  
  // Handle Array
  if (obj instanceof Array) {
    const arrCopy = [];
    hash.set(obj, arrCopy);
    obj.forEach((item, index) => {
      arrCopy[index] = deepClone2(item, hash);
    });
    return arrCopy;
  }
  
  // Handle Object
  if (obj instanceof Object) {
    const objCopy = {};
    hash.set(obj, objCopy);
    Object.keys(obj).forEach(key => {
      objCopy[key] = deepClone2(obj[key], hash);
    });
    return objCopy;
  }
  
  throw new Error("Unable to clone object");
}

// Solution 3: Using structuredClone (modern browsers)
function deepClone3(obj) {
  return structuredClone(obj);
}

// Test
const original = {
  a: 1,
  b: { c: 2, d: { e: 3 } },
  f: [1, 2, 3]
};

const cloned = deepClone2(original);
cloned.b.c = 999;
console.log(original.b.c);  // 2 (unchanged)
console.log(cloned.b.c);    // 999
```

**Time Complexity:** O(n)  
**Space Complexity:** O(n)

---

### 12. Curry Function

**Problem:** Transform a function with multiple arguments into a sequence of functions with single arguments.

```javascript
// Input: add(1, 2, 3)
// Output: add(1)(2)(3)
```

**Solution:**

```javascript
// Basic curry
function curry(func) {
  return function curried(...args) {
    if (args.length >= func.length) {
      return func(...args);
    } else {
      return function(...nextArgs) {
        return curried(...args, ...nextArgs);
      };
    }
  };
}

// Usage
function add(a, b, c) {
  return a + b + c;
}

const curriedAdd = curry(add);

console.log(curriedAdd(1)(2)(3));        // 6
console.log(curriedAdd(1, 2)(3));        // 6
console.log(curriedAdd(1)(2, 3));        // 6
console.log(curriedAdd(1, 2, 3));        // 6

// Practical example
function multiply(a, b, c) {
  return a * b * c;
}

const curriedMultiply = curry(multiply);
const multiplyBy2 = curriedMultiply(2);
const multiplyBy2And3 = multiplyBy2(3);

console.log(multiplyBy2And3(4));   // 24
```

**Use Case:** Partial application, functional programming

---

## Polyfill Implementations

### 13. Array.map() Polyfill

**Problem:** Implement Array.prototype.map() from scratch.

**Solution:**

```javascript
Array.prototype.myMap = function(callback, thisArg) {
  if (this == null) {
    throw new TypeError('Array.prototype.myMap called on null or undefined');
  }
  
  if (typeof callback !== 'function') {
    throw new TypeError(callback + ' is not a function');
  }
  
  const result = [];
  const arr = Object(this);
  const len = arr.length >>> 0;  // Convert to unsigned 32-bit integer
  
  for (let i = 0; i < len; i++) {
    if (i in arr) {
      result[i] = callback.call(thisArg, arr[i], i, arr);
    }
  }
  
  return result;
};

// Test
const numbers = [1, 2, 3, 4, 5];
const doubled = numbers.myMap(x => x * 2);
console.log(doubled);  // [2, 4, 6, 8, 10]
```

---

### 14. Array.filter() Polyfill

**Problem:** Implement Array.prototype.filter() from scratch.

**Solution:**

```javascript
Array.prototype.myFilter = function(callback, thisArg) {
  if (this == null) {
    throw new TypeError('Array.prototype.myFilter called on null or undefined');
  }
  
  if (typeof callback !== 'function') {
    throw new TypeError(callback + ' is not a function');
  }
  
  const result = [];
  const arr = Object(this);
  const len = arr.length >>> 0;
  
  for (let i = 0; i < len; i++) {
    if (i in arr) {
      const val = arr[i];
      if (callback.call(thisArg, val, i, arr)) {
        result.push(val);
      }
    }
  }
  
  return result;
};

// Test
const numbers = [1, 2, 3, 4, 5, 6];
const evens = numbers.myFilter(x => x % 2 === 0);
console.log(evens);  // [2, 4, 6]
```

---

### 15. Array.reduce() Polyfill

**Problem:** Implement Array.prototype.reduce() from scratch.

**Solution:**

```javascript
Array.prototype.myReduce = function(callback, initialValue) {
  if (this == null) {
    throw new TypeError('Array.prototype.myReduce called on null or undefined');
  }
  
  if (typeof callback !== 'function') {
    throw new TypeError(callback + ' is not a function');
  }
  
  const arr = Object(this);
  const len = arr.length >>> 0;
  let accumulator;
  let startIndex = 0;
  
  // No initial value provided
  if (arguments.length < 2) {
    if (len === 0) {
      throw new TypeError('Reduce of empty array with no initial value');
    }
    
    // Find first existing element
    while (startIndex < len && !(startIndex in arr)) {
      startIndex++;
    }
    
    accumulator = arr[startIndex];
    startIndex++;
  } else {
    accumulator = initialValue;
  }
  
  for (let i = startIndex; i < len; i++) {
    if (i in arr) {
      accumulator = callback(accumulator, arr[i], i, arr);
    }
  }
  
  return accumulator;
};

// Test
const numbers = [1, 2, 3, 4, 5];
const sum = numbers.myReduce((acc, curr) => acc + curr, 0);
console.log(sum);  // 15
```

---

[Content continues with more challenges...]

---

**[← Back to Interview Prep](./README.md)** | **[Next: Tricky Concepts →](./tricky-concepts.md)**

---

**Made with ❤️ for JavaScript learners**
