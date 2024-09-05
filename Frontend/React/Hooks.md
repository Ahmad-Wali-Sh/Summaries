`Summary by Ahmad Wali Sharify`

Hooks allow us to "hook" into React Features such as state and lifecycle methods.

they are reusable functions. from React or custom third party including you.

    Hooks Rules:
    - Hooks can only be called inside React Functional Components 
    - Hooks can only be called at the top level of a component
    - Hooks cannot be conditional

## `useEffect`
---

To Perform side effects (Fetching Data, directly Updating `DOM`, and timers) in your components Use `useEffect`
Effects are external systems to be connected like `setInterval()` and more..

```jsx
useEffect(() {}, [])
```

```jsx
import { useState, useEffect } from "react";

function Timer() {
const [count, setCount] = useState(0);

useEffect(() => {setTimeout(() => 
        {setCount((count) => count + 1);}, 1000);},
 []);

```

dependencies can be added to [] in `useEffect` optional argument.

any time a dependency changes, function calls.

Some Effect require cleanup to reduce memory leaks
like timeouts, subscriptions, event listeners and other...

we do this by clean up in useEffect return 

```jsx
function Timer() {
const [count, setCount] = useState(0);

useEffect(() => {
let timer = setTimeout(() => {
  setCount((count) => count + 1);
}, 1000);
return () => clearTimeout(timer)
}, []);
```

useEffect for Fetching data is not so great, you can use your framework mechanism for fetching data.

## `useContext`
---

React Context is a way to manage state globally.

it can be used with the `useState` hook to share state between deeply nested components.

a solution to prop drilling.

to Create A Context: 

`Context.jsx`
```jsx
import { createContext } from "react";

export const ContextConfig = createContext()
App.jsx
import { useState } from 'react'
import './App.css'
import { ContextConfig } from './Context/Contexts'
import Component1 from './Components/Component1'


function App() {

  const [user, setUser] = useState('Ahmad')
  const [theme, setTheme] = useState('light')

  return (
      <ContextConfig.Provider value={{user, setUser, theme, setTheme}}>
        <Component1 />
      </ContextConfig.Provider>
  )
}

export default App
```

**Component1.jsx**
```jsx
import React from 'react'
import { useContext } from 'react'
import { ContextConfig } from '../Context/Contexts'

function Component1() {
    const Context = useContext(ContextConfig)

  return (
      <>
      <div className={Context.theme}>
        <div>{Context.user} and {Context.theme}</div>
          <button onClick={(e) => {
              Context.setUser('Hashim')
              Context.setTheme((prev) => prev == 'light' ? 'dark' : 'light')
              }
          }>
          Change
          </button>
      </div>
      </>
  )
}

export default Component1
```
    Steps: 
      1. Create Context via createContext 
      2. Provide Root State values to Components
      3. Use and Edit State values vie useContext

## `useRef`
---

Allows you to persist values between renders.
A mutable value that not trigger re-render.

a reference for DOM Objects.

returns:
 an object, `current`

Manipulating the DOM with a ref:
```jsx
import { useRef }  from 'react';
function inputRef = useRef(null);

function handleClick () {
  inputRef.current.focus();
}

return <input ref={inputRef} />
```

<br>

## `useReducer`
---

`useReducer()` is the hook for extracting state management out of the component.

structure:
```jsx
const [state, dispatch] = useReducer(reducer, initialState)

function reducer (state, action) {
  let newState;
    switch(action.type) {
      case 'actionType':
        newState = {action.user.name}
    }
  return newState;
}

const action1 = {
  type: 'actionType'
  user: {
     name: 'Ahmad'
  }
}

onClick={() => dispatch(action1)}
```
Simply, set of actions to be done on state object conditionally using dispatch.

## `useMemo`
---

`useMemo` Hook returns a `memoized` value.

`memoization` is like `caching value` so it can be recalculated just in case it needed.

`useMemo` Runs only its `dependencies updates`.

Structure:
```jsx
const Count = useMemo(() => {function > value} , [dependency])
```
it is used for better performance. and is like `useCallBack` but it returns a value.

## `useCallBack`
---
`useCallback` Hook returns a `memoized` callback function.

a Function that only runs when its dependency updates. 

Like `useMemo`.
structure:
```jsx
const addTodo = useCallback(() => {funtion}, [dependency])
```
addTodo will run only if dependency changes and updates.
its for performance optimization, like `useMemo` but returns a function, not value

## Custom Hooks
---
    To Maintain DRY 'Don't Repeat Yourself' Principle in Coding. You Can Use React Custom Hooks to Achieve Similar Functionality across different Components.

Structure:
```jsx
const useCustomHook  = (params) => {
//functionality...
return [data, anything]
}

const [data, anything] = useCustomHook(params)
```
With This Structure, you can Share a logic to different part and components. 

Ex:

```jsx
const useFetch = (url) => {
  const [data, setData] = useState(null);

  useEffect(() => {
    fetch(url)
      .then((res) => res.json())
      .then((data) => setData(data));
  }, [url]);

  return [data];
};

const [data] = useFetch('api.address')
```


