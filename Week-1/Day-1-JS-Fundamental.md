# Day 1 — JavaScript Fundamentals

## Q1. What is the difference between `var`, `let`, and `const` in JavaScript?

### Answer

`var`, `let`, and `const` are used to declare variables in JavaScript, but they behave differently.

| Feature | `var` | `let` | `const` |
|---------|-------|-------|---------|
| Scope | Function Scope | Block Scope | Block Scope |
| Reassign | ✅ Yes | ✅ Yes | ❌ No |
| Redeclare | ✅ Yes | ❌ No | ❌ No |
| Hoisted | ✅ Yes | ✅ Yes (TDZ) | ✅ Yes (TDZ) |

### Example

```javascript
var name = "Imon";
let age = 23;
const country = "Bangladesh";

name = "John";      // ✅ Allowed
age = 24;           // ✅ Allowed
// country = "USA"; // ❌ Error
```

### Interview Tip

- Use `const` by default.
- Use `let` when the value needs to change.
- Avoid using `var` in modern JavaScript.

---

## Q2. Explain the concept of hoisting in JavaScript.

### Answer

**Hoisting** is JavaScript's behavior where declarations are processed before the code starts executing.

JavaScript works in two main phases:

### 1. Memory Creation Phase

Before executing the code, JavaScript looks for variables and functions and creates memory for them.

- `var` → memory is created and initialized with `undefined`
- `let` and `const` → memory is created but they are not initialized, so they stay in the **Temporal Dead Zone (TDZ)**
- Function declarations → are stored completely in memory

### 2. Execution Phase

JavaScript then executes the code **line by line**.

### Example

```javascript
console.log(a); // undefined
var a = 10;

console.log(b); // ReferenceError
let b = 20;

greet(); // Hello

function greet() {
    console.log("Hello");
}
```
## Q3. What are the primitive data types in JavaScript?

### Answer

JavaScript has **7 primitive data types**.

1. String
2. Number
3. Boolean
4. Undefined
5. Null
6. Symbol
7. BigInt

Primitive values are immutable and are stored by value.

### Example

```javascript
let name = "Imon";                     // String
let age = 23;                          // Number
let isStudent = true;                  // Boolean
let city;                              // Undefined
let data = null;                       // Null
let id = Symbol("id");                 // Symbol
let bigNumber = 1234567890123456789n;  // BigInt
```

## Q4. What is the difference between `==` and `===` in JavaScript?
- `==` → Compares only values (after type conversion).
- `===` → Compares both value and type.
- Always prefer `===` to avoid unexpected results.

```javascript
console.log(5 == "5");    // true
console.log(5 === "5");   // false

console.log(true == 1);   // true
console.log(true === 1);  // false
```

---

## Q5. Explain how closures work in JavaScript with an example.

### Answer

A **closure** is a function that remembers and can access variables from its outer (parent) scope, even after the outer function has finished executing.

### Example

```javascript
function outer() {
    let count = 0;

    return function inner() {
        count++;
        console.log(count);
    };
}

const counter = outer();

counter(); // 1
counter(); // 2
counter(); // 3
```

### How it works

- `outer()` creates a local variable `count`.
- `inner()` remembers (`closes over`) `count`.
- Even after `outer()` finishes, `inner()` can still access and update `count`.

### Interview Tip

Closures are commonly used for:

- Data privacy
- Function factories
- Callbacks
- Event handlers

---

## Q6. What is the difference between `null` and `undefined`?

### Answer

Both represent the absence of a value, but they are used differently.

| `null` | `undefined` |
|---------|-------------|
| Assigned intentionally | Assigned automatically |
| Means "empty value" | Means "value not assigned" |
| Type is `object` (historical bug) | Type is `undefined` |

### Example

```javascript
let a;
console.log(a); // undefined

let b = null;
console.log(b); // null

console.log(typeof a); // "undefined"
console.log(typeof b); // "object"
```

### Interview Tip

- `undefined` → Variable declared but not assigned.
- `null` → Developer intentionally assigns "no value".

---

## Q7. What are arrow functions and how do they differ from regular functions?

### Answer

Arrow functions are a shorter syntax for writing functions, introduced in ES6.

Unlike regular functions, arrow functions do **not** have their own `this`. They inherit `this` from the surrounding scope.

### Example

#### Regular Function

```javascript
function greet(name) {
    return "Hello " + name;
}
```

#### Arrow Function

```javascript
const greet = (name) => {
    return "Hello " + name;
};
```

#### Short Form

```javascript
const greet = name => `Hello ${name}`;
```

### Differences

| Regular Function | Arrow Function |
|------------------|----------------|
| Has its own `this` | Inherits `this` |
| Can be used as a constructor | Cannot be used as a constructor |
| Supports `arguments` object | No `arguments` object |
| Traditional syntax | Shorter syntax |

### Interview Tip

Use arrow functions for callbacks and short functions. Use regular functions when you need your own `this`, such as in object methods or constructors.

---

## Q8. What is the scope chain in JavaScript?

### Answer

The **scope chain** is the mechanism JavaScript uses to look for variables.

When a variable is accessed:

1. JavaScript checks the current scope.
2. If not found, it checks the parent scope.
3. It continues until it reaches the global scope.
4. If the variable is still not found, a `ReferenceError` is thrown.

### Example

```javascript
let country = "Bangladesh";

function outer() {
    let city = "Chattogram";

    function inner() {
        let name = "Imon";

        console.log(name);
        console.log(city);
        console.log(country);
    }

    inner();
}

outer();
```

### How it works

`inner()` can access:

- Its own variables
- Variables from `outer()`
- Global variables

This searching process is called the **scope chain**.

### Interview Tip

JavaScript always searches for variables from the **inside out**:

**Current Scope → Parent Scope → Global Scope**



## Q9. Explain the concept of the Temporal Dead Zone (TDZ).

### Answer

The **Temporal Dead Zone (TDZ)** is the period between entering a block scope and initializing a variable declared with `let` or `const`.

During this period, the variable exists but **cannot be accessed**. Attempting to do so results in a `ReferenceError`.

### Example

```javascript
{
    // console.log(name); // ReferenceError

    let name = "Imon";

    console.log(name); // Imon
}
```

### Interview Tip

- Only `let` and `const` have a TDZ.
- `var` is hoisted and initialized with `undefined`, so it does not have a TDZ.

---

## Q10. What is a pure function? Give an example.

### Answer

A **pure function** is a function that:

1. Always returns the same output for the same input.
2. Does not modify or depend on external variables (no side effects).

### Example

```javascript
function add(a, b) {
    return a + b;
}

console.log(add(2, 3)); // 5
```

### Not a Pure Function

```javascript
let total = 0;

function add(value) {
    total += value;
}
```

This is **not** pure because it modifies an external variable.

### Interview Tip

Pure functions are predictable, easier to test, and commonly used in React and functional programming.

---

## Q11. What is the difference between a function declaration and a function expression?

### Answer

A **function declaration** defines a named function and is fully hoisted.

A **function expression** stores a function inside a variable and is not fully hoisted.

### Function Declaration

```javascript
greet();

function greet() {
    console.log("Hello");
}
```

### Function Expression

```javascript
// sayHello(); // Error

const sayHello = function () {
    console.log("Hello");
};

sayHello();
```

### Differences

| Function Declaration | Function Expression |
|----------------------|---------------------|
| Fully hoisted | Not fully hoisted |
| Can be called before declaration | Cannot be called before initialization |
| Has a function name | May be anonymous |

### Interview Tip

Use function declarations for reusable functions and function expressions when assigning functions to variables or passing them as callbacks.

---

## Q12. What are default parameters in JavaScript?

### Answer

Default parameters allow you to assign default values to function parameters if no value is provided.

### Example

```javascript
function greet(name = "Guest") {
    return `Hello, ${name}!`;
}

console.log(greet());        // Hello, Guest!
console.log(greet("Imon"));  // Hello, Imon!
```

### Interview Tip

Default parameters help avoid checking for `undefined` inside the function.

---

## Q13. What is the `typeof` operator, and what are its possible return values?

### Answer

The `typeof` operator returns the data type of a value.

### Example

```javascript
console.log(typeof "Hello");      // string
console.log(typeof 100);          // number
console.log(typeof true);         // boolean
console.log(typeof undefined);    // undefined
console.log(typeof null);         // object
console.log(typeof Symbol());     // symbol
console.log(typeof 10n);          // bigint
console.log(typeof {});           // object
console.log(typeof []);           // object
console.log(typeof function(){}); // function
```

### Common Return Values

- `"string"`
- `"number"`
- `"boolean"`
- `"undefined"`
- `"object"`
- `"function"`
- `"symbol"`
- `"bigint"`

### Interview Tip

Remember:

```javascript
typeof null // "object"
```

This is a well-known historical bug in JavaScript.

---

## Q14. Explain type coercion in JavaScript with examples.

### Answer

**Type coercion** is the automatic conversion of one data type to another by JavaScript during operations or comparisons.

### Example

```javascript
console.log("5" + 2);    // "52"
console.log("5" - 2);    // 3
console.log(true + 1);   // 2
console.log(false + 5);  // 5
console.log(5 == "5");   // true
console.log(5 === "5");  // false
```

### Interview Tip

- `+` with a string performs string concatenation.
- `-`, `*`, and `/` convert values to numbers.
- Prefer `===` to avoid unexpected type coercion.

---

## Q15. What is an Immediately Invoked Function Expression (IIFE)?

### Answer

An **Immediately Invoked Function Expression (IIFE)** is a function that executes immediately after it is defined.

It is commonly used to create a private scope and avoid polluting the global namespace.

### Example

```javascript
(function () {
    console.log("IIFE executed!");
})();
```

### Arrow Function IIFE

```javascript
(() => {
    console.log("Arrow IIFE");
})();
```

### Interview Tip

IIFEs were widely used before ES6 modules to create private variables and prevent global scope pollution.


