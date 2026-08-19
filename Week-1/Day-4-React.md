# Day 4 — React Advanced Topic: Routing, Performance & Patterns

## Q46. What is the useReducer hook and when is it preferred over useState?

`useReducer` is a React Hook used to manage complex state logic.

It is preferred over `useState` when:

* The state has multiple related values.
* State updates are complex.
* Multiple actions can modify the same state.
* You want to keep state update logic in one place.

```jsx
import { useReducer } from "react";

function reducer(state, action) {
  switch (action.type) {
    case "increment":
      return { count: state.count + 1 };
    case "decrement":
      return { count: state.count - 1 };
    default:
      return state;
  }
}

function Counter() {
  const [state, dispatch] = useReducer(reducer, { count: 0 });

  return (
    <>
      <p>{state.count}</p>
      <button onClick={() => dispatch({ type: "increment" })}>
        +
      </button>
      <button onClick={() => dispatch({ type: "decrement" })}>
        -
      </button>
    </>
  );
}
```

**In short:** Use `useState` for simple state and `useReducer` for complex state logic.

---

## Q47. Explain the useMemo hook and give a use case.

`useMemo` is used to **memoize a calculated value**. It prevents an expensive calculation from running again unless its dependencies change.

### Syntax

```jsx
const result = useMemo(() => expensiveCalculation(data), [data]);
```

### Example

```jsx
import { useMemo } from "react";

function UserList({ users, search }) {
  const filteredUsers = useMemo(() => {
    return users.filter(user =>
      user.name.toLowerCase().includes(search.toLowerCase())
    );
  }, [users, search]);

  return (
    <ul>
      {filteredUsers.map(user => (
        <li key={user.id}>{user.name}</li>
      ))}
    </ul>
  );
}
```

Here, `filteredUsers` is recalculated only when `users` or `search` changes.

**Use case:** Expensive operations such as filtering, sorting, or complex calculations.

> `useMemo` should not be used everywhere. For simple calculations, normal JavaScript is usually enough.

---

## Q48. What is the useCallback hook and when do you use it?

`useCallback` is used to **memoize a function reference** between renders.

### Syntax

```jsx
const functionName = useCallback(() => {
  // logic
}, [dependencies]);
```

### Example

```jsx
import { useCallback } from "react";

function Parent() {
  const handleClick = useCallback(() => {
    console.log("Button clicked");
  }, []);

  return <Child onClick={handleClick} />;
}
```

It is mainly useful when:

* Passing a function to a memoized child component.
* Preventing unnecessary child re-renders.
* Using a function as a dependency of another Hook.

### useMemo vs useCallback

| Hook          | Memoizes           |
| ------------- | ------------------ |
| `useMemo`     | A calculated value |
| `useCallback` | A function         |

```jsx
const value = useMemo(() => calculate(), []);
```

```jsx
const handleClick = useCallback(() => {}, []);
```

---

## Q49. What is React Router and how do you set up client-side routing?

React Router is a library used to implement **client-side routing** in React applications.

It allows users to navigate between different pages or views without completely reloading the browser.

### Installation

```bash
npm install react-router-dom
```

### Basic Setup

```jsx
import {
  BrowserRouter,
  Routes,
  Route
} from "react-router-dom";

function App() {
  return (
    <BrowserRouter>
      <Routes>
        <Route path="/" element={<Home />} />
        <Route path="/about" element={<About />} />
        <Route path="/contact" element={<Contact />} />
      </Routes>
    </BrowserRouter>
  );
}
```

Now:

```text
/          → Home
/about     → About
/contact   → Contact
```

### Example Components

```jsx
function Home() {
  return <h1>Home Page</h1>;
}

function About() {
  return <h1>About Page</h1>;
}

function Contact() {
  return <h1>Contact Page</h1>;
}
```

React Router handles navigation on the client side, so the page does not need to perform a full browser reload for normal route changes.

---

## Q50. What is the difference between useNavigate and Link in React Router?

Both `Link` and `useNavigate` are used for navigation, but they are used in different situations.

### Link

`Link` is used for **declarative navigation**, usually when creating navigation links in the UI.

```jsx
import { Link } from "react-router-dom";

function Navbar() {
  return (
    <nav>
      <Link to="/">Home</Link>
      <Link to="/about">About</Link>
    </nav>
  );
}
```

### useNavigate

`useNavigate` is used for **programmatic navigation**.

```jsx
import { useNavigate } from "react-router-dom";

function Login() {
  const navigate = useNavigate();

  const handleLogin = () => {
    // Login logic
    navigate("/dashboard");
  };

  return (
    <button onClick={handleLogin}>
      Login
    </button>
  );
}
```

### Main Difference

| `Link`                              | `useNavigate`                                             |
| ----------------------------------- | --------------------------------------------------------- |
| Declarative navigation              | Programmatic navigation                                   |
| Used directly in JSX                | Used inside JavaScript logic                              |
| Good for menus and navigation links | Good after actions such as login, logout, form submission |
| `<Link to="/about">About</Link>`    | `navigate("/about")`                                      |

**In short:** Use `Link` when the user clicks a navigation link. Use `useNavigate` when your JavaScript logic needs to change the route.



## Q51. What are custom hooks in React? Write a simple example.

A **custom Hook** is a JavaScript function that starts with `use` and allows us to **reuse stateful logic** between multiple components.

Custom Hooks can use built-in Hooks such as `useState`, `useEffect`, and `useContext`.

### Example

```jsx
import { useState } from "react";

function useCounter(initialValue = 0) {
  const [count, setCount] = useState(initialValue);

  const increment = () => {
    setCount(count + 1);
  };

  const decrement = () => {
    setCount(count - 1);
  };

  return {
    count,
    increment,
    decrement
  };
}
```

Using the custom Hook:

```jsx
function Counter() {
  const { count, increment, decrement } = useCounter(0);

  return (
    <>
      <h2>{count}</h2>

      <button onClick={increment}>+</button>
      <button onClick={decrement}>-</button>
    </>
  );
}
```

### Benefits of Custom Hooks

* Reuse logic between components.
* Keep components cleaner.
* Avoid repeating the same Hook logic.
* Make complex logic easier to maintain.

**In short:** Custom Hooks are mainly used to **reuse stateful logic**, not UI.

---

## Q52. What is lazy loading in React and how is it implemented?

**Lazy loading** means loading a component only when it is needed instead of loading all components when the application initially loads.

React provides `lazy()` and `Suspense` for this.

### Example

```jsx
import { lazy, Suspense } from "react";

const Dashboard = lazy(() => import("./Dashboard"));

function App() {
  return (
    <Suspense fallback={<p>Loading...</p>}>
      <Dashboard />
    </Suspense>
  );
}
```

Here, `Dashboard` is loaded only when React needs to render it.

### Benefits

* Reduces the initial JavaScript bundle size.
* Improves initial page loading time.
* Loads resources only when required.
* Useful for large applications.

Lazy loading is commonly used together with **code splitting** and React Router.

---

## Q53. What are React error boundaries and why are they useful?

**Error Boundaries** are React components that catch JavaScript errors in their child component tree and display a fallback UI instead of allowing the entire application UI to crash.

They are useful for:

* Handling unexpected rendering errors.
* Showing a user-friendly error message.
* Preventing the entire application from crashing.
* Providing a recovery or error page.

### Example

Error boundaries are traditionally implemented using class components:

```jsx
import React from "react";

class ErrorBoundary extends React.Component {
  constructor(props) {
    super(props);

    this.state = {
      hasError: false
    };
  }

  static getDerivedStateFromError() {
    return {
      hasError: true
    };
  }

  render() {
    if (this.state.hasError) {
      return <h1>Something went wrong.</h1>;
    }

    return this.props.children;
  }
}
```

Usage:

```jsx
function App() {
  return (
    <ErrorBoundary>
      <Dashboard />
    </ErrorBoundary>
  );
}
```

If `Dashboard` throws an error during rendering, the Error Boundary can display the fallback UI.

**Important:** Error boundaries do not catch every type of error. For example, they do not automatically catch errors inside event handlers.

---

## Q54. What is the Context API and when should you use Redux instead?

The **Context API** is a built-in React feature that allows data to be shared between components without passing props manually through every level of the component tree.

### Example

```jsx
import { createContext } from "react";

const UserContext = createContext();

function App() {
  const user = {
    name: "Imon"
  };

  return (
    <UserContext.Provider value={user}>
      <Dashboard />
    </UserContext.Provider>
  );
}
```

A child component can access the value using `useContext`:

```jsx
import { useContext } from "react";

function Dashboard() {
  const user = useContext(UserContext);

  return <h1>Hello {user.name}</h1>;
}
```

### When should you use Context?

Context is useful for relatively simple global data such as:

* Theme
* Current user
* Authentication information
* Language
* Application settings

### When should you use Redux?

Redux can be a better choice when:

* The application has complex global state.
* Many components need to read and update the same state.
* State transitions need to be predictable and structured.
* You need middleware and advanced debugging tools.
* State management logic has become difficult to maintain with Context and local state.

### Context vs Redux

| Context API                       | Redux                                    |
| --------------------------------- | ---------------------------------------- |
| Built into React                  | External state-management library        |
| Simple global data                | Complex application state                |
| Less setup                        | More structured                          |
| Good for theme/auth/user settings | Good for large shared state              |
| No additional dependency          | Provides advanced state-management tools |

**In short:** Context is useful for **sharing data**, while Redux is designed for **structured and complex state management**.

---

## Q55. Explain the concept of reconciliation in React.

**Reconciliation** is the process React uses to determine what changes are required in the UI when a component's **state or props change**.

When a component re-renders, React creates a new representation of the UI and compares it with the previous one. It then updates only the necessary parts of the actual DOM.

### Basic Process

```text
State / Props Change
        ↓
Component Re-renders
        ↓
React Creates New Virtual DOM Representation
        ↓
React Compares Old and New Representations
        ↓
React Determines Necessary Changes
        ↓
Actual DOM Is Updated
```

This comparison process helps React update the UI efficiently.

### Example

Suppose we have:

```jsx
function App() {
  const [count, setCount] = useState(0);

  return (
    <div>
      <h1>Hello</h1>
      <p>{count}</p>

      <button onClick={() => setCount(count + 1)}>
        Increment
      </button>
    </div>
  );
}
```

When `count` changes, React does not need to recreate the entire DOM manually. It determines which part of the rendered output changed and updates the necessary DOM node.

### Role of Keys

Keys are especially important when rendering lists.

```jsx
users.map(user => (
  <li key={user.id}>
    {user.name}
  </li>
))
```

Keys help React identify which items have been:

* Added
* Removed
* Changed
* Reordered

**In short:** Reconciliation allows React to efficiently determine **what changed and what needs to be updated in the UI**.



## Q56. What is the difference between React.Fragment and empty tags (`<>`)?

Both `React.Fragment` and the shorthand syntax `<>...</>` allow us to group multiple elements **without adding an extra DOM element**.

### React.Fragment

```jsx
import React from "react";

function App() {
  return (
    <React.Fragment>
      <h1>Hello</h1>
      <p>Welcome to React</p>
    </React.Fragment>
  );
}
```

### Empty Tags / Fragment Shorthand

```jsx
function App() {
  return (
    <>
      <h1>Hello</h1>
      <p>Welcome to React</p>
    </>
  );
}
```

### Main Difference

The shorthand syntax `<>...</>` cannot accept props, while `React.Fragment` can accept a `key`.

For example, when rendering a list:

```jsx
items.map(item => (
  <React.Fragment key={item.id}>
    <h2>{item.title}</h2>
    <p>{item.description}</p>
  </React.Fragment>
))
```

**In short:** Both work similarly, but use `React.Fragment` when you need to provide a `key` or other supported Fragment props.

---

## Q57. How do you handle forms in React? Explain with Formik or react-hook-form.

Forms in React can be handled using controlled components or form libraries such as **Formik** and **React Hook Form**.

React Hook Form is popular because it provides simple form handling, validation, and good performance.

### Installation

```bash
npm install react-hook-form
```

### Example

```jsx
import { useForm } from "react-hook-form";

function Login() {
  const {
    register,
    handleSubmit,
    formState: { errors }
  } = useForm();

  const onSubmit = (data) => {
    console.log(data);
  };

  return (
    <form onSubmit={handleSubmit(onSubmit)}>
      <input
        type="email"
        {...register("email", {
          required: "Email is required"
        })}
      />

      {errors.email && (
        <p>{errors.email.message}</p>
      )}

      <input
        type="password"
        {...register("password", {
          required: "Password is required"
        })}
      />

      {errors.password && (
        <p>{errors.password.message}</p>
      )}

      <button type="submit">
        Login
      </button>
    </form>
  );
}
```

### Benefits of React Hook Form

* Simple form handling.
* Built-in validation support.
* Less boilerplate code.
* Good performance.
* Easy integration with validation libraries.

**In short:** Form libraries make it easier to manage form values, validation, errors, and submission logic in larger React applications.

---

## Q58. What is code splitting in React and how does it improve performance?

**Code splitting** is the process of dividing a large JavaScript bundle into smaller chunks that can be loaded when they are needed.

Without code splitting, the browser may need to download a large JavaScript bundle when the application initially loads.

With code splitting, only the code required for the current page or feature needs to be loaded initially.

### Example

React provides `lazy()` for component-level code splitting:

```jsx
import { lazy, Suspense } from "react";

const Dashboard = lazy(() => import("./Dashboard"));

function App() {
  return (
    <Suspense fallback={<p>Loading...</p>}>
      <Dashboard />
    </Suspense>
  );
}
```

Here, the `Dashboard` component is placed in a separate chunk and loaded when required.

### Benefits

* Smaller initial JavaScript bundle.
* Faster initial page load.
* Less JavaScript downloaded initially.
* Better performance for large applications.
* Resources can be loaded on demand.

**In short:** Code splitting improves performance by loading only the JavaScript that is needed at a particular time.

---

## Q59. What are portals in React and when are they useful?

**React Portals** allow us to render a component into a different DOM node outside its normal parent DOM hierarchy.

They are commonly used for UI elements that need to appear outside the normal layout structure.

### Example

Suppose `index.html` contains:

```html
<div id="root"></div>
<div id="modal-root"></div>
```

We can render a modal into `modal-root`:

```jsx
import { createPortal } from "react-dom";

function Modal() {
  return createPortal(
    <div className="modal">
      <h2>Hello</h2>
      <button>Close</button>
    </div>,
    document.getElementById("modal-root")
  );
}
```

Even though the modal is rendered elsewhere in the DOM, it still belongs to the same React component tree.

### Common Use Cases

Portals are useful for:

* Modals
* Dialog boxes
* Tooltips
* Dropdowns
* Toast notifications

They are especially useful when a component needs to avoid layout or stacking issues caused by properties such as `overflow: hidden` or certain CSS positioning contexts.

**In short:** Portals allow React components to render outside their normal DOM parent while remaining part of the React tree.

---

## Q60. Explain the lifecycle of a React functional component with hooks.

A React functional component generally goes through three main stages:

1. **Mounting**
2. **Updating**
3. **Unmounting**

### 1. Mounting

Mounting happens when the component is rendered for the first time.

For example:

```jsx
import { useEffect } from "react";

function App() {
  useEffect(() => {
    console.log("Component mounted");
  }, []);

  return <h1>Hello</h1>;
}
```

With an empty dependency array `[]`, the Effect runs after the initial render.

---

### 2. Updating

Updating happens when the component's **state or props change**.

```jsx
import { useEffect, useState } from "react";

function Counter() {
  const [count, setCount] = useState(0);

  useEffect(() => {
    console.log("Count changed");
  }, [count]);

  return (
    <button onClick={() => setCount(count + 1)}>
      {count}
    </button>
  );
}
```

Whenever `count` changes, the component re-renders and the Effect runs again.

---

### 3. Unmounting

Unmounting happens when the component is removed from the UI.

Effects can return a **cleanup function** that runs when the component unmounts.

```jsx
import { useEffect } from "react";

function Timer() {
  useEffect(() => {
    const interval = setInterval(() => {
      console.log("Running...");
    }, 1000);

    return () => {
      clearInterval(interval);
      console.log("Component unmounted");
    };
  }, []);

  return <h1>Timer</h1>;
}
```

The cleanup function prevents resources such as timers, subscriptions, or event listeners from continuing after the component is removed.

### Functional Component Lifecycle

```text
Mount
  ↓
Render
  ↓
Effects run
  ↓
State / Props change
  ↓
Re-render
  ↓
Effects re-run if dependencies changed
  ↓
Unmount
  ↓
Effect cleanup
```

**In short:** Functional components use Hooks such as `useEffect` to perform side effects and cleanup during the component's lifecycle.
