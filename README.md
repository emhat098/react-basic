
# React Basic Components

> This blog post summarizes the concept of React components.

## What Will You Learn in This Article?

1. How to define a component in React.
2. JSX: Write it right.
3. Props and State in components.
4. Conditional Rendering.
5. Composition - The pillar of React.

## Function Component and Class Component

In React, there are two ways to define a component: Class components and Function components.

### Class Component

> `Component` is the base class for React components defined as JavaScript classes.

At the beginning of the [React.dev - Component](https://react.dev/reference/react/Component) page, there's a warning: 

> "We recommend defining components as functions instead of classes. See how to migrate."

Why does React recommend using Function components for new applications? Let’s first understand Class components and their pitfalls.

Class components are essentially JavaScript classes designed for rendering React components. The Class component has 29 references, and you can dive into each on the [React.dev documentation](https://react.dev/reference/react/Component#component). Here's an example to illustrate:

```jsx
class Counter extends React.Component {
  constructor(props) {
    super(props);
    this.state = { count: 0 };
  }
  increment = () => this.setState({ count: this.state.count + 1 });
  render() {
    return <button onClick={this.increment}>{this.state.count}</button>;
  }
}
```

#### My Story

We created a simple `Counter` component with just one button. But look at the number of lines required to make it functional! As applications grow, so do the challenges of using Class components: managing lifecycle methods, reusing logic, handling `this`, and dealing with boilerplate-heavy code. 

To resolve these issues, the React team introduced **Hooks**, allowing Function components to manage state and side effects. Hooks provide all the functionality of Class components (and more), making them the standard for modern React applications.

---

### Function Component

```jsx
import React from 'react';

const Counter = () => {
  const [count, setCount] = React.useState(0);
  return <button onClick={() => setCount(count + 1)}>{count}</button>;
};
```

Wow! With just a few lines of code, we’ve built the same component using a Function component. No need for classes, constructors, or `this`.

---

### Why Use Function Components?

1. **Simpler Syntax and Readability**:
   - Function components are cleaner and easier to understand, especially for beginners.
2. **Reusability with Hooks**:
   - Hooks like `useState` and `useEffect` make it easier to reuse logic without restructuring components.
3. **Avoiding Complexity from `this`**:
   - Function components eliminate the need to manage `this` bindings.
4. **Performance Benefits**:
   - Function components are faster as they don’t need to instantiate a class.
5. **Easier to Test**:
   - Function components are simpler to test since they are plain functions.
6. **Modern Ecosystem Alignment**:
   - React’s modern tools and features are optimized for Function components.

**Do You Need to Migrate All Class Components?**
Not necessarily! While Function components are preferred for new development, existing Class components are still supported. Migrate only when modernizing or refactoring your code.

Reference: https://www.robinwieruch.de/react-function-component/

---

## JSX: Write It Right

JSX is a combination of HTML and JavaScript, known as JavaScript XML. For example:

```jsx
<button onClick={() => setCount(count + 1)}>{count}</button>
```

JSX represents the UI of React components, resembling HTML but with stricter rules:

### JSX Rules:

1. Return a **single root element**:
   ```jsx
   return <div><h1>Hello!</h1></div>;
   ```
2. Close all tags:
   ```jsx
   <img src="image.jpg" alt="description" />
   ```
3. Use `camelCase` for attributes:
   ```jsx
   <button onClick={...} className="btn">Click Me</button>
   ```

Reference: https://react.dev/learn/writing-markup-with-jsx

---

## State in Components

State represents the "memory" of a component. For example:

```jsx
const Counter = () => {
  const [count, setCount] = React.useState(0);
  return <button onClick={() => setCount(count + 1)}>{count}</button>;
};
```

Here, `count` is the state of the `Counter` component, managed using `useState`.

Reference: https://react.dev/learn/state-a-components-memory

---

## Props in Components

Props (short for "properties") allow you to pass data from parent to child components. For example:

```jsx
const Counter = ({ className, children }) => {
  const [count, setCount] = React.useState(0);
  return (
    <div>
      {children}
      <button className={className} onClick={() => setCount(count + 1)}>
        {count}
      </button>
    </div>
  );
};
```

Reference: https://www.robinwieruch.de/react-pass-props-to-component/

---

## Conditional Rendering

Use JavaScript’s conditional operators to render components conditionally:

```jsx
const Counter = () => {
  const [count, setCount] = React.useState(0);
  return (
    <button onClick={() => setCount(count + 1)}>
      {count === 0 ? "Zero" : count}
    </button>
  );
};
```

Reference: https://www.robinwieruch.de/conditional-rendering-react/

---

## Composition - The Pillar of React

React allows nesting components within others, making it highly composable:

```jsx
const Avatar = ({ src, alt }) => <img src={src} alt={alt} />;

const Profile = () => (
  <div>
    <Avatar src="https://picsum.photos/200" alt="Profile Picture" />
  </div>
);
```

Reference: https://react.dev/learn/passing-props-to-a-component#passing-jsx-as-children

---

### Summary:
This blog covered the basics of React components, explaining their types, JSX rules, state, props, and conditional rendering. It also highlighted why Function components are preferred in modern React development. Keep these principles in mind as you build scalable and maintainable React applications.
