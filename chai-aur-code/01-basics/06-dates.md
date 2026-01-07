# 📅 Dates in JavaScript

## 📑 Table of Contents
- [Date Basics](#date-basics)
- [Creating Dates](#creating-dates)
- [Date Methods](#date-methods)
- [Getting Date Components](#getting-date-components)
- [Setting Date Components](#setting-date-components)
- [Date Formatting](#date-formatting)
- [Date Calculations](#date-calculations)
- [Timezones](#timezones)
- [Common Mistakes](#-common-mistakes)
- [Interview Tips](#-interview-tips)
- [Practice Exercises](#practice-exercises)

---

## Date Basics

JavaScript Date objects represent a single moment in time. Internally, dates are stored as milliseconds since January 1, 1970, 00:00:00 UTC (Unix Epoch).

```javascript
// Current date and time
let now = new Date();
console.log(now); // e.g., 2024-01-15T10:30:00.000Z

// Date as milliseconds since epoch
console.log(now.getTime()); // e.g., 1705315800000

// Epoch start
let epoch = new Date(0);
console.log(epoch); // 1970-01-01T00:00:00.000Z
```

---

## Creating Dates

### Different Ways to Create Dates

```javascript
// 1. Current date and time
let now = new Date();
console.log(now);

// 2. From date string
let date1 = new Date("2024-01-15");
console.log(date1); // 2024-01-15T00:00:00.000Z

let date2 = new Date("January 15, 2024");
console.log(date2);

let date3 = new Date("2024-01-15T10:30:00");
console.log(date3);

// 3. From milliseconds (since epoch)
let date4 = new Date(1705315800000);
console.log(date4);

// 4. From individual components (year, month, day, hour, minute, second, ms)
// Note: Month is 0-indexed (0 = January, 11 = December)
let date5 = new Date(2024, 0, 15); // Jan 15, 2024
console.log(date5);

let date6 = new Date(2024, 0, 15, 10, 30, 0); // Jan 15, 2024, 10:30:00
console.log(date6);

let date7 = new Date(2024, 0, 15, 10, 30, 45, 500); // Including milliseconds
console.log(date7);

// 5. Using Date.parse() - returns milliseconds
let ms = Date.parse("2024-01-15");
let date8 = new Date(ms);
console.log(date8);

// 6. Copy existing date
let original = new Date();
let copy = new Date(original);
console.log(copy);
```

### Invalid Dates

```javascript
// Invalid date strings return "Invalid Date"
let invalid1 = new Date("invalid");
console.log(invalid1); // Invalid Date

// Check if date is valid
function isValidDate(date) {
  return date instanceof Date && !isNaN(date);
}

console.log(isValidDate(new Date())); // true
console.log(isValidDate(new Date("invalid"))); // false

// Another way to check
let date = new Date("2024-01-15");
console.log(date.toString()); // Valid date string
console.log(new Date("invalid").toString()); // "Invalid Date"
```

### Date.now()

```javascript
// Get current timestamp (more efficient than new Date().getTime())
let timestamp = Date.now();
console.log(timestamp); // e.g., 1705315800000

// Practical use: measuring time
let start = Date.now();
// ... some operation ...
let end = Date.now();
console.log(`Operation took ${end - start}ms`);
```

---

## Date Methods

### Converting to Different Formats

```javascript
let date = new Date("2024-01-15T10:30:00");

// toString() - full string representation
console.log(date.toString());
// "Mon Jan 15 2024 10:30:00 GMT+0000 (Coordinated Universal Time)"

// toDateString() - date only
console.log(date.toDateString());
// "Mon Jan 15 2024"

// toTimeString() - time only
console.log(date.toTimeString());
// "10:30:00 GMT+0000 (Coordinated Universal Time)"

// toISOString() - ISO 8601 format
console.log(date.toISOString());
// "2024-01-15T10:30:00.000Z"

// toJSON() - same as toISOString()
console.log(date.toJSON());
// "2024-01-15T10:30:00.000Z"

// toUTCString() - UTC format
console.log(date.toUTCString());
// "Mon, 15 Jan 2024 10:30:00 GMT"

// toLocaleString() - locale-specific format
console.log(date.toLocaleString());
// e.g., "1/15/2024, 10:30:00 AM"

// toLocaleDateString() - locale date only
console.log(date.toLocaleDateString());
// e.g., "1/15/2024"

// toLocaleTimeString() - locale time only
console.log(date.toLocaleTimeString());
// e.g., "10:30:00 AM"

// valueOf() / getTime() - milliseconds since epoch
console.log(date.valueOf());
console.log(date.getTime());
// 1705315800000
```

---

## Getting Date Components

### Get Components (Local Time)

```javascript
let date = new Date("2024-01-15T10:30:45.500");

// Year
console.log(date.getFullYear()); // 2024
// Note: getYear() is deprecated, always use getFullYear()

// Month (0-11, 0 = January)
console.log(date.getMonth()); // 0 (January)

// Month name
const months = ["Jan", "Feb", "Mar", "Apr", "May", "Jun",
                "Jul", "Aug", "Sep", "Oct", "Nov", "Dec"];
console.log(months[date.getMonth()]); // "Jan"

// Date (day of month, 1-31)
console.log(date.getDate()); // 15

// Day of week (0-6, 0 = Sunday)
console.log(date.getDay()); // 1 (Monday)

// Day name
const days = ["Sun", "Mon", "Tue", "Wed", "Thu", "Fri", "Sat"];
console.log(days[date.getDay()]); // "Mon"

// Hours (0-23)
console.log(date.getHours()); // 10

// Minutes (0-59)
console.log(date.getMinutes()); // 30

// Seconds (0-59)
console.log(date.getSeconds()); // 45

// Milliseconds (0-999)
console.log(date.getMilliseconds()); // 500

// Timestamp (ms since epoch)
console.log(date.getTime()); // 1705315845500

// Timezone offset in minutes
console.log(date.getTimezoneOffset()); // e.g., 0 (UTC), -300 (EST)
```

### Get Components (UTC)

```javascript
let date = new Date("2024-01-15T10:30:45.500Z");

console.log(date.getUTCFullYear()); // 2024
console.log(date.getUTCMonth()); // 0
console.log(date.getUTCDate()); // 15
console.log(date.getUTCDay()); // 1
console.log(date.getUTCHours()); // 10
console.log(date.getUTCMinutes()); // 30
console.log(date.getUTCSeconds()); // 45
console.log(date.getUTCMilliseconds()); // 500
```

---

## Setting Date Components

### Set Components (Local Time)

```javascript
let date = new Date("2024-01-15T10:30:00");

// Set year
date.setFullYear(2025);
console.log(date); // 2025-01-15T10:30:00

// Set month (0-11)
date.setMonth(5); // June
console.log(date); // 2025-06-15T10:30:00

// Set date (day of month)
date.setDate(25);
console.log(date); // 2025-06-25T10:30:00

// Set hours
date.setHours(15);
console.log(date); // 2025-06-25T15:30:00

// Set minutes
date.setMinutes(45);
console.log(date); // 2025-06-25T15:45:00

// Set seconds
date.setSeconds(30);
console.log(date); // 2025-06-25T15:45:30

// Set milliseconds
date.setMilliseconds(500);
console.log(date); // 2025-06-25T15:45:30.500

// Set timestamp
date.setTime(1705315800000);
console.log(date); // 2024-01-15T10:30:00.000
```

### Set Multiple Components at Once

```javascript
let date = new Date();

// setFullYear(year, month, day)
date.setFullYear(2024, 0, 15);
console.log(date); // Jan 15, 2024

// setMonth(month, day)
date.setMonth(5, 25);
console.log(date); // Jun 25, 2024

// setHours(hours, minutes, seconds, ms)
date.setHours(10, 30, 0, 0);
console.log(date); // Jun 25, 2024, 10:30:00.000

// setMinutes(minutes, seconds, ms)
date.setMinutes(45, 30, 500);
console.log(date); // Jun 25, 2024, 10:45:30.500

// setSeconds(seconds, ms)
date.setSeconds(15, 250);
console.log(date); // Jun 25, 2024, 10:45:15.250
```

### Set Components (UTC)

```javascript
let date = new Date();

date.setUTCFullYear(2024);
date.setUTCMonth(0);
date.setUTCDate(15);
date.setUTCHours(10);
date.setUTCMinutes(30);
date.setUTCSeconds(0);
date.setUTCMilliseconds(0);

console.log(date.toISOString()); // 2024-01-15T10:30:00.000Z
```

### Auto-correction

```javascript
// JavaScript auto-corrects out-of-range values
let date = new Date(2024, 0, 1);

// Set date to 32 (Jan only has 31 days)
date.setDate(32);
console.log(date.toDateString()); // "Thu Feb 01 2024" (auto-corrects to Feb 1)

// Set month to 12 (goes to next year)
date = new Date(2024, 0, 15);
date.setMonth(12);
console.log(date.toDateString()); // "Wed Jan 15 2025"

// Negative values go backwards
date = new Date(2024, 0, 15);
date.setDate(0); // Goes to last day of previous month
console.log(date.toDateString()); // "Sun Dec 31 2023"

date = new Date(2024, 0, 15);
date.setDate(-1); // Goes back 2 days from start of month
console.log(date.toDateString()); // "Sat Dec 30 2023"
```

---

## Date Formatting

### Basic Formatting

```javascript
let date = new Date("2024-01-15T10:30:00");

// Manual formatting
function formatDate(date) {
  let day = String(date.getDate()).padStart(2, '0');
  let month = String(date.getMonth() + 1).padStart(2, '0');
  let year = date.getFullYear();
  return `${day}/${month}/${year}`;
}
console.log(formatDate(date)); // "15/01/2024"

// Time formatting
function formatTime(date) {
  let hours = String(date.getHours()).padStart(2, '0');
  let minutes = String(date.getMinutes()).padStart(2, '0');
  let seconds = String(date.getSeconds()).padStart(2, '0');
  return `${hours}:${minutes}:${seconds}`;
}
console.log(formatTime(date)); // "10:30:00"

// DateTime formatting
function formatDateTime(date) {
  return `${formatDate(date)} ${formatTime(date)}`;
}
console.log(formatDateTime(date)); // "15/01/2024 10:30:00"
```

### Locale-Specific Formatting

```javascript
let date = new Date("2024-01-15T10:30:00");

// Different locales
console.log(date.toLocaleString('en-US'));
// "1/15/2024, 10:30:00 AM"

console.log(date.toLocaleString('en-GB'));
// "15/01/2024, 10:30:00"

console.log(date.toLocaleString('de-DE'));
// "15.1.2024, 10:30:00"

console.log(date.toLocaleString('ja-JP'));
// "2024/1/15 10:30:00"

// With options
let options = {
  weekday: 'long',
  year: 'numeric',
  month: 'long',
  day: 'numeric',
  hour: '2-digit',
  minute: '2-digit'
};

console.log(date.toLocaleString('en-US', options));
// "Monday, January 15, 2024, 10:30 AM"

console.log(date.toLocaleString('fr-FR', options));
// "lundi 15 janvier 2024, 10:30"

// Date only with options
let dateOptions = {
  weekday: 'short',
  year: 'numeric',
  month: 'short',
  day: 'numeric'
};

console.log(date.toLocaleDateString('en-US', dateOptions));
// "Mon, Jan 15, 2024"

// Time only with options
let timeOptions = {
  hour: '2-digit',
  minute: '2-digit',
  second: '2-digit',
  hour12: false
};

console.log(date.toLocaleTimeString('en-US', timeOptions));
// "10:30:00"
```

### Custom Formatting Function

```javascript
function formatDate(date, format) {
  const map = {
    'YYYY': date.getFullYear(),
    'YY': String(date.getFullYear()).slice(-2),
    'MM': String(date.getMonth() + 1).padStart(2, '0'),
    'M': date.getMonth() + 1,
    'DD': String(date.getDate()).padStart(2, '0'),
    'D': date.getDate(),
    'HH': String(date.getHours()).padStart(2, '0'),
    'H': date.getHours(),
    'hh': String(date.getHours() % 12 || 12).padStart(2, '0'),
    'h': date.getHours() % 12 || 12,
    'mm': String(date.getMinutes()).padStart(2, '0'),
    'm': date.getMinutes(),
    'ss': String(date.getSeconds()).padStart(2, '0'),
    's': date.getSeconds(),
    'A': date.getHours() >= 12 ? 'PM' : 'AM',
    'a': date.getHours() >= 12 ? 'pm' : 'am'
  };
  
  return format.replace(/YYYY|YY|MM|M|DD|D|HH|H|hh|h|mm|m|ss|s|A|a/g, 
    match => map[match]);
}

let date = new Date("2024-01-15T14:30:45");

console.log(formatDate(date, 'YYYY-MM-DD')); // "2024-01-15"
console.log(formatDate(date, 'DD/MM/YYYY')); // "15/01/2024"
console.log(formatDate(date, 'HH:mm:ss')); // "14:30:45"
console.log(formatDate(date, 'hh:mm A')); // "02:30 PM"
console.log(formatDate(date, 'YYYY-MM-DD HH:mm:ss')); // "2024-01-15 14:30:45"
```

---

## Date Calculations

### Adding/Subtracting Time

```javascript
let date = new Date("2024-01-15T10:30:00");

// Add days
function addDays(date, days) {
  let result = new Date(date);
  result.setDate(result.getDate() + days);
  return result;
}
console.log(addDays(date, 7)); // 7 days later

// Add months
function addMonths(date, months) {
  let result = new Date(date);
  result.setMonth(result.getMonth() + months);
  return result;
}
console.log(addMonths(date, 3)); // 3 months later

// Add years
function addYears(date, years) {
  let result = new Date(date);
  result.setFullYear(result.getFullYear() + years);
  return result;
}
console.log(addYears(date, 2)); // 2 years later

// Add hours
function addHours(date, hours) {
  let result = new Date(date);
  result.setHours(result.getHours() + hours);
  return result;
}
console.log(addHours(date, 5)); // 5 hours later

// Add minutes
function addMinutes(date, minutes) {
  return new Date(date.getTime() + minutes * 60000);
}
console.log(addMinutes(date, 30)); // 30 minutes later

// Subtract (use negative values)
console.log(addDays(date, -7)); // 7 days ago
console.log(addMonths(date, -3)); // 3 months ago
```

### Difference Between Dates

```javascript
let date1 = new Date("2024-01-15");
let date2 = new Date("2024-01-20");

// Difference in milliseconds
let diffMs = date2 - date1;
console.log(diffMs); // 432000000

// Difference in seconds
let diffSeconds = diffMs / 1000;
console.log(diffSeconds); // 432000

// Difference in minutes
let diffMinutes = diffSeconds / 60;
console.log(diffMinutes); // 7200

// Difference in hours
let diffHours = diffMinutes / 60;
console.log(diffHours); // 120

// Difference in days
let diffDays = diffHours / 24;
console.log(diffDays); // 5

// Function to get difference
function getDaysDifference(date1, date2) {
  const oneDay = 24 * 60 * 60 * 1000; // milliseconds in a day
  return Math.round(Math.abs((date1 - date2) / oneDay));
}
console.log(getDaysDifference(date1, date2)); // 5

// Age calculator
function calculateAge(birthDate) {
  let today = new Date();
  let birth = new Date(birthDate);
  let age = today.getFullYear() - birth.getFullYear();
  let monthDiff = today.getMonth() - birth.getMonth();
  
  if (monthDiff < 0 || (monthDiff === 0 && today.getDate() < birth.getDate())) {
    age--;
  }
  
  return age;
}
console.log(calculateAge("1990-05-15")); // e.g., 33
```

### Comparing Dates

```javascript
let date1 = new Date("2024-01-15");
let date2 = new Date("2024-01-20");
let date3 = new Date("2024-01-15");

// Comparison operators
console.log(date1 < date2); // true
console.log(date1 > date2); // false
console.log(date1 <= date3); // true
console.log(date1 >= date3); // true

// Equality (be careful!)
console.log(date1 == date3); // false (different objects)
console.log(date1 === date3); // false (different objects)

// Compare timestamps instead
console.log(date1.getTime() === date3.getTime()); // true

// Helper function
function isSameDay(date1, date2) {
  return date1.getFullYear() === date2.getFullYear() &&
         date1.getMonth() === date2.getMonth() &&
         date1.getDate() === date2.getDate();
}
console.log(isSameDay(date1, date3)); // true

// Check if date is in the past
function isInPast(date) {
  return date < new Date();
}

// Check if date is in the future
function isInFuture(date) {
  return date > new Date();
}

// Check if date is today
function isToday(date) {
  return isSameDay(date, new Date());
}
```

### Working Days Calculator

```javascript
function isWeekend(date) {
  const day = date.getDay();
  return day === 0 || day === 6; // Sunday or Saturday
}

function getWorkingDays(startDate, endDate) {
  let count = 0;
  let current = new Date(startDate);
  
  while (current <= endDate) {
    if (!isWeekend(current)) {
      count++;
    }
    current.setDate(current.getDate() + 1);
  }
  
  return count;
}

let start = new Date("2024-01-15");
let end = new Date("2024-01-20");
console.log(getWorkingDays(start, end)); // Working days between dates
```

---

## Timezones

### Understanding Timezone Offset

```javascript
let date = new Date();

// Get timezone offset in minutes
let offset = date.getTimezoneOffset();
console.log(offset); // e.g., 0 (UTC), -300 (EST), 330 (IST)

// Convert to hours
let offsetHours = -offset / 60;
console.log(`UTC ${offsetHours >= 0 ? '+' : ''}${offsetHours}`);
// e.g., "UTC+0", "UTC-5", "UTC+5.5"

// Get timezone name (approximate)
let timezoneName = Intl.DateTimeFormat().resolvedOptions().timeZone;
console.log(timezoneName); // e.g., "America/New_York", "Asia/Kolkata"
```

### Working with Different Timezones

```javascript
let date = new Date("2024-01-15T10:30:00");

// Format with specific timezone
console.log(date.toLocaleString('en-US', { 
  timeZone: 'America/New_York' 
})); // Eastern Time

console.log(date.toLocaleString('en-US', { 
  timeZone: 'America/Los_Angeles' 
})); // Pacific Time

console.log(date.toLocaleString('en-US', { 
  timeZone: 'Asia/Kolkata' 
})); // Indian Time

console.log(date.toLocaleString('en-US', { 
  timeZone: 'Europe/London' 
})); // British Time

console.log(date.toLocaleString('en-US', { 
  timeZone: 'Asia/Tokyo' 
})); // Japan Time
```

### UTC vs Local Time

```javascript
// Current time
let now = new Date();

console.log("Local:", now.toString());
console.log("UTC:", now.toUTCString());
console.log("ISO:", now.toISOString());

// Create date in UTC
let utcDate = new Date(Date.UTC(2024, 0, 15, 10, 30, 0));
console.log(utcDate.toISOString()); // "2024-01-15T10:30:00.000Z"

// Convert local to UTC
function localToUTC(date) {
  return new Date(date.getTime() + date.getTimezoneOffset() * 60000);
}

// Convert UTC to local
function utcToLocal(date) {
  return new Date(date.getTime() - date.getTimezoneOffset() * 60000);
}
```

---

## ⚠️ Common Mistakes

### 1. Month is 0-indexed

```javascript
// ❌ Wrong: Thinking January is 1
let wrong = new Date(2024, 1, 15); // This is February 15!
console.log(wrong.toDateString()); // "Thu Feb 15 2024"

// ✓ Correct: January is 0
let correct = new Date(2024, 0, 15); // This is January 15
console.log(correct.toDateString()); // "Mon Jan 15 2024"
```

### 2. Comparing Date Objects

```javascript
let date1 = new Date("2024-01-15");
let date2 = new Date("2024-01-15");

// ❌ Wrong: Comparing objects
console.log(date1 == date2); // false
console.log(date1 === date2); // false

// ✓ Correct: Compare timestamps
console.log(date1.getTime() === date2.getTime()); // true
console.log(+date1 === +date2); // true
```

### 3. Modifying Date Objects

```javascript
let date = new Date("2024-01-15");

// ❌ Wrong: Thinking methods return new date
date.setDate(20);
console.log(date); // Original date is modified!

// ✓ Correct: Create a copy first
let original = new Date("2024-01-15");
let modified = new Date(original);
modified.setDate(20);
console.log(original); // Unchanged
console.log(modified); // Changed
```

### 4. Date String Parsing

```javascript
// ❌ Wrong: Ambiguous date strings
let ambiguous = new Date("01/02/2024"); // Is it Jan 2 or Feb 1?

// ✓ Correct: Use ISO format
let clear = new Date("2024-01-02"); // Definitely Jan 2, 2024

// Or use individual components
let explicit = new Date(2024, 0, 2); // Jan 2, 2024
```

### 5. Timezone Confusion

```javascript
// When you create a date, be aware of timezone
let date1 = new Date("2024-01-15"); // Treated as UTC midnight
let date2 = new Date(2024, 0, 15); // Treated as local midnight

console.log(date1.toISOString()); // "2024-01-15T00:00:00.000Z"
console.log(date2.toISOString()); // May show different time depending on timezone
```

---

## 💼 Interview Tips

### Q1: How do you get the number of days in a month?

**Answer:**
```javascript
function getDaysInMonth(year, month) {
  // Set date to day 0 of next month (last day of current month)
  return new Date(year, month + 1, 0).getDate();
}

console.log(getDaysInMonth(2024, 0)); // 31 (January)
console.log(getDaysInMonth(2024, 1)); // 29 (February - leap year)
console.log(getDaysInMonth(2023, 1)); // 28 (February - not leap year)
```

### Q2: How do you check if a year is a leap year?

**Answer:**
```javascript
function isLeapYear(year) {
  // Divisible by 4, except century years (unless divisible by 400)
  return (year % 4 === 0 && year % 100 !== 0) || (year % 400 === 0);
}

console.log(isLeapYear(2024)); // true
console.log(isLeapYear(2023)); // false
console.log(isLeapYear(2000)); // true (divisible by 400)
console.log(isLeapYear(1900)); // false (century year not divisible by 400)

// Alternative using Date
function isLeapYear2(year) {
  return new Date(year, 1, 29).getDate() === 29;
}
```

### Q3: How do you format a date as "YYYY-MM-DD"?

**Answer:**
```javascript
function formatDate(date) {
  let year = date.getFullYear();
  let month = String(date.getMonth() + 1).padStart(2, '0');
  let day = String(date.getDate()).padStart(2, '0');
  return `${year}-${month}-${day}`;
}

let date = new Date("2024-01-05");
console.log(formatDate(date)); // "2024-01-05"

// Alternative using toISOString
function formatDate2(date) {
  return date.toISOString().split('T')[0];
}
console.log(formatDate2(date)); // "2024-01-05"
```

### Q4: How do you calculate the difference between two dates in days?

**Answer:**
```javascript
function getDaysDifference(date1, date2) {
  const oneDay = 24 * 60 * 60 * 1000; // ms in a day
  const diffMs = Math.abs(date2 - date1);
  return Math.floor(diffMs / oneDay);
}

let start = new Date("2024-01-01");
let end = new Date("2024-01-15");
console.log(getDaysDifference(start, end)); // 14

// More precise (accounting for DST)
function getDaysDifference2(date1, date2) {
  const utc1 = Date.UTC(date1.getFullYear(), date1.getMonth(), date1.getDate());
  const utc2 = Date.UTC(date2.getFullYear(), date2.getMonth(), date2.getDate());
  return Math.floor((utc2 - utc1) / (24 * 60 * 60 * 1000));
}
```

### Q5: Why is month 0-indexed but day and year are not?

**Answer:**
This is a legacy decision from Java's Date class (JavaScript's Date was modeled after it). Months are 0-indexed (0-11) for consistency with arrays, as month names can be stored in an array and accessed by index. However, days (1-31) and years use their natural values for better readability and to match how we write dates in real life. While inconsistent, this has been maintained for backward compatibility.

---

## Practice Exercises

### Exercise 1: Date Formatter
Create a function that formats a date in multiple ways.

```javascript
function formatMultipleWays(date) {
  // Return object with different formats
  // {
  //   iso: "2024-01-15",
  //   us: "01/15/2024",
  //   eu: "15/01/2024",
  //   long: "Monday, January 15, 2024"
  // }
}
```

<details>
<summary>Solution</summary>

```javascript
function formatMultipleWays(date) {
  const year = date.getFullYear();
  const month = String(date.getMonth() + 1).padStart(2, '0');
  const day = String(date.getDate()).padStart(2, '0');
  
  const days = ['Sunday', 'Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday', 'Saturday'];
  const months = ['January', 'February', 'March', 'April', 'May', 'June',
                  'July', 'August', 'September', 'October', 'November', 'December'];
  
  return {
    iso: `${year}-${month}-${day}`,
    us: `${month}/${day}/${year}`,
    eu: `${day}/${month}/${year}`,
    long: `${days[date.getDay()]}, ${months[date.getMonth()]} ${date.getDate()}, ${year}`
  };
}

let date = new Date("2024-01-15");
console.log(formatMultipleWays(date));
```
</details>

### Exercise 2: Get Week Number
Write a function to get the ISO week number of a date.

```javascript
function getWeekNumber(date) {
  // Your code here
}

console.log(getWeekNumber(new Date("2024-01-15"))); // Week number
```

<details>
<summary>Solution</summary>

```javascript
function getWeekNumber(date) {
  const d = new Date(Date.UTC(date.getFullYear(), date.getMonth(), date.getDate()));
  const dayNum = d.getUTCDay() || 7;
  d.setUTCDate(d.getUTCDate() + 4 - dayNum);
  const yearStart = new Date(Date.UTC(d.getUTCFullYear(), 0, 1));
  return Math.ceil((((d - yearStart) / 86400000) + 1) / 7);
}

console.log(getWeekNumber(new Date("2024-01-15"))); // 3
```
</details>

### Exercise 3: Countdown Timer
Create a function that returns time remaining until a target date.

```javascript
function countdown(targetDate) {
  // Return object with days, hours, minutes, seconds remaining
}

let target = new Date("2024-12-31");
console.log(countdown(target));
```

<details>
<summary>Solution</summary>

```javascript
function countdown(targetDate) {
  const now = new Date();
  const diff = targetDate - now;
  
  if (diff <= 0) {
    return { days: 0, hours: 0, minutes: 0, seconds: 0 };
  }
  
  return {
    days: Math.floor(diff / (1000 * 60 * 60 * 24)),
    hours: Math.floor((diff % (1000 * 60 * 60 * 24)) / (1000 * 60 * 60)),
    minutes: Math.floor((diff % (1000 * 60 * 60)) / (1000 * 60)),
    seconds: Math.floor((diff % (1000 * 60)) / 1000)
  };
}

let target = new Date("2024-12-31");
console.log(countdown(target));
```
</details>

---

**[← Back: Numbers and Math](./05-numbers-and-math.md)** | **[Next: Arrays and Objects →](../02-arrays-and-objects/01-arrays.md)**

---

**Made with ❤️ for JavaScript learners**
