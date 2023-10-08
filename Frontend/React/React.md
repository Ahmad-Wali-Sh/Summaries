# React

`Summary by Ahmad Wali Sharify`

    React is a Project From Facebook in 2013
    A Frontend JavaScript Framework for User Interfaces.

its main target was to implement an entire page more Real-time
so they implement a way to describe a Virtual DOM, that updates rapidly the Actual DOM. By Comparing Differences.

- React is based on `Components` (Small Chunks For Different part of UI) that has there own interface and functions.

- React use `JSX (JavaScript XML)` to write HTML into JavaScript.

- React use `Props` in components to send different data from 
parent to child components.

- React use `States` in Components to set changeable values accordingly and real-time that they make entire Component re render and then Actual DOM.

- React use `Hooks` in Functional Components to do anything Class Components Can Like State and Context and More.

<br>

## Configuration With Vite
---
Vite is Like Create React App Package Manager, that is more scalable and paper wight. using it is so easy and maintainable. 

```
npm create vite@latest
? Project name: >> your-app-name
use arrow keys to React
use Javascript or Typescript
```
then:
```
cd path-to-vite-project
npm install
npm run dev 
```
**vite.config.ts**
```javascript
import { defineConfig } from 'vite'
import react from '@vitejs/plugin-react'

// https://vitejs.dev/config/
export default defineConfig({
  server: {
    port: 3000
    // to start port 3000
  },
  plugins: [react()],
})
```

<br>

# Components

They are small chunks of a big app, they have there functions, data, states, styling individually.  

Two Kind of Components:
- Functional Components
- Class Components



## `Functional Component:` 
```jsx
import React from 'react'

export default function MyFirstComponent (props) {
  return <h1>Hi Dev World</h1>
}

import MyFirstComponent from './components/MyFirstComponent'

function App () {
  return (
  <div>
     <MyFirstComponent />
  </div>
  )
}
```
    Note: any Component can return just one element that can has other elements. that is a law.

## `Class Components:`

- Class Components are more Ordered and needs more attention. 
- it has a state object in constructor.
- all states properties are in one object.
- use this.setState to Change a state.
- We use this.props to add some props to declare later on its parent.

```jsx
class {ComponentName} extends React.Component {
	constructor (props){
	  super(props);
	  this.state = { color: "yellow"}
}
render () {
	return (
    	<>
          <h1 onClick={()=> {this.setState({color: "blue"})}}>
              This is a text {this.state.color}
          </h1>
          <h2>This is a text with props {this.props.angle}</h2>
        </>
    )
}
```

<br>

# States with useState hook

`State` in React means **Current data** or a data that needs to be tracking in an application.

`useState` returns two values: 
- Current State
- a function that updates the state.

```jsx
import { useState } from 'react'

fucntion FavoriteColor () {
  const [color, setColor] = useState("")
}

const [car, setCar] = useState({
  brand: "ford",
  model: "mustang",
  year: "1945",
  color: "red"
})

// to update our object state:
setCar(prevState => {
  return { ...prevState, color: 'blue'} 
})
```

<br>



