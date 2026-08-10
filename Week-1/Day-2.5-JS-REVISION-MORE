# Day 3 — JavaScript Fundamentals III

## Q31. What is the difference between primitive and reference types in JavaScript?

### Answer

JavaScript values can be broadly divided into **primitive types** and **reference types**.

### Primitive Types

Primitive values are simple values that are stored and copied **by value**.

The primitive data types are:

* String
* Number
* Boolean
* Undefined
* Null
* Symbol
* BigInt

### Example

```javascript
let a = 10;
let b = a;

b = 20;

console.log(a); // 10
console.log(b); // 20
```

Changing `b` does not affect `a` because the value was copied.

### Reference Types

Objects, arrays, and functions are reference types.

When a reference type is assigned to another variable, both variables can refer to the **same object in memory**.

### Example

```javascript
const user1 = {
    name: "Imon"
};

const user2 = user1;

user2.name = "John";

console.log(user1.name); // John
console.log(user2.name); // John
```

Both variables refer to the same object.

### Interview Tip

```text
Primitive → copied by value
Reference → copied by reference
```

---

## Q32. What is the difference between shallow equality and deep equality?

### Answer

**Shallow equality** checks whether two values or objects have the same references or top-level values.

**Deep equality** checks whether the complete structure and nested values are equal.

### Shallow Equality

```javascript
const user1 = {
    name: "Imon"
};

const user2 = {
    name: "Imon"
};

console.log(user1 === user2); // false
```

Even though the objects contain the same data, they are different objects in memory.

### Reference Equality

```javascript
const user1 = {
    name: "Imon"
};

const user2 = user1;

console.log(user1 === user2); // true
```

Both variables refer to the same object.

### Deep Equality

Deep equality compares the actual contents of objects, including nested values.

For example:

```javascript
const user1 = {
    name: "Imon",
    address: {
        city: "Chattogram"
    }
};

const user2 = {
    name: "Imon",
    address: {
        city: "Chattogram"
    }
};
```

These objects have the same structure and values, but `===` still returns `false`.

### Interview Tip

```text
Shallow equality → Compare references/top-level values
Deep equality    → Compare complete nested structure
```

---

## Q33. What is lexical scope in JavaScript?

### Answer

**Lexical scope** means that the accessibility of variables is determined by **where the code is written**, not where the function is called.

A function can access variables from its own scope and its outer scopes.

### Example

```javascript
let name = "Imon";

function outer() {
    let age = 23;

    function inner() {
        console.log(name);
        console.log(age);
    }

    inner();
}

outer();
```

The `inner()` function can access:

* Its own variables
* Variables from `outer()`
* Global variables

### Interview Tip

JavaScript uses **lexical scoping**, meaning scope is determined by the structure of the code.

---

## Q34. What is the difference between function scope and block scope?

### Answer

**Function scope** means a variable is accessible throughout the function.

**Block scope** means a variable is accessible only inside the block `{ }` where it was declared.

### Function Scope

`var` is function-scoped.

```javascript
function test() {
    if (true) {
        var name = "Imon";
    }

    console.log(name); // Imon
}

test();
```

The `var` variable is accessible outside the `if` block because it is function-scoped.

### Block Scope

`let` and `const` are block-scoped.

```javascript
function test() {
    if (true) {
        let name = "Imon";
        const age = 23;
    }

    // console.log(name); // ReferenceError
    // console.log(age);  // ReferenceError
}

test();
```

### Interview Tip

```text
var         → Function Scope
let / const → Block Scope
```

---

## Q35. What is a callback function in JavaScript?

### Answer

A **callback function** is a function passed as an argument to another function and executed later.

### Example

```javascript
function greet(name, callback) {
    console.log(`Hello ${name}`);

    callback();
}

function sayBye() {
    console.log("Goodbye!");
}

greet("Imon", sayBye);
```

### Output

```text
Hello Imon
Goodbye!
```

Here, `sayBye` is passed to `greet()` as a callback.

### Common Uses

Callbacks are commonly used with:

* Event handlers
* Array methods
* Timers
* Asynchronous operations

### Interview Tip

```text
Callback = A function passed to another function
```

---

## Q36. What is callback hell and how can you avoid it?

### Answer

**Callback hell** occurs when multiple asynchronous callbacks are nested inside each other, making the code difficult to read and maintain.

### Example

```javascript
getUser(function(user) {
    getOrders(user, function(orders) {
        getPayment(orders, function(payment) {
            getReceipt(payment, function(receipt) {
                console.log(receipt);
            });
        });
    });
});
```

The code becomes deeply nested and difficult to manage.

### How to Avoid Callback Hell

We can use:

1. Promises
2. `async/await`
3. Properly separated functions

### Using async/await

```javascript
async function processOrder() {
    const user = await getUser();
    const orders = await getOrders(user);
    const payment = await getPayment(orders);
    const receipt = await getReceipt(payment);

    console.log(receipt);
}
```

This is much easier to read.

### Interview Tip

```text
Callback Hell → Too many nested callbacks

Avoid using:
→ Promises
→ async/await
```

---

## Q37. What is the difference between synchronous and asynchronous JavaScript?

### Answer

**Synchronous JavaScript** executes code one statement at a time and waits for each operation to finish before moving to the next one.

**Asynchronous JavaScript** allows certain operations to run without blocking the execution of other code.

### Synchronous Example

```javascript
console.log("Start");

console.log("Processing...");

console.log("End");
```

Output:

```text
Start
Processing...
End
```

Each statement executes sequentially.

### Asynchronous Example

```javascript
console.log("Start");

setTimeout(() => {
    console.log("Timeout");
}, 2000);

console.log("End");
```

Output:

```text
Start
End
Timeout
```

The timer runs asynchronously, so JavaScript continues executing the next statement.

### Interview Tip

```text
Synchronous   → Blocking
Asynchronous  → Non-blocking
```

---

## Q38. What are microtasks and macrotasks in the event loop?

### Answer

JavaScript uses different queues to manage asynchronous callbacks.

The two important categories are:

* **Microtasks**
* **Macrotasks**

### Microtasks

Examples include:

* Promise `.then()`
* `.catch()`
* `.finally()`
* `queueMicrotask()`

### Macrotasks

Examples include:

* `setTimeout()`
* `setInterval()`
* Some I/O operations

### Example

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

### Output

```text
Start
End
Promise
Timeout
```

### Why?

After the synchronous code finishes, JavaScript processes the **microtask queue before moving to the macrotask queue**.

### Interview Tip

```text
Synchronous code
      ↓
Microtasks
      ↓
Macrotasks
```

---

## Q39. What is the difference between `Promise.all()`, `Promise.allSettled()`, `Promise.race()`, and `Promise.any()`?

### Answer

These methods are used to handle multiple Promises.

| Method                 | Behavior                                          |
| ---------------------- | ------------------------------------------------- |
| `Promise.all()`        | Resolves when all resolve; rejects if one rejects |
| `Promise.allSettled()` | Waits for all Promises to finish                  |
| `Promise.race()`       | Settles when the first Promise settles            |
| `Promise.any()`        | Resolves when the first Promise fulfills          |

### `Promise.all()`

```javascript
const result = await Promise.all([
    promise1,
    promise2,
    promise3
]);
```

If any Promise rejects, `Promise.all()` rejects.

### `Promise.allSettled()`

```javascript
const result = await Promise.allSettled([
    promise1,
    promise2,
    promise3
]);
```

It waits for every Promise, whether fulfilled or rejected.

### `Promise.race()`

```javascript
const result = await Promise.race([
    promise1,
    promise2
]);
```

The first Promise to settle determines the result.

### `Promise.any()`

```javascript
const result = await Promise.any([
    promise1,
    promise2,
    promise3
]);
```

It returns the first successfully fulfilled Promise.

### Interview Tip

```text
all        → All must succeed
allSettled → Wait for all
race       → First to settle
any        → First to succeed
```

---

## Q40. What is error handling in JavaScript?

### Answer

JavaScript provides several ways to handle errors.

The most common tools are:

* `try`
* `catch`
* `finally`
* `throw`

### Example

```javascript
try {
    const result = riskyFunction();
    console.log(result);
} catch (error) {
    console.log("Something went wrong:", error.message);
} finally {
    console.log("Execution completed");
}
```

### `throw`

We can manually create an error using `throw`.

```javascript
function divide(a, b) {
    if (b === 0) {
        throw new Error("Cannot divide by zero");
    }

    return a / b;
}
```

### Interview Tip

```text
try     → Code that may cause an error
catch   → Handle the error
finally → Always executes
throw   → Create/raise an error
```

---

## Q41. What is the difference between localStorage, sessionStorage, and cookies?

### Answer

All three can store data in a browser, but they work differently.

| Feature                  | localStorage           | sessionStorage           | Cookies                     |
| ------------------------ | ---------------------- | ------------------------ | --------------------------- |
| Lifetime                 | Until manually removed | Until tab/session closes | Depends on expiration       |
| Storage                  | Around 5–10 MB         | Around 5–10 MB           | Around 4 KB                 |
| Sent with HTTP requests  | No                     | No                       | Yes                         |
| Accessible by JavaScript | Yes                    | Yes                      | Usually yes                 |
| Common use               | Persistent client data | Temporary session data   | Authentication/session data |

### localStorage

```javascript
localStorage.setItem("name", "Imon");

console.log(localStorage.getItem("name"));
```

The data remains after closing the browser until it is removed.

### sessionStorage

```javascript
sessionStorage.setItem("name", "Imon");
```

The data is generally available only for the current browser tab/session.

### Cookies

```javascript
document.cookie = "name=Imon";
```

Cookies can be automatically sent with HTTP requests.

### Interview Tip

```text
localStorage   → Persistent browser storage
sessionStorage → Temporary tab/session storage
Cookies        → Small data sent with HTTP requests
```

---

## Q42. What is JSON, and what are `JSON.stringify()` and `JSON.parse()`?

### Answer

**JSON (JavaScript Object Notation)** is a lightweight text format commonly used to exchange data between a client and a server.

### JavaScript Object

```javascript
const user = {
    name: "Imon",
    age: 23
};
```

### `JSON.stringify()`

It converts a JavaScript value into a JSON string.

```javascript
const jsonData = JSON.stringify(user);

console.log(jsonData);
```

Output:

```text
{"name":"Imon","age":23}
```

### `JSON.parse()`

It converts a JSON string back into a JavaScript value.

```javascript
const userData = JSON.parse(jsonData);

console.log(userData.name);
// Imon
```

### Interview Tip

```text
JSON.stringify() → Object → JSON string

JSON.parse()     → JSON string → Object
```

---

## Q43. What are optional chaining (`?.`) and nullish coalescing (`??`)?

### Answer

### Optional Chaining (`?.`)

Optional chaining allows us to safely access nested properties without getting an error when a property does not exist.

### Example

```javascript
const user = {
    profile: {
        name: "Imon"
    }
};

console.log(user.profile?.name);
// Imon

console.log(user.address?.city);
// undefined
```

Without optional chaining, accessing `user.address.city` could cause an error if `address` is `undefined`.

### Nullish Coalescing (`??`)

The `??` operator provides a default value when the left side is `null` or `undefined`.

```javascript
const name = null;

const result = name ?? "Guest";

console.log(result);
// Guest
```

### Important Difference

`??` only checks for:

* `null`
* `undefined`

It does not treat `0`, `false`, or `""` as missing values.

```javascript
const age = 0;

console.log(age ?? 18);
// 0
```

### Interview Tip

```text
?. → Safely access nested properties
?? → Provide a default for null/undefined
```

---

## Q44. What is the difference between `Object.freeze()` and `Object.seal()`?

### Answer

Both methods prevent certain changes to an object, but they behave differently.

### `Object.freeze()`

`Object.freeze()` prevents:

* Adding properties
* Removing properties
* Changing existing properties

```javascript
const user = {
    name: "Imon",
    age: 23
};

Object.freeze(user);

user.age = 24;
user.city = "Chattogram";

console.log(user);
// { name: "Imon", age: 23 }
```

### `Object.seal()`

`Object.seal()` prevents:

* Adding properties
* Removing properties

But existing properties can still be modified.

```javascript
const user = {
    name: "Imon",
    age: 23
};

Object.seal(user);

user.age = 24;

console.log(user.age);
// 24
```

### Comparison

| Method            | Add | Delete | Modify |
| ----------------- | --- | ------ | ------ |
| `Object.freeze()` | ❌   | ❌      | ❌      |
| `Object.seal()`   | ❌   | ❌      | ✅      |

### Interview Tip

```text
freeze → Cannot add, delete, or modify
seal   → Cannot add or delete, but can modify
```

---

## Q45. What is garbage collection in JavaScript?

### Answer

**Garbage collection** is the automatic process of removing objects from memory when they are no longer reachable or needed by the program.

JavaScript automatically manages memory using a garbage collector.

### Example

```javascript
let user = {
    name: "Imon"
};

user = null;
```

After assigning `null`, the original object may become unreachable.

```text
user
 ↓
Object

user = null

user
 ↓
null

Object → No reference
       → Eligible for garbage collection
```

The garbage collector can eventually remove the unreachable object and free its memory.

### Why Is It Important?

Garbage collection helps:

* Free unused memory
* Reduce memory usage
* Prevent some types of memory leaks

### Interview Tip

You do not normally manually free memory in JavaScript. The **garbage collector automatically manages unreachable objects**.

### Main Idea

```text
Object has references → Keep it in memory

No reachable references → Eligible for garbage collection
```

---

# Quick Revision — Q31–Q45

```text
31. Primitive vs Reference
32. Shallow Equality vs Deep Equality
33. Lexical Scope
34. Function Scope vs Block Scope
35. Callback Function
36. Callback Hell
37. Synchronous vs Asynchronous
38. Microtasks vs Macrotasks
39. Promise.all vs allSettled vs race vs any
40. Error Handling
41. localStorage vs sessionStorage vs Cookies
42. JSON.stringify vs JSON.parse
43. Optional Chaining vs Nullish Coalescing
44. Object.freeze vs Object.seal
45. Garbage Collection
```

### Most Important for MERN Interviews

```text
★★★★★ 35. Callback
★★★★★ 36. Callback Hell
★★★★★ 37. Sync vs Async
★★★★★ 38. Event Loop / Microtasks / Macrotasks
★★★★★ 39. Promise Methods
★★★★★ 41. Storage & Cookies
★★★★★ 42. JSON
★★★★★ 43. Optional Chaining & Nullish Coalescing
```
