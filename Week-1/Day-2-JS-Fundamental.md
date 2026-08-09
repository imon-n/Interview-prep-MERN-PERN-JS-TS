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

For arrays, prefer `for...of` when you need the values.
