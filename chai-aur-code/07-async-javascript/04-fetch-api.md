# 🌐 Fetch API in JavaScript

## 📑 Table of Contents
- [Basic Fetch](#basic-fetch)
- [HTTP Methods](#http-methods)
- [Handling Responses](#handling-responses)
- [Error Handling](#error-handling)
- [Practical Examples](#practical-examples)
- [Common Mistakes](#-common-mistakes)
- [Interview Tips](#-interview-tips)

---

## Basic Fetch

```javascript
// GET request
fetch('https://api.example.com/users')
  .then(response => response.json())
  .then(data => console.log(data))
  .catch(error => console.error(error));

// With async/await
async function getUsers() {
  try {
    const response = await fetch('https://api.example.com/users');
    const data = await response.json();
    return data;
  } catch (error) {
    console.error('Error:', error);
  }
}
```

---

## HTTP Methods

```javascript
// GET (default)
fetch('https://api.example.com/users')

// POST
fetch('https://api.example.com/users', {
  method: 'POST',
  headers: {
    'Content-Type': 'application/json'
  },
  body: JSON.stringify({
    name: 'John',
    email: 'john@example.com'
  })
})

// PUT
fetch('https://api.example.com/users/1', {
  method: 'PUT',
  headers: {
    'Content-Type': 'application/json'
  },
  body: JSON.stringify({
    name: 'John Updated'
  })
})

// DELETE
fetch('https://api.example.com/users/1', {
  method: 'DELETE'
})
```

---

## Handling Responses

```javascript
async function getData() {
  const response = await fetch('https://api.example.com/data');
  
  // Check if response is OK
  if (!response.ok) {
    throw new Error(`HTTP error! status: ${response.status}`);
  }
  
  // Parse JSON
  const data = await response.json();
  
  // Other formats:
  // const text = await response.text();
  // const blob = await response.blob();
  // const formData = await response.formData();
  
  return data;
}
```

---

## Error Handling

```javascript
async function fetchData() {
  try {
    const response = await fetch('https://api.example.com/data');
    
    if (!response.ok) {
      throw new Error(`HTTP error! status: ${response.status}`);
    }
    
    const data = await response.json();
    return data;
  } catch (error) {
    if (error.name === 'TypeError') {
      console.error('Network error:', error);
    } else {
      console.error('Error:', error);
    }
    throw error;
  }
}
```

---

## Practical Examples

```javascript
// POST with JSON
async function createUser(userData) {
  const response = await fetch('https://api.example.com/users', {
    method: 'POST',
    headers: {
      'Content-Type': 'application/json',
      'Authorization': 'Bearer token123'
    },
    body: JSON.stringify(userData)
  });
  
  if (!response.ok) {
    throw new Error('Failed to create user');
  }
  
  return response.json();
}

// Usage
createUser({name: 'John', email: 'john@example.com'})
  .then(user => console.log('Created:', user))
  .catch(error => console.error('Error:', error));
```

---

## ⚠️ Common Mistakes

```javascript
// ❌ Not checking response.ok
fetch('url')
  .then(response => response.json())  // Might not be JSON if error!
  .then(data => console.log(data));

// ✓ Check response.ok
fetch('url')
  .then(response => {
    if (!response.ok) {
      throw new Error('HTTP error');
    }
    return response.json();
  })
  .then(data => console.log(data));

// ❌ Forgetting Content-Type header
fetch('url', {
  method: 'POST',
  body: JSON.stringify(data)  // Missing header!
});

// ✓ Include Content-Type
fetch('url', {
  method: 'POST',
  headers: {
    'Content-Type': 'application/json'
  },
  body: JSON.stringify(data)
});
```

---

## 💼 Interview Tips

### Q1: What is the Fetch API?

**Answer:**
A modern API for making HTTP requests. It returns Promises and provides a cleaner interface than XMLHttpRequest.

### Q2: How do you handle errors with fetch?

**Answer:**
Check `response.ok` and use try/catch:

```javascript
try {
  const response = await fetch('url');
  if (!response.ok) {
    throw new Error(`HTTP error! status: ${response.status}`);
  }
  const data = await response.json();
} catch (error) {
  console.error('Error:', error);
}
```

### Q3: What are common fetch options?

**Answer:**
- `method`: HTTP method (GET, POST, PUT, DELETE)
- `headers`: Request headers
- `body`: Request body (for POST/PUT)
- `mode`: CORS mode
- `credentials`: Include cookies

---

**[← Back: Async/Await](./03-async-await.md)** | **[Complete! 🎉](#)**

---

**Made with ❤️ for JavaScript learners**
