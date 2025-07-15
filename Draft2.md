# Understanding How React Works

[![Watch the video](https://i.ytimg.com/vi/za2FZ8QCE18/hq720.jpg)](https://youtu.be/za2FZ8QCE18?si=x8Vflay5vdqpI6s4)

## What is React?

React is a **library**, not a framework. It lets you **build user interfaces** by using components.

At its core:

* React lets you **describe the UI** you want to show using components.
* It converts those components into a **tree of elements** that are used to render the page.

> **React doesn’t render anything itself** — it just creates elements.
> For rendering to the browser, we use **React DOM**, which used to be part of React but is now a separate library.

## Platform-Agnostic Rendering

Since React only creates a structure of elements and doesn’t deal with how they’re shown:

* You can use **React Native** to render on mobile apps.
* You can use **custom libraries** to render on desktops (like Electron).
* You can also build your own renderers to display content wherever you want.

## Why is it called React?

React keeps track of your **data (state)** and **automatically updates the UI** whenever that data changes.

That’s why it’s called **React** – it *reacts* to changes in the code and syncs the UI accordingly.

## JSX is Optional

React **does not understand HTML or JSX** — it only understands JavaScript.

So what looks like HTML (JSX) is actually **converted** to JavaScript using `React.createElement()`.

## Example: Without JSX

```js
// likeButton.js

import React from 'react';

function LikeButton() {
    const [liked, setLiked] = React.useState(false);
    
    if (liked) {
        return React.createElement("span", null, "You liked this");
    } else {
        return React.createElement(
            "button",
            { onClick: () => setLiked(true) },
            "Like"
        );
    }
}

const domContainer = document.querySelector("#like_button_container");
const root = ReactDOM.createRoot(domContainer);
root.render(React.createElement(LikeButton));
```

## Example: With JSX

```js
// likeButton.js

import { useState } from 'react';

function LikeButton() {
    const [liked, setLiked] = useState(false);

    if (liked) {
        return <span>You liked this</span>;
    } else {
        return <button onClick={() => setLiked(true)}>Like</button>;
    }
}

const domContainer = document.querySelector("#like_button_container");
const root = ReactDOM.createRoot(domContainer);
root.render(<LikeButton />);
```

## Setting Up a React Development Environment

For a good developer experience, we need to combine React with other libraries and tools:

### Essential Tools

- **Live Server**: Allows you to see what you're building in real-time, including helpful errors and warnings
- **Babel**: Enables the use of JSX instead of describing UI with JavaScript Objects (React.createElement)
- **Bundler**: Bundles all of your JavaScript code together

### Create React App and Alternatives

The React team created **Create React App** - a tool we're all familiar with that provides a ready-to-use React project with all the necessary tools and configurations. This makes setting up a React project very easy.

Since React is a library and we can add any set of tools, we can also create React applications using alternative bundlers:
- **Parcel**
- **Vite**

## React's Declarative Nature

React is **declarative**, not **imperative**. This means:

- You **cannot** directly interact with the DOM (like appending HTML elements or changing them)
- You simply **describe** the UI, and React handles the inserting and updating for you

## Understanding JSX

### Why JSX is Essential

For writing large-scale applications, we need to use JSX. Otherwise, the codebase becomes too complicated to manage.

### How JSX Works

React cannot understand JSX directly. That's where **Babel** comes in - it converts JSX into `React.createElement` calls under the hood, which React can understand.

### JSX vs HTML: Key Differences

While JSX and HTML may look alike, they're not the same. JSX is more strict:

#### Self-Closing Tags
```html
<!-- HTML -->
<img>

<!-- JSX -->
<img/>
```

#### Single Root Element Rule

You must return exactly one root element. You cannot return multiple elements directly.

**Using a div wrapper:**
```jsx
<div>
    <img/>
    <p>Lorem ipsum</p>
</div>
```

**Using React Fragments:**
```jsx
<>
    <img/>
    <p>Lorem ipsum</p>
</>
```

### JavaScript Integration in JSX

The most powerful feature of JSX is the ability to break out of HTML and directly insert JavaScript wherever you want. This allows you to express your UI however you want without learning new syntax.

## Framework Comparison: UI Expression

### React (JavaScript Integration)
```jsx
if(loading) {
    return <LoadingScreen/>
}
if(error) {
    return <NotFound/>
}
return <Content/>
```

### Angular (Template Syntax)
```html
<li *ngFor="let item of items">
    {{item}}
</li>
```

### Vue (Template Syntax)
```html
<li v-for="({message}, index) in items">
    {{message}} {{index}}
</li>
```

## The JSX Trade-off: Freedom vs Performance

### The Downside of JSX Freedom

Writing JSX in React leads to **countless different ways** the UI can be constructed and changed. This creates challenges:

- When React needs to re-render your component, it becomes **hard to predict** what actually changed
- It's difficult to determine **where** the changes occurred
- Since anything is possible, it's hard to make assumptions
- This causes **more work** and makes the process **slower**

### Template-Based Frameworks Advantage

Template-based frameworks like Vue and Angular have an advantage:

- They are **more restricted** in how UI can be expressed
- This helps them **make assumptions** about what can and cannot change in a component
- They know the **boundaries** of possible changes
- This leads to **better performance** optimizations
