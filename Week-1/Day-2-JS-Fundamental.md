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


### Q24. What is the difference between `call()`, `apply()`, and `bind()`?

### Answer

`call()`, `apply()`, and `bind()` are used to control the value of the `this` keyword when calling a function.

The main difference is how they pass arguments and whether they execute the function immediately.

| Method | Arguments | Executes Immediately? |
|---|---|---|
| `call()` | Individual arguments | ✅ Yes |
| `apply()` | Arguments as an array | ✅ Yes |
| `bind()` | Individual arguments | ❌ No, returns a new function |

### `call()`

```javascript
const user = {
    name: "Imon"
};

function greet(city) {
    console.log(`Hello ${this.name} from ${city}`);
}

greet.call(user, "Chattogram");
// Hello Imon from Chattogram
```

### `apply()`

```javascript
greet.apply(user, ["Chattogram"]);
// Hello Imon from Chattogram
```

The main difference is that `apply()` takes arguments as an **array**.

### `bind()`

```javascript
const newGreet = greet.bind(user, "Chattogram");

newGreet();
// Hello Imon from Chattogram
```

`bind()` returns a new function that can be called later.

### Interview Tip

Remember:

```text
call()  → arguments separately → executes now
apply() → arguments as array    → executes now
bind()  → returns new function  → executes later
```

---

### Q25. What is prototypal inheritance in JavaScript?

### Answer

**Prototypal inheritance** is a mechanism in JavaScript where an object can access properties and methods from another object through its **prototype**.

Every JavaScript object has an internal link to another object called its prototype.

### Example

```javascript
const person = {
    greet() {
        console.log("Hello!");
    }
};

const user = Object.create(person);

user.greet();
// Hello!
```

Here, `user` does not have its own `greet()` method. JavaScript looks at its prototype (`person`) and finds the method there.

### Using Constructor Functions

```javascript
function Person(name) {
    this.name = name;
}

Person.prototype.greet = function () {
    console.log(`Hello, ${this.name}`);
};

const user = new Person("Imon");

user.greet();
// Hello, Imon
```

### Interview Tip

When JavaScript cannot find a property on an object, it looks for that property in the object's **prototype chain**.

```text
Object
   ↓
Prototype
   ↓
Prototype's Prototype
   ↓
null
```

---

### Q26. Explain the concept of the `this` keyword in different contexts.

### Answer

The `this` keyword refers to the object associated with the current execution context.

Its value depends on **how a function is called**, not where the function is written.

### 1. Global Context

```javascript
console.log(this);
```

In a browser's regular script, `this` refers to the global `window` object.

### 2. Object Method

```javascript
const user = {
    name: "Imon",

    greet() {
        console.log(this.name);
    }
};

user.greet();
// Imon
```

Here, `this` refers to the `user` object.

### 3. Regular Function

```javascript
function showThis() {
    console.log(this);
}

showThis();
```

The value depends on the execution mode. In strict mode, `this` is `undefined`.

### 4. Arrow Function

Arrow functions do **not** have their own `this`. They inherit `this` from their surrounding lexical scope.

```javascript
const user = {
    name: "Imon",

    greet: () => {
        console.log(this.name);
    }
};
```

Using an arrow function as an object method generally does **not** make `this` refer to the object.

### 5. Constructor with `new`

```javascript
function User(name) {
    this.name = name;
}

const user = new User("Imon");

console.log(user.name);
// Imon
```

Here, `this` refers to the newly created object.

### Interview Tip

Remember:

```text
Object method → this = object
Regular function → depends on how it is called
Arrow function → inherits this
new → this = newly created object
call/apply/bind → explicitly set this
```

---

### Q27. What are JavaScript modules (`import`/`export`)?

### Answer

**JavaScript modules** allow us to split code into separate files and share variables, functions, classes, or objects between them.

This makes applications easier to organize and maintain.

### Named Export

```javascript
// math.js

export function add(a, b) {
    return a + b;
}

export function subtract(a, b) {
    return a - b;
}
```

### Named Import

```javascript
// app.js

import { add, subtract } from "./math.js";

console.log(add(10, 5));
console.log(subtract(10, 5));
```

### Default Export

```javascript
// user.js

export default function getUser() {
    return "Imon";
}
```

Import:

```javascript
import getUser from "./user.js";

console.log(getUser());
```

### Interview Tip

- `export` → Makes code available to other modules.
- `import` → Uses exported code.
- Named exports use `{ }`.
- A default export can be imported with any name.

---

### Q28. What is the difference between shallow copy and deep copy of objects?

### Answer

A **shallow copy** copies the top-level properties, but nested objects are still shared.

A **deep copy** creates a completely independent copy, including nested objects.

### Shallow Copy

```javascript
const user = {
    name: "Imon",
    address: {
        city: "Chattogram"
    }
};

const copy = { ...user };

copy.address.city = "Dhaka";

console.log(user.address.city);
// Dhaka
```

The nested `address` object is still shared.

### Deep Copy

One modern way is `structuredClone()`:

```javascript
const user = {
    name: "Imon",
    address: {
        city: "Chattogram"
    }
};

const copy = structuredClone(user);

copy.address.city = "Dhaka";

console.log(user.address.city);
// Chattogram
```

Now the nested object is also copied.

### Comparison

| Shallow Copy | Deep Copy |
|---|---|
| Copies top-level properties | Copies nested properties too |
| Nested objects are shared | Nested objects are independent |
| Faster | Usually more expensive |
| `{ ...obj }` | `structuredClone(obj)` |

### Interview Tip

```text
Shallow copy → nested references are shared
Deep copy    → nested data is independent
```

---

### Q29. What are `WeakMap` and `WeakSet`, and when would you use them?

### Answer

`WeakMap` and `WeakSet` are special collections that hold **weak references to objects**.

This means they do not prevent objects from being garbage-collected when there are no other references to them.

### WeakMap

A `WeakMap` stores **key-value pairs**, where the keys must be objects.

```javascript
const weakMap = new WeakMap();

let user = {
    name: "Imon"
};

weakMap.set(user, "User Data");

console.log(weakMap.get(user));
// User Data
```

If the `user` object is no longer referenced elsewhere, it can be garbage-collected.

### WeakSet

A `WeakSet` stores objects as values.

```javascript
const weakSet = new WeakSet();

let user = {
    name: "Imon"
};

weakSet.add(user);

console.log(weakSet.has(user));
// true
```

### When to Use Them

They can be useful for:

- Storing metadata associated with objects.
- Tracking objects without preventing garbage collection.
- Managing private-like object-related data.

### Interview Tip

Remember:

```text
WeakMap → Object keys + values
WeakSet → Objects only
```

They are **not iterable**, so you cannot use methods like `forEach()` on them.

---

### Q30. Explain the concept of memoization with an example.

### Answer

**Memoization** is an optimization technique where the result of an expensive function is stored so that the same calculation does not need to be performed again.

### Example

```javascript
function memoize(fn) {
    const cache = {};

    return function (n) {
        if (n in cache) {
            return cache[n];
        }

        const result = fn(n);
        cache[n] = result;

        return result;
    };
}

function square(n) {
    console.log("Calculating...");
    return n * n;
}

const memoizedSquare = memoize(square);

console.log(memoizedSquare(5));
// Calculating...
// 25

console.log(memoizedSquare(5));
// 25
```

The second time `memoizedSquare(5)` is called, JavaScript gets the result from the cache instead of calculating `5 × 5` again.

### How It Works

```text
First call
    ↓
Calculate result
    ↓
Store result in cache
    ↓
Return result

Same input again
    ↓
Check cache
    ↓
Return stored result
```

### Interview Tip

Memoization is useful when:

- A function is expensive to execute.
- The same inputs are used repeatedly.
- The function is deterministic (same input → same output).

**Main idea:**

```text
Memoization = Cache previous results to improve performance.
```
```

For arrays, prefer `for...of` when you need the values.
