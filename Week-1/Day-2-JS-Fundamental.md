# Day 2 — JavaScript Fundamentals II

## Topic: Arrays, Objects, ES6+ & Async

### Q16. What is destructuring in JavaScript? Explain with array and object examples.

### Answer

**Destructuring** is a JavaScript feature that allows us to extract values from arrays or properties from objects and assign them to variables easily.

#### Array Destructuring

```javascript
const numbers = [10, 20, 30];

const [first, second, third] = numbers;

console.log(first);  // 10
console.log(second); // 20
console.log(third);  // 30
```

#### Object Destructuring

```javascript
const user = {
    name: "Imon",
    age: 23,
    city: "Chattogram"
};

const { name, age, city } = user;

console.log(name); // Imon
console.log(age);  // 23
console.log(city); // Chattogram
```

#### Interview Tip

Destructuring makes code **shorter, cleaner, and easier to read**. It is commonly used in React, especially when working with props and objects.

---

### Q17. What are the spread and rest operators and how are they used?

### Answer

The **spread (`...`)** and **rest (`...`)** operators use the same syntax, but they have different purposes.

- **Spread** → expands elements of an array or properties of an object.
- **Rest** → collects multiple values into a single array.

#### Spread Operator

```javascript
const numbers = [1, 2, 3];
const newNumbers = [...numbers, 4, 5];

console.log(newNumbers);
// [1, 2, 3, 4, 5]
```

For objects:

```javascript
const user = {
    name: "Imon",
    age: 23
};

const updatedUser = {
    ...user,
    city: "Chattogram"
};

console.log(updatedUser);
// { name: "Imon", age: 23, city: "Chattogram" }
```

#### Rest Operator

```javascript
function sum(...numbers) {
    return numbers.reduce((total, num) => total + num, 0);
}

console.log(sum(10, 20, 30));
// 60
```

Here, `...numbers` collects all arguments into an array.

### Interview Tip

Remember:

**Spread → Expand**

**Rest → Collect**

---

### Q18. Explain the difference between `map()`, `filter()`, and `reduce()`.

### Answer

All three are commonly used array methods, but they have different purposes.

| Method | Purpose | Returns |
|---|---|---|
| `map()` | Transform every element | New array |
| `filter()` | Select elements based on a condition | New array |
| `reduce()` | Combine elements into a single value | Single value |

#### `map()`

Used when you want to **transform every element**.

```javascript
const numbers = [1, 2, 3, 4];

const doubled = numbers.map(num => num * 2);

console.log(doubled);
// [2, 4, 6, 8]
```

#### `filter()`

Used when you want to **select specific elements**.

```javascript
const numbers = [1, 2, 3, 4, 5];

const evenNumbers = numbers.filter(num => num % 2 === 0);

console.log(evenNumbers);
// [2, 4]
```

#### `reduce()`

Used when you want to **combine all elements into one value**.

```javascript
const numbers = [1, 2, 3, 4];

const sum = numbers.reduce((total, num) => total + num, 0);

console.log(sum);
// 10
```

### Interview Tip

Easy way to remember:

```text
map()    → Transform
filter() → Select
reduce() → Combine
```

---

### Q19. What is the difference between `for...in` and `for...of` loops?

### Answer

Both are used to iterate, but they work differently.

- **`for...in`** → iterates over the **keys/properties** of an object or the indexes of an array.
- **`for...of`** → iterates over the **values** of an iterable such as an array, string, or Set.

#### `for...in`

```javascript
const user = {
    name: "Imon",
    age: 23
};

for (const key in user) {
    console.log(key);
}

// name
// age
```

It gives us the **keys**.

#### `for...of`

```javascript
const numbers = [10, 20, 30];

for (const number of numbers) {
    console.log(number);
}

// 10
// 20
// 30
```

It gives us the **values**.

### Comparison

| `for...in` | `for...of` |
|---|---|
| Iterates over keys/properties | Iterates over values |
| Commonly used with objects | Commonly used with arrays |
| Returns property names/indexes | Returns actual values |

### Interview Tip

Remember:

```text
for...in → keys
for...of → values
```



### Q20. What are template literals and tagged templates?

### Answer

**Template literals** are a way to create strings using backticks (`` ` ``). They allow us to easily insert variables and expressions using `${}`.

#### Template Literal

```javascript
const name = "Imon";
const age = 23;

const message = `My name is ${name} and I am ${age} years old.`;

console.log(message);
// My name is Imon and I am 23 years old.
```

They also support **multi-line strings**:

```javascript
const message = `
Hello Imon,
Welcome to JavaScript!
`;

console.log(message);
```

#### Tagged Template

A **tagged template** allows a function to process a template literal before it is created.

```javascript
function greet(strings, name) {
    return `${strings[0]}${name.toUpperCase()}${strings[1]}`;
}

const name = "Imon";

console.log(greet`Hello ${name}!`);
// Hello IMON!
```

### Interview Tip

- Template literals → Use backticks `` ` ``
- `${}` → Insert variables or expressions
- Tagged templates → A function processes the template literal

---

### Q21. What is the event loop in JavaScript?

### Answer

The **event loop** is the mechanism that allows JavaScript to handle asynchronous operations even though JavaScript is **single-threaded**.

It continuously checks whether the **call stack** is empty and then moves waiting callbacks from the task queues to the call stack for execution.

### Example

```javascript
console.log("Start");

setTimeout(() => {
    console.log("Timeout");
}, 0);

console.log("End");
```

### Output

```text
Start
End
Timeout
```

### Why?

1. `"Start"` is executed.
2. `setTimeout()` is sent to the browser/Node.js environment.
3. `"End"` is executed.
4. The callback waits in the task queue.
5. When the call stack is empty, the event loop moves the callback to the call stack.
6. `"Timeout"` is executed.

### Simple Diagram

```text
Call Stack
    ↓
Web APIs / Node.js APIs
    ↓
Task Queue
    ↓
Event Loop
    ↓
Call Stack
```

### Interview Tip

Remember:

**JavaScript is single-threaded, but the event loop allows it to handle asynchronous tasks without blocking the main thread.**

---

### Q22. Explain how Promises work in JavaScript.

### Answer

A **Promise** is an object that represents the eventual result of an asynchronous operation.

A Promise has three states:

1. **Pending** → Operation is still running.
2. **Fulfilled** → Operation completed successfully.
3. **Rejected** → Operation failed.

### Example

```javascript
const promise = new Promise((resolve, reject) => {
    const success = true;

    if (success) {
        resolve("Operation successful!");
    } else {
        reject("Operation failed!");
    }
});

promise
    .then(result => {
        console.log(result);
    })
    .catch(error => {
        console.log(error);
    });
```

### Using a Real Example

```javascript
fetch("https://api.example.com/users")
    .then(response => response.json())
    .then(data => {
        console.log(data);
    })
    .catch(error => {
        console.log(error);
    });
```

### Important Methods

- `.then()` → Handles successful result.
- `.catch()` → Handles errors.
- `.finally()` → Runs whether the Promise succeeds or fails.

### Interview Tip

Remember the three states:

```text
Pending → Fulfilled
        ↘ Rejected
```

Promises are commonly used for **API calls, database operations, file operations, and other asynchronous tasks**.

---

### Q23. What is `async/await` and how does it improve upon Promises?

### Answer

`async/await` is a cleaner way to work with Promises. It makes asynchronous code look and behave more like synchronous code.

- `async` makes a function return a Promise.
- `await` pauses execution inside an `async` function until the Promise settles.

### Using Promise `.then()`

```javascript
function getUser() {
    return fetch("https://api.example.com/users")
        .then(response => response.json())
        .then(data => {
            console.log(data);
        })
        .catch(error => {
            console.log(error);
        });
}
```

### Using `async/await`

```javascript
async function getUser() {
    try {
        const response = await fetch("https://api.example.com/users");
        const data = await response.json();

        console.log(data);
    } catch (error) {
        console.log(error);
    }
}
```

### Advantages of `async/await`

- Easier to read and understand.
- Makes complex asynchronous code cleaner.
- Uses familiar `try...catch` for error handling.
- Avoids deeply nested `.then()` chains.

### Interview Tip

`async/await` **does not replace Promises**. It is built on top of Promises and provides cleaner syntax for working with them.

```text
Promise → .then() / .catch()

async/await → Cleaner syntax for Promises
```

For arrays, prefer `for...of` when you need the values.
