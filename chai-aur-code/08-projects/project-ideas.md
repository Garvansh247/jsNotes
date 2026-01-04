# 🎯 15 JavaScript Mini Projects

Build your skills with these practical projects ranging from beginner to intermediate level.

## 📑 Table of Contents
- [Beginner Projects (1-5)](#beginner-projects)
- [Intermediate Projects (6-10)](#intermediate-projects)
- [Advanced Projects (11-15)](#advanced-projects)
- [Project Tips](#-project-tips)

---

## Beginner Projects

### 1. 🎨 Color Flipper

**Description:** Generate random colors and change the background color on button click.

**Skills Practiced:**
- DOM manipulation
- Event listeners
- Math.random()
- Array methods

**Features to Include:**
- Generate random hex colors
- Copy color code to clipboard
- Show color name/code
- Simple/hex color modes

**Code Snippet:**
```javascript
const btn = document.getElementById('btn');
const colorDisplay = document.getElementById('color');

btn.addEventListener('click', function() {
  const randomColor = getRandomColor();
  document.body.style.backgroundColor = randomColor;
  colorDisplay.textContent = randomColor;
});

function getRandomColor() {
  const letters = '0123456789ABCDEF';
  let color = '#';
  for (let i = 0; i < 6; i++) {
    color += letters[Math.floor(Math.random() * 16)];
  }
  return color;
}
```

---

### 2. 🔢 Counter App

**Description:** A simple counter that can increment, decrement, and reset.

**Skills Practiced:**
- Variables and state management
- Event listeners
- Conditional styling
- querySelector

**Features to Include:**
- Increment/Decrement buttons
- Reset button
- Change color based on value (positive=green, negative=red, zero=black)
- Prevent going below zero (optional)

**Code Snippet:**
```javascript
let count = 0;
const value = document.querySelector('#value');
const btns = document.querySelectorAll('.btn');

btns.forEach(function(btn) {
  btn.addEventListener('click', function(e) {
    const styles = e.currentTarget.classList;
    
    if (styles.contains('decrease')) {
      count--;
    } else if (styles.contains('increase')) {
      count++;
    } else {
      count = 0;
    }
    
    // Update color
    if (count > 0) {
      value.style.color = 'green';
    } else if (count < 0) {
      value.style.color = 'red';
    } else {
      value.style.color = 'black';
    }
    
    value.textContent = count;
  });
});
```

---

### 3. ✅ Todo List

**Description:** Create, read, update, and delete todo items.

**Skills Practiced:**
- CRUD operations
- Local storage
- Array methods (map, filter)
- Event delegation

**Features to Include:**
- Add new todos
- Mark as complete
- Delete todos
- Edit todos
- Filter (all/active/completed)
- Persist with localStorage

**Code Snippet:**
```javascript
let todos = JSON.parse(localStorage.getItem('todos')) || [];

function addTodo(text) {
  const todo = {
    id: Date.now(),
    text: text,
    completed: false
  };
  todos.push(todo);
  saveTodos();
  renderTodos();
}

function deleteTodo(id) {
  todos = todos.filter(todo => todo.id !== id);
  saveTodos();
  renderTodos();
}

function toggleTodo(id) {
  todos = todos.map(todo => 
    todo.id === id ? { ...todo, completed: !todo.completed } : todo
  );
  saveTodos();
  renderTodos();
}

function saveTodos() {
  localStorage.setItem('todos', JSON.stringify(todos));
}

function renderTodos() {
  const todoList = document.getElementById('todo-list');
  todoList.innerHTML = '';
  
  todos.forEach(todo => {
    const li = document.createElement('li');
    li.innerHTML = `
      <input type="checkbox" ${todo.completed ? 'checked' : ''} 
        onchange="toggleTodo(${todo.id})">
      <span class="${todo.completed ? 'completed' : ''}">${todo.text}</span>
      <button onclick="deleteTodo(${todo.id})">Delete</button>
    `;
    todoList.appendChild(li);
  });
}

// Initialize
renderTodos();
```

---

### 4. 🕐 Digital Clock

**Description:** Display current time that updates every second.

**Skills Practiced:**
- Date object
- setInterval
- String formatting
- Time manipulation

**Features to Include:**
- Display hours, minutes, seconds
- 12/24 hour format toggle
- Display date
- Different time zones (bonus)

**Code Snippet:**
```javascript
function updateClock() {
  const now = new Date();
  const hours = now.getHours();
  const minutes = now.getMinutes();
  const seconds = now.getSeconds();
  
  // Format with leading zeros
  const formattedTime = [
    hours.toString().padStart(2, '0'),
    minutes.toString().padStart(2, '0'),
    seconds.toString().padStart(2, '0')
  ].join(':');
  
  document.getElementById('clock').textContent = formattedTime;
}

// Update every second
setInterval(updateClock, 1000);
updateClock(); // Initial call
```

---

### 5. 🎲 Guess the Number

**Description:** Random number guessing game with hints.

**Skills Practiced:**
- Math.random()
- Conditional logic
- User input validation
- Game state management

**Features to Include:**
- Generate random number (1-100)
- Input for user guess
- "Too high" / "Too low" hints
- Attempt counter
- Play again button
- High score tracking

**Code Snippet:**
```javascript
let randomNumber = Math.floor(Math.random() * 100) + 1;
let attempts = 0;

function checkGuess() {
  const userGuess = parseInt(document.getElementById('guess').value);
  const message = document.getElementById('message');
  const attemptsDisplay = document.getElementById('attempts');
  
  if (isNaN(userGuess) || userGuess < 1 || userGuess > 100) {
    message.textContent = 'Please enter a valid number between 1 and 100';
    return;
  }
  
  attempts++;
  attemptsDisplay.textContent = `Attempts: ${attempts}`;
  
  if (userGuess === randomNumber) {
    message.textContent = `🎉 Correct! You guessed it in ${attempts} attempts!`;
    message.style.color = 'green';
  } else if (userGuess < randomNumber) {
    message.textContent = '📈 Too low! Try again.';
    message.style.color = 'blue';
  } else {
    message.textContent = '📉 Too high! Try again.';
    message.style.color = 'red';
  }
}

function resetGame() {
  randomNumber = Math.floor(Math.random() * 100) + 1;
  attempts = 0;
  document.getElementById('guess').value = '';
  document.getElementById('message').textContent = '';
  document.getElementById('attempts').textContent = 'Attempts: 0';
}
```

---

## Intermediate Projects

### 6. 💬 Random Quote Generator

**Description:** Display random quotes with ability to share on social media.

**Skills Practiced:**
- Arrays and objects
- Random selection
- Tweet functionality
- Copy to clipboard API

**Features to Include:**
- Display random quote with author
- "New Quote" button
- Tweet quote button
- Copy to clipboard
- Quote categories (optional)

---

### 7. ✔️ Form Validation

**Description:** Validate form inputs with real-time feedback.

**Skills Practiced:**
- Form handling
- Regular expressions
- Event listeners (input, blur)
- Error display

**Features to Include:**
- Required field validation
- Email format validation
- Password strength checker
- Confirm password matching
- Real-time validation feedback

---

### 8. 🖼️ Image Slider

**Description:** Carousel to display images with navigation.

**Skills Practiced:**
- Array manipulation
- setInterval/setTimeout
- Transform CSS with JS
- Touch events (bonus)

**Features to Include:**
- Previous/Next buttons
- Auto-play functionality
- Dot indicators
- Keyboard navigation
- Pause on hover

---

### 9. ⏰ Countdown Timer

**Description:** Timer that counts down to a specific date/time.

**Skills Practiced:**
- Date calculations
- setInterval
- Time formatting
- Timezones

**Features to Include:**
- Set target date
- Display days, hours, minutes, seconds
- "Time's up" message
- Multiple countdowns (optional)

---

### 10. 🧮 Calculator

**Description:** Functional calculator with basic operations.

**Skills Practiced:**
- eval() or manual calculation
- State management
- Error handling
- Keyboard support

**Features to Include:**
- Basic operations (+, -, *, /)
- Clear and backspace
- Decimal support
- Keyboard input
- Operation history

---

## Advanced Projects

### 11. 🌤️ Weather App

**Description:** Fetch and display weather data from API.

**Skills Practiced:**
- Fetch API
- Async/await
- API key management
- Error handling
- JSON parsing

**Features to Include:**
- Search by city name
- Current weather display
- 5-day forecast
- Loading states
- Error messages

**API Suggestion:** OpenWeatherMap API

**Code Snippet:**
```javascript
async function getWeather(city) {
  const apiKey = 'YOUR_API_KEY';
  const url = `https://api.openweathermap.org/data/2.5/weather?q=${city}&appid=${apiKey}&units=metric`;
  
  try {
    const response = await fetch(url);
    if (!response.ok) throw new Error('City not found');
    
    const data = await response.json();
    displayWeather(data);
  } catch (error) {
    console.error('Error:', error);
    displayError(error.message);
  }
}

function displayWeather(data) {
  document.getElementById('city-name').textContent = data.name;
  document.getElementById('temperature').textContent = `${Math.round(data.main.temp)}°C`;
  document.getElementById('description').textContent = data.weather[0].description;
}
```

---

### 12. 🔍 GitHub User Search

**Description:** Search and display GitHub user information.

**Skills Practiced:**
- GitHub API
- Async/await
- Dynamic content rendering
- Profile data display

**Features to Include:**
- Search by username
- Display profile info
- Show repositories list
- Follower/following count
- Handle user not found

**Code Snippet:**
```javascript
async function searchUser(username) {
  const url = `https://api.github.com/users/${username}`;
  
  try {
    const response = await fetch(url);
    if (!response.ok) throw new Error('User not found');
    
    const user = await response.json();
    displayUser(user);
  } catch (error) {
    console.error('Error:', error);
  }
}
```

---

### 13. 📝 Local Storage Notes

**Description:** Note-taking app with local storage persistence.

**Skills Practiced:**
- localStorage API
- CRUD operations
- JSON stringify/parse
- Rich text editing (bonus)

**Features to Include:**
- Create/edit/delete notes
- Search notes
- Categories/tags
- Export notes
- Dark mode toggle

---

### 14. ♾️ Infinite Scroll

**Description:** Load content dynamically as user scrolls.

**Skills Practiced:**
- Scroll events
- IntersectionObserver API
- Pagination
- Performance optimization

**Features to Include:**
- Load more items on scroll
- Loading indicator
- End of content message
- Smooth loading experience

**Code Snippet:**
```javascript
const observer = new IntersectionObserver((entries) => {
  entries.forEach(entry => {
    if (entry.isIntersecting) {
      loadMoreContent();
    }
  });
}, {
  threshold: 1.0
});

const sentinel = document.getElementById('sentinel');
observer.observe(sentinel);

function loadMoreContent() {
  // Fetch and append more items
}
```

---

### 15. 🌙 Dark Mode Toggle

**Description:** Implement dark mode with user preference persistence.

**Skills Practiced:**
- CSS variables
- localStorage
- Theme switching
- System preference detection

**Features to Include:**
- Toggle button
- Save preference
- Detect system preference
- Smooth transition
- Custom themes (bonus)

**Code Snippet:**
```javascript
const toggle = document.getElementById('theme-toggle');
const currentTheme = localStorage.getItem('theme') || 'light';

document.documentElement.setAttribute('data-theme', currentTheme);

toggle.addEventListener('click', () => {
  const theme = document.documentElement.getAttribute('data-theme');
  const newTheme = theme === 'light' ? 'dark' : 'light';
  
  document.documentElement.setAttribute('data-theme', newTheme);
  localStorage.setItem('theme', newTheme);
});
```

---

## 🎯 Project Tips

### Getting Started
1. **Plan First**: Sketch UI and list features
2. **Start Simple**: Basic version first, add features later
3. **Commit Often**: Version control your progress
4. **Test Thoroughly**: Try different inputs and edge cases

### Best Practices
- ✅ Use semantic HTML
- ✅ Write clean, readable code
- ✅ Add comments for complex logic
- ✅ Handle errors gracefully
- ✅ Make it responsive
- ✅ Optimize performance
- ✅ Accessibility (a11y) considerations

### Learning Approach
1. **Build without tutorial**: Try on your own first
2. **Stuck? Research**: Google, MDN, Stack Overflow
3. **Compare solutions**: See how others solved it
4. **Refactor**: Improve your code after it works
5. **Add features**: Extend functionality

### Portfolio Tips
- 🎨 Make it look professional (CSS matters!)
- 📱 Ensure mobile responsiveness
- 🚀 Deploy (Netlify, Vercel, GitHub Pages)
- 📝 Write good README with demo link
- 💻 Clean, well-structured code
- ✨ Add unique features to stand out

---

## 🚀 Next Steps

After completing these projects:
1. **Build something original**: Combine concepts
2. **Contribute to open source**: Real-world experience
3. **Start a bigger project**: Multi-page application
4. **Learn a framework**: React, Vue, or Angular
5. **Build full-stack**: Add backend (Node.js)

---

**[← Back to Chai aur Code](../README.md)** | **[← Back to Main README](../../README.md)**

---

**Happy Building! 🚀✨**
