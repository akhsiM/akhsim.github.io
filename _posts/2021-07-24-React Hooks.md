---
layout: post-toc
title: React Hooks
tags: webdev software tech
---

# Hello World

Hooks are functions that let you "hook" into a React component's state and React lifecycle features from function components. Hooks don't work inside classes — they let you work without classes. 

Hooks work utilising features of the React framework by calling special hook functions from within components.

Prior to React version 16.8, developers were required to write classses to take advantage of React features. Nowadays we can still use classes to write React components, but using hooks to build our component is more ergonomic as we can re-use stateful logic without changing our components' hierarchy.

React has 10 different hooks.

## What's the point and what the hell is a hook?

Stateful logic, a.k.a data that changes in an application, was tightly coupled within a class component. What this means is that, in order to use stateful logic to build applications, we always needed to write a class.

In order to reuse logic with class components, we would need to use shitty patterns that look and sound like black magic such as higher order components and render props, which is essentially passing components to other components. These complex strategies in turn lead to complex nested hierarchy of components, like so:

<img class="mx-auto w-1/2" src="{{site.baseurl}}/assets/img/orgNotesImages/React Hooks-2021-07-24-13-37-50.png">

There is one thing that we need to understand and that is: **Hooks are the building blocks of the React framework**.

By giving developers access to hooks, React allows us to build components without having to extend the native React class component.

Hooks are functions that always starts with `use` like `useSuperPower()`. 

## Rules of the hooks

There is one rule to using React Hooks: **We can only call them from the top level of a functional component.**

<img class="mx-auto w-1/2" src="{{site.baseurl}}/assets/img/orgNotesImages/React Hooks-2021-07-24-13-42-04.png">

- **Do not** call Hooks inside loops, conditions or nested functions.

    *By following this rule, we ensure that Hooks are called in the same order each time a component renders. That is what allows React to correctly preserve the state of Hooks between multiple `useState` and `useEffect` calls.*

- **Do not** call Hooks from regular Javascript functions.

# The Basic Hooks

## `useState`

`useState()` is easily the most important and most used hook. 

`useState()` is to handle reactive data. Any data that changes in the application is called **state**. Whenever the state of a component changes, we want to update our component so that the DOM element is re-rendered accordingly so the latest changes are reflected to the end user.

The `useState()` hook takes one optional argument which is **the default state**.

For example:
```js
import { useState } from 'react';

function App() {

    useState(0);

    return (<div></div>);

}
```

The `useState()` function returns an array that contains two values that we can use within our components. We can the [destructure](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment) these two values with Javascript like so:
i.e:
```js
const [count, setCount] = useState(0); 
```

The first element is the reactive data, or state. When this value is changed, React will automatically re-render the component and updates the UI element.

The second element is a **setter function** that is used to update the piece of state. This setter function can be used to link up with event listener, like so:
```js
import { useState } from 'react';

function App() {

    const [count, setCount] = useState(0);

    return (
        <button onClick={() => setCount(count + 1)}>
            {count}
        </button>
    );
}
```

## `useEffect`

This is one of the most important hooks of React. It is also one of the most confusing.

In order to understand this hook, we need to first understand React's **Component lifecycle**.

### React Component Lifecycle

Each React component has several **lifecycle methods** that we can override to run code at particular time in the process. We can refer to this [React Lifecycle Cheatsheet](https://projects.wojtekmaj.pl/react-lifecycle-methods-diagram/).

#### Mounting

When an instance of a component is being created and inserted into the DOM, the following methods are called in the following order:

1. `constructor()`
2. `static getDerivedStateFromProps()`
3. `render()`
4. `componentDidMount()`

The important one to note is `componentDidMount()`. This is called **only once** when the component is mounted.

#### Updating

An update can be caused by changes to a component's state or props. The following methods are called in the following order when a component is being re-rendered:

1. `static getDerivedStateFromProps()`
2. `shouldComponentUpdate()`
3. `render()`
4. `getSnapshotBeforeUpdate()`
5. `componentDidUpdate()`

The important one to note is `componentDidUpdate()` which is called **multiple times** when the component is updated.

#### Unmounting

This method is called **once** when a component is being removed/destroyed from the DOM:
- `componentWillUnmount()`

### Back to `useEffect`

Understanding the three lifecycle methods above helps us understand `useEffect`, which allows developers to implement logic for all of them within a single function API.

`useEffect()` is a function which takes another function as its **first argument**. React will then run this function, so called **side effect function** after it has updated the DOM. The **second argument** is an array of **dependencies**. 

Options for array of dependencies:
- `[]` → No dependencies → Side effect function is only run **once** when the component first mounts.
- `[foo, bar]` → Some dependencies → These states will be tracked by React. Anytime they change, the side effect function will be invoked.

#### The cleanup function

Anther feature that we can implement within `useEffect` is a **tear-down** function, or cleanup function. This is done by declaring a `return` statement. Example:
```js
import React, { useState, useEffect } from 'react';

function FriendStatus(props) {
  const [isOnline, setIsOnline] = useState(null);

  useEffect(() => {    function handleStatusChange(status) {      setIsOnline(status.isOnline);    }    ChatAPI.subscribeToFriendStatus(props.friend.id, handleStatusChange);    // Specify how to clean up after this effect:    return function cleanup() {      ChatAPI.unsubscribeFromFriendStatus(props.friend.id, handleStatusChange);    };  });
  if (isOnline === null) {
    return 'Loading...';
  }
  return isOnline ? 'Online' : 'Offline';
}
```

The above `useEffect()` function returns a function. This is the **optional cleanup** mechanism that is used to enable cleanup behaviour. **Every effect may return a function that cleans up after it.**

The cleanup is performed after a component unmounts.

However, `useEffect` run for **every render**, when the component changes, and not just once. Every time something changes, the cleanup function is invoked to clear up effects from the **previous render** before running the new effects.

The key point to remember is that, when an `useEffect()` function is called, the side effect function is invoked, however **the cleanup function is not invoked**. It is stored in memory.

On the subsequent rendering, when `useEffect` is called again, the previous cleanup function is invoked with the props from the **previous** execution. This is extremely useful in scenarios where we want to cancel a timer variable from the previous execution.

## `useContext`

This hook allows us to work with React's context API which allows us to share data with the entire component tree.

<img class="mx-auto w-1/2" src="{{site.baseurl}}/assets/img/orgNotesImages/React Hooks-2021-07-24-14-30-09.png">

Imagine that we have an object called `Mood` that can be either "happy" or "sad".

```js
const moods = {
    happy: '😊',
    sad: '😥'
}
```

In order to share the current mood across different disconnected components in our App, we can create a `MoodContext`.  
```js
const moods = {
    happy: '😊',
    sad: '😥'
}

function App(props) {
    return (
        <MoodContext.Provider value={mood.happy}>
            <MoodEmoj />
        </MoodContext.Provider>
    )
}
```

Any child component of `MoodContext` or any nested child component of it can inherit this value without the needs for passing props down to the children.

The `useContext` hook allows us to access or consume the current value from the Context Provider, which might live many levels above in the component tree.

```js
const moods = {
    happy: '😊',
    sad: '😥'
}

function App(props) {
    return (
        <MoodContext.Provider value={mood.happy}>
            <MoodEmoj />
        </MoodContext.Provider>
    )
}

function MoodEmoji() {
    const mood = useContext(MoodContext);

    return <p>{mood}</p>
}
```

How does `useContext` access the current value of a specific context? Well, it calls the `value` prop of the **nearest** `<MyContext.Provider>` above the calling component in a tree.

When the nearest `<MyContext.Provider>` above the component updates, the `useContext` hook will trigger a rerender with the latest context `value` passed to the context provider.

A component that calls `useContext` will always re-render when the context value changes.

The argument to `useContext` must be the context object itself:

**CORRECT USE**: `useContext(MoodContext)`

** `useRef`

This hook allows us to create a mutable object that will keep the same value between different renders. The returned object of a `useRef()` call will **persist** for the full lifetime of the component.
 
```js
function App() {

    const count = useRef(0);

    return (
        <button onClick={() => count.current++ }>
            {count.current}
        </button>
    )
}

```

The argument that is passed to `useRef()` is the value which the `.current` property of the mutable object will be initialised to. Essentially, `useRef` is like a box that can hold a mutable value in its `.current` property.

This hook is useful when we want to keep a changing value that will persist throughout the whole lifetime of the component. An easy way to remember `useRef` is that it is similar to `useState`, except that any update to the returned object of `useRef` doesn't trigger re-rendering of the component.

### Common Use Case

A common use case for `useRef` is to access an element from the DOM. We do this by passing the returned ref object to the `ref` prop of the component. Then we can reference the raw HTML element in our function to **call native DOM element's API** like `.change()`, `.click()`...etc..

Example:
```js
function App() {

    const inputElement = useRef(null);

    const onClick = () => {
        // '.current' here points to the mounted text input element
        inputElement.current.focus(); 
    }

    return (
        <>
            <input ref={inputElement} type="text" />
            <button onClick={onClick}>Focus on the Text Input</button>
        </>
    );
}
```

# The Additional Hooks

These are either variants from the basic ones from the previous sections or only needed for specific edge cases.

## `useReducer`

```js
const [state, dispatch] = useReducer(reducerFunction, initialState, Args);
```

This is a variant of `setState` but goes about the task in a different way using the Redux pattern.

Esentially, instead of updating the state, we dispatch certain actions that go to a reducer function, which then determines **how to computes the next state**.

<img class="mx-auto w-1/2" src="{{site.baseurl}}/assets/img/orgNotesImages/React Hooks-2021-07-24-15-27-49.png">

This function accepts a reducer function that accepts two arguments `(state, action) => newState`. It also accepts a second argument which is the initial state. 

`useReducer` return an array of two elements, with the first being the current state. The second element, however, is a `dispatch` function that is used to dispatch an action.

`useReducer` is preferable to `useState` when we have complex state logic that involves multiple sub-values or when the next state depends on the previous one. Using a `switch` statement inside the reducer function is a common practice.

Common Example:

```js
function reducer(state, action) {
    switch (action.type) {
        case 'minus':
            return {count: state.count - 1};
        case 'plus':
            return {count: state.count + 1};
        default:
            throw new Error();
    }
}

function App() {
    const initialState = {count : 0};
    const [state, dispatch] = useReducer(reducer, initialState);

    return (
        <>
            Count: {state}
            <button onClick={() => dispatch({type: 'minus'})}> ➖ </button>
            <button onClick={() => dispatch({type: 'plus'})}> ➕ </button>
        </>
    )
}
```

This Redux pattern looks confusing initially however as our app grows complex, it helps with managing our component's state in a reliable and consistent manner.

## `useMemo`

This returns a "memoized" value. This is used to optimise the performance and computation cost for **improved performance**.

> **Memoization**: An optimization technique used to speed up computer programs by storing the results of the expensive function calls and returning the cached result when the same input occurs again.

We should use this only as needed for expensive calculation that we know for sure are hurting our app's performance.

Let's imagine that we have a component with a `count` value. From this counter, we also compute an additional value called `expensiveCount` that needs some sort of expensive computation.

Instead of re-running the expensive computation on every render, we can "memoize" the value.   

```js
function App() {

    const [count, setCount] = useState(60);

    const expensiveCount = useMemo(() => {
        return count ** 2;
    }, [count]);

    return (
        <>

        </>
    );
}
```

This function accepts a "create" function and an array of dependencies. `useMemo` will only recompute the memoized value **when one of the dependencies have changed**. This optimization helps to avoid the expensive logic on every render.

If no array is provided, a new value is computer on every render.

An important thing to remember is that the function that is passed to `useMemo` runs **during rendering**.

We use `useMemo()` when we want to memoize a return value. However, in cases where we want to memoize a callback function. We use `useCallback`.

## `useCallback`

This function returns a memoized callback.

When we define a function within a component, a new function object is created **each time the component is re-rendered**. Usually this isn't a big deal for most use cases, however in some edge cases we may want to memoize the function. 

A typical use is when we want to pass a function to **multiple child components**. By referencing the function using `useCallback`, we can prevent unnecessary rendering of the child component. This is because they would always be using the same function object.

```js

function App() {
    const [count, setCount] = useState(60);

    const showCount = useCallback(() => {
        alert(`Count ${count}`);
    }, [count]);

    return <> <SomeChild handler={showCount} /> </>
}
```

## `useImperativeHandle`

This is a more confusing hook. 

It is useful when we build a reusable component library in React, we might want to access the underlying DOM element and forward it to a consumer of the React component library. 

`useImperativeHandle` should be used with `forwardRef`.

What we can do is accessing the native DOM element using the `useRef` hook, then wrap it within the `forwardRef` to make that `ref` available when someone uses the component.

```js
function CoolButton(props, ref) {
    const myBtn = useRef(null);

    return  (
        <button ref={myBtn}></button>
    )
}
```

`useImperativeHandle` comes in handy when we want to change the behaviour of the exposed ref. This is a rare use case.

## `useLayoutEffect`

This is another hook that is used for rare use cases.

It is similar to `useEffect` but it fires synchronously after all components have been rendered, **but before** the updates have been painted onto the screen. This is used when we want to access the DOM and synchronously re-render.

Essentially, React will wait for the codeblock to run, before the UI update is rendered to the users. 

This can be useful, for example when we need to calculate a DOM attribute, e.g. scroll position, before the DOM is updated.

```js
function CoolButton(props, ref) {
    const myBtn = useRef(null);

    useLayoutEffect(() => {
        const rect = myBtn.current.getBoundingClientRect();

        console.log(box.height);
    })

    return  (
        <button ref={myBtn}></button>
    )
}
```

## `useDebugValue`

This can be used to display a label for custom hooks in React DevTools.

This doesn't make a lot of sense, until we have started to make custom React hooks from scratch. It allows us to easily debug our custom built hooks using the React DevTools.