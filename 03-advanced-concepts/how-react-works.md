## 1. **React is Just JavaScript**

The first thing to understand is that **React is just JavaScript**. React is a JavaScript library that helps you build **user interfaces (UIs)** using components.

## 2. **React Uses Components**

A component is just a JavaScript function that returns JSX.

Example:

```jsx
function Button() {
  return <button>Click Me!</button>;
}
```

> JSX looks like HTML, works like HTML, but **it is not HTML**.

## 3. **JSX is Not HTML – It Becomes JavaScript**

JSX is converted into JavaScript using `React.createElement()`.

For example:

```jsx
<h1>Hello</h1>
```

is converted to:

```jsx
React.createElement("h1", null, "Hello");
```

Explanation:

* `"h1"` → element type
* `null` → props (no props passed)
* `"Hello"` → child content

`createElement(type, props, ...children)` creates a React element.

## Reference: `createElement(type, props, ...children)`

### Usage:

```jsx
import { createElement } from 'react';

function Greeting({ name }) {
  return createElement(
    'h1',
    { className: 'greeting' },
    'Hello'
  );
}
```

### Parameters:

* `type`: A valid tag name string (`'div'`, `'span'`) or component (e.g., `Greeting`, `Fragment`, etc.)
* `props`: An object or `null`. Note that `ref` and `key` are treated specially and are not stored under `props`.
* `...children`: Can be strings, numbers, other React elements, `null`, `true`, arrays, etc.

### Returns:

An object like:

```js
{
  type: 'h1',
  props: { className: 'greeting', children: 'Hello' },
  ref: null,
  key: null
}
```

### Caveats:

* React elements are **immutable**. Don’t modify them after creation.
* JSX components must begin with a **capital letter**:
  `<MyComponent />` → `createElement(MyComponent)`
  `<div />` → `createElement('div')`
* For **dynamic children**, pass them as an array:
  `createElement('ul', {}, listItems)`
  (for static ones, `child1, child2, ...` is fine)

## Creating Elements Without JSX

If you're not using JSX, you can write components like this:

```jsx
import { createElement } from 'react';

function Greeting({ name }) {
  return createElement(
    'h1',
    { className: 'greeting' },
    'Hello ',
    createElement('i', null, name),
    '. Welcome!'
  );
}
```

With JSX, the same looks like:

```jsx
function Greeting({ name }) {
  return (
    <h1 className="greeting">
      Hello <i>{name}</i>. Welcome!
    </h1>
  );
}
```

Rendering it:

```jsx
export default function App() {
  return createElement(Greeting, { name: 'Taylor' });
}
```

Or with JSX:

```jsx
export default function App() {
  return <Greeting name="Taylor" />;
}
```

## 4. **React Builds a Virtual DOM**

When you return JSX, React builds a **Virtual DOM** – a JavaScript object that represents what the UI should look like.

Example:

```js
{
  type: 'div',
  props: {
    children: [
      { type: 'h1', props: { children: 'Hello' } },
      { type: 'button', props: { children: 'Click' } }
    ]
  }
}
```

## 5. **React Uses Diffing to Compare Virtual DOMs**

When state or props change, React:

1. Creates a **new Virtual DOM**
2. **Compares** it with the old one (diffing)
3. Finds the **differences**

## 6. **React Only Updates What Changed**

Instead of re-rendering the whole page, React updates **only the changed parts** in the real DOM.

This makes it **much faster** than traditional DOM manipulation.

## 7. **Reconciliation: Applying Changes**

Once React finds the difference between old and new virtual DOMs, it **reconciles** the change and **updates the real DOM** with minimal operations.

## 8. **State and Props Trigger Re-renders**

* **State**: Local component data
* **Props**: Data passed from parent to child

Changes in state or props will trigger a **re-render**, and React will go through the diffing and updating process again.

## 9. **React is Efficient Using Fiber**

React uses **Fiber** — a reimplementation of the React core algorithm — that allows:

* Breaking rendering into small chunks
* Pausing and resuming work
* Prioritizing updates

This improves performance, especially in complex apps.

## Final Summary

| Step | What Happens                                           |
| ---- | ------------------------------------------------------ |
| 1    | You write JSX                                          |
| 2    | JSX gets converted to `React.createElement()`          |
| 3    | React creates a Virtual DOM                            |
| 4    | On state/props change, React creates a new Virtual DOM |
| 5    | React compares old and new (diffing)                   |
| 6    | React updates only the changed parts in the real DOM   |
| 7    | Fiber helps manage and prioritize updates efficiently  |
