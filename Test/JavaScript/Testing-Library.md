`Summary: Ahmad Wali Sharify`

the `@testing-library` family of packages helps you test UI components in a user-centric way.

a light-weight solution for testing web pages by querying and interacting with DOM nodes.
### Queries

Query is for **selecting** Elements to fire *events* on them or *assert* them using `jest` or `jest-dom`

`example.js`
```javascript
import { render, screen } from '@testing-library/react'

test('should show login form', () => {
	render{<Login />}
	const input = screen.getByLabelText('Username')
	// Events and Assertions...
})
```


#### Types of Queries

- Single Elements
	- `getBy...` returns the matching node, throw error if no elements or more than one elements countered. 
	- `queryBy` returns the matching node for a query, `null` if none, throws `error` if more than one countered.
	- `findBy` returns a Promise which resolves when an elements is found which matches the given query, after 1000ms (default), rejected if no element is found or more than one. 
- Multiple Elements
	- `getAllBy...` returns an array of all matching nodes, throw error if no encounter 
	- `queryAllBy` returns an array of all matching nodes, empty array if no elements
	- `findAllBy...` return a promise which resolve to an array of elements, rejected in 1000ms if no element encounter

#### Priority

1. `getByRole` like `getByRole('button', {name: /submit/i})`
2. `getByLabelText` for form Fields
3. `getByPlaceholderText`
4. `getByText` text contents to find elements
5. `getByDisplayValue` the current value of a form element
6. `getByAltText` for alt texts in `area`, `input` and `img`
7. `getByTitle` the title attribute

#### Using Queries

primary argument to a query can be a string, regular expression or function.

```html
<body>
	<diV>
		<label for='username-input'>Username</label>
		<input id='username-input'/>
	</div>
</body>
```

```javascript
import { screen, getByLabelText } from '@testing-library/dom'

const inputNode = screen.getByLabelText('Username')
```

#### `queryOptions`

#####  `TextMatch`

most of query APIs take a Text as an argument.

```html
<div>Hello World</div>
```

```javascript
screen.getByText('Hello World')
screen.getByText('llo Worl', {excat: false})

screen.getByText(/World/i) // substring match, ignore case

screen.getByText((content, element) => content.startsWith('Hello'))

screen.getByText((content, element) => {
	return element.tabName.toLowerCase() === 'span' && content.startsWith('Hello')
})
```


---

### Firing Events

`fire-event` and `userEvent` are utilities for simulating user interactions in your tests.

#### `fire-event` 

is a lower-level dispatches synthetic events directly to a DOM element.
```javascript
import { fireEvent, render } from '@testing-library/react'
import MyComponent from './MyComponent'

test('clicks a button', () => {
	const { getByText } = render(<MyComponent />)
	const button = getByText('Submit')

	fireEvent.click(button)
	expect(button).toBeDisabled();
})
```
structure:
```javascript
fireEvent[eventName](node: HTMLElement, eventProperties: Object)
```

#### Target:
when an event is dispatched on an element, the event has the subjected element on a property called target, you can assign values to target as an option

```javascript
fireEvent.change(getByLabelText(/username/i), {target: { value: 'a'}})
```

#### `dataTransfer`

properties as `dataTransfer` will be added to the event.

```javascript
fireEvent.drop(getByLabelText(/drop files here/i), {
	dataTransfer: {
		files: [new File([('__()__')], 'checking.png', {type : 'image/png'})]
	}
})
```

#### Keyboard Events:
`keeyPress`, `keyDown`, `keyUp`

```javascript
fireEvent.keyDown(domNode, {key: 'Enter', code: 'Enter', charCode: 13})
```

#### `createEvent`

```javascript
createEvent[eventName](node: HTMLElement, eventProperties: Object)

const MyEvent = createEvent.click(node, {button: 2})
fireEvent(node, MyEvent)
```

#### Using Jest Function Mocks

```javascript
import { render, screen, fireEvent} from '@testing-library/react'

const Button = ({onClick, children}) => (
	<button onClick={onClick}>{children}</button>
)

test('calls onClick prop when clicked', () => {
	const handleClick = jest.fn()
	render(<Button onClick={handleClick}>Click Me</Button>)
	fireEvent.click(screen.getByText(/click me/i))
	expect(handleClick).toHaveBeeCalledTimes(1)
})
```

#### Async Methods

`findBy`, `waitFor`, `waitForElementToBeRemoved`

```javascript
const button = screen.getByRole('button', {name: 'Click Me'})
fireEvent.click(button)
await screen.findByText('Clicked Once')
fireEvnet.click(button)


await waitFor(() => {
	expect(MockAPI).toHaveBeenCalledTimes(1)
})

waitForElementToBeRemoved(document.querySelectro('div.getOuttaHere')).then(() => {
	console.log('Element Removed')
})
el.parentElement.removeChild(el)

await waitFor(() => {
	expect(queryByText('i, robot')).not.toBeInTheDocument()
})
```

