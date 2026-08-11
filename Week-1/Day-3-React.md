# React Fundamentals — Questions & Answers

## Q31. What is React and what problem does it solve?

### Answer

React is a **JavaScript library for building user interfaces**, especially single-page applications (SPAs). It was developed by Meta.

React solves the problem of efficiently building and updating complex, interactive UIs by using:

* **Component-based architecture** — UI is divided into reusable components.
* **State management** — components can manage changing data.
* **Virtual DOM** — React efficiently determines which parts of the UI need to be updated.
* **Declarative programming** — we describe what the UI should look like based on the current state.

### Example

```jsx
function Welcome() {
  return <h1>Hello, Imon!</h1>;
}
```

Here, `Welcome` is a reusable React component.

---

## Q32. What is JSX and why is it used in React?

### Answer

JSX stands for **JavaScript XML**. It is a syntax extension for JavaScript that allows us to write HTML-like code inside JavaScript.

JSX makes React code easier to read and write because we can describe the UI structure directly inside the component.

### Example

```jsx
function App() {
  const name = "Imon";

  return <h1>Hello, {name}</h1>;
}
```

JSX is **not directly understood by the browser**. Tools such as Babel or the project's compiler transform it into JavaScript.

For example:

```jsx
<h1>Hello</h1>
```

is conceptually transformed into a React element creation call.

---

## Q33. What is the difference between functional and class components?

### Answer

Both functional and class components can be used to create React components, but **functional components are the modern and preferred approach**.

| Functional Component             | Class Component                 |
| -------------------------------- | ------------------------------- |
| JavaScript function              | JavaScript class                |
| Uses Hooks                       | Uses lifecycle methods          |
| Simpler and less code            | More verbose                    |
| Modern React approach            | Older approach                  |
| Does not use `this`              | Uses `this`                     |
| Easier to reuse logic with Hooks | Logic reuse is more complicated |

### Functional Component

```jsx
function Welcome({ name }) {
  return <h1>Hello {name}</h1>;
}
```

### Class Component

```jsx
class Welcome extends React.Component {
  render() {
    return <h1>Hello {this.props.name}</h1>;
  }
}
```

**Interview Point:** Modern React generally uses **functional components with Hooks**.

---

## Q34. What is the Virtual DOM and how does React use it?

### Answer

The Virtual DOM is an **in-memory representation of the UI** that React uses to determine what needs to change in the actual DOM.

When state or props change:

1. React creates a new representation of the UI.
2. React compares it with the previous representation.
3. It determines the necessary changes.
4. React updates the relevant parts of the actual DOM.

This process helps React avoid unnecessary DOM updates.

### Example

If a counter changes from:

```text
Count: 5
```

to:

```text
Count: 6
```

React doesn't need to recreate the entire page. It can update the relevant DOM content.

**Interview Point:** The Virtual DOM is an implementation detail that helps React efficiently reconcile UI changes.

---

## Q35. Explain the `useState` Hook with an example.

### Answer

`useState` is a React Hook that allows a functional component to **store and update state**.

### Example

```jsx
import { useState } from "react";

function Counter() {
  const [count, setCount] = useState(0);

  return (
    <div>
      <p>Count: {count}</p>

      <button onClick={() => setCount(count + 1)}>
        Increase
      </button>
    </div>
  );
}
```

Here:

```jsx
const [count, setCount] = useState(0);
```

* `count` → current state value
* `setCount` → function used to update the state
* `0` → initial value

When `setCount` is called, React schedules a re-render with the new state.

---

## Q36. What is the `useEffect` Hook and what are its use cases?

### Answer

`useEffect` is a React Hook used to perform **side effects** in a component.

Common use cases include:

* Fetching data from an API
* Setting up event listeners
* Using timers
* Subscribing and unsubscribing to services
* Synchronizing with external systems

### Example

```jsx
import { useEffect } from "react";

function App() {
  useEffect(() => {
    console.log("Component rendered");
  }, []);

  return <h1>Hello</h1>;
}
```

The empty dependency array:

```jsx
[]
```

means the effect runs after the component is initially mounted.

### With Dependencies

```jsx
useEffect(() => {
  console.log("Count changed");
}, [count]);
```

This effect runs when `count` changes.

### Cleanup Example

```jsx
useEffect(() => {
  const id = setInterval(() => {
    console.log("Running...");
  }, 1000);

  return () => clearInterval(id);
}, []);
```

The returned function performs cleanup.

---

## Q37. What is the difference between controlled and uncontrolled components?

### Answer

The main difference is **where the form data is managed**.

### Controlled Component

The form value is controlled by React state.

```jsx
function Form() {
  const [name, setName] = useState("");

  return (
    <input
      value={name}
      onChange={(e) => setName(e.target.value)}
    />
  );
}
```

Here, React state is the source of truth.

### Uncontrolled Component

The DOM itself manages the value, and we can access it using a ref.

```jsx
function Form() {
  const inputRef = useRef();

  return <input ref={inputRef} />;
}
```

### Difference

| Controlled                       | Uncontrolled                 |
| -------------------------------- | ---------------------------- |
| React manages the value          | DOM manages the value        |
| Uses state                       | Usually uses `ref`           |
| Easier validation and dynamic UI | Simpler for some basic forms |
| More common in React forms       | Useful in specific cases     |

---

## Q38. What are props in React and how are they passed?

### Answer

Props, short for **properties**, are used to pass data from a parent component to a child component.

Props are **read-only** from the receiving component's perspective.

### Example

```jsx
function User({ name }) {
  return <h2>Hello {name}</h2>;
}

function App() {
  return <User name="Imon" />;
}
```

Here:

```jsx
name="Imon"
```

is a prop passed from `App` to `User`.

The child receives it through:

```jsx
function User({ name })
```

**Interview Point:** Props generally flow **from parent to child**.

---

## Q39. What is prop drilling and how can it be avoided?

### Answer

**Prop drilling** happens when data needs to be passed through multiple intermediate components even though those components don't actually need the data.

For example:

```text
App
 ↓
Parent
 ↓
Child
 ↓
GrandChild
```

If `GrandChild` needs some data from `App`, we may have to pass it through `Parent` and `Child`.

### Ways to Avoid Prop Drilling

1. **Context API**
2. **State management libraries** such as Redux or Zustand
3. **Better component architecture**
4. **Component composition**

For example, Context can allow deeply nested components to access shared data without manually passing props through every level.

---

## Q40. Explain the `useContext` Hook with an example.

### Answer

`useContext` allows a component to access data from a React Context without manually passing props through every intermediate component.

### Example

```jsx
import { createContext, useContext } from "react";

const UserContext = createContext();

function App() {
  return (
    <UserContext.Provider value="Imon">
      <Profile />
    </UserContext.Provider>
  );
}

function Profile() {
  const user = useContext(UserContext);

  return <h1>Hello {user}</h1>;
}
```

Here:

```jsx
<UserContext.Provider value="Imon">
```

provides the value.

And:

```jsx
const user = useContext(UserContext);
```

reads the value.

### Common Uses

* Theme
* Authentication/user information
* Language preferences
* Application-wide settings

---

## Q41. What is the `useRef` Hook and when would you use it?

### Answer

`useRef` is a React Hook that creates a mutable reference whose value **persists between renders without causing a re-render when changed**.

### Example: Accessing a DOM Element

```jsx
import { useRef } from "react";

function App() {
  const inputRef = useRef(null);

  const focusInput = () => {
    inputRef.current.focus();
  };

  return (
    <>
      <input ref={inputRef} />

      <button onClick={focusInput}>
        Focus
      </button>
    </>
  );
}
```

Here:

```jsx
inputRef.current
```

refers to the input DOM element.

### Common Uses

* Accessing DOM elements
* Storing timer IDs
* Keeping mutable values between renders
* Storing previous values

**Important:** Updating `ref.current` does **not** trigger a re-render.

---

## Q42. What are React keys and why are they important in lists?

### Answer

Keys are **unique identifiers** that React uses to identify elements in a list.

### Example

```jsx
const users = [
  { id: 1, name: "Imon" },
  { id: 2, name: "Rahim" }
];

function Users() {
  return (
    <ul>
      {users.map(user => (
        <li key={user.id}>
          {user.name}
        </li>
      ))}
    </ul>
  );
}
```

Here:

```jsx
key={user.id}
```

helps React identify each list item.

Keys are important because they help React correctly determine **which items were added, removed, or changed** during reconciliation.

### Important

Avoid using array indexes as keys when the list can be reordered, inserted into, or deleted from.

---

## Q43. What is the difference between state and props?

### Answer

Both are used to store data in React, but they have different purposes.

| State                            | Props                                  |
| -------------------------------- | -------------------------------------- |
| Managed by the component         | Passed from parent                     |
| Can change                       | Read-only to the receiving component   |
| Updated using state setters      | Parent controls the value              |
| Used for internal component data | Used to communicate between components |

### Example

```jsx
function Counter({ title }) {
  const [count, setCount] = useState(0);

  return (
    <>
      <h1>{title}</h1>

      <p>{count}</p>

      <button onClick={() => setCount(count + 1)}>
        +
      </button>
    </>
  );
}
```

Here:

* `title` → **prop**
* `count` → **state**

---

## Q44. How does conditional rendering work in React?

### Answer

Conditional rendering means displaying different UI based on a condition.

React commonly uses the following techniques.

### 1. Ternary Operator

```jsx
function App({ isLoggedIn }) {
  return (
    <div>
      {isLoggedIn ? <Dashboard /> : <Login />}
    </div>
  );
}
```

### 2. Logical AND (`&&`)

```jsx
{isAdmin && <AdminPanel />}
```

The `AdminPanel` is rendered only when `isAdmin` is truthy.

### 3. `if` Statement

```jsx
function App({ isLoggedIn }) {
  if (!isLoggedIn) {
    return <Login />;
  }

  return <Dashboard />;
}
```

These techniques allow React to dynamically render UI based on state or props.

---

## Q45. What is `React.memo` and when should you use it?

### Answer

`React.memo` is a performance optimization that **memoizes a functional component**.

If a parent re-renders, React can skip re-rendering the memoized child when its props have not changed.

### Example

```jsx
const User = React.memo(function User({ name }) {
  console.log("User rendered");

  return <h2>{name}</h2>;
});
```

If the parent re-renders but `name` remains the same, React can reuse the previous rendered result.

### When Should You Use It?

Use `React.memo` when:

* A component renders frequently.
* The component is relatively expensive to render.
* Its props often remain unchanged.
* Profiling shows that unnecessary re-renders are causing a performance problem.

### Important

Don't automatically wrap every component with `React.memo`. It adds complexity and isn't always beneficial.

### Interview One-Liner

> `React.memo` prevents unnecessary re-renders of a functional component when its props haven't changed.
