
is a higher-level utility that simulate more realistic user interactions.
```javascript
import { render } from '@testing-library/react'
import userEvent from '@testing-library/user-event'
import MyComponent from './MyComponent';

test('types into field', async () => {
	const { getByLabelText } = render(<MyComponet />)
	const input = getByLabelText('Name');
	const user = userEvent.setup() // setup userEvent first

	await user.type(input, 'Jhon Doe');

	expect(input).toHaveValue('Jhon Doe')

	await user.keyboard('[ShiftLeft>]') // press shift without release
	await user.click(input) // perform a click with shiftKey: ture
})
```

installation:
```bash
npm install --save-dev @testing-library/user-event
```

#### Pointer

```javascript
const user = userEvent.setup()
user.pointer(input: PointerInput): Promise<void>

// simulate interaction with pointer devices.

user.pointer({target: button, keys: '[MouseLeft]'})

user.pointer('[MouseLeft>]') // press the left mouse button
user.pointer('[/MouseLeft]') // relase the left mouse button

user.pointer([
	{keys: '[TouchA>]', target: element1}, // thouch the element 1
	{pointerName: 'ThouchA', target: element2}, // move the thouch pointer to element2
	{keys: '[/TouchA]'} // release the thouch pointer at the last posistion
])
```


#### Keyboard

```javascript
const user = userEvent.setup()
user.keyboard(input: KeyboardInput): Promise<void>

user.keyboard('foo')
user.keyboard('{Shift}{f}{o}{o}') // Shift, f, o, o


// **Special keys**: Use square brackets `[ ]` to represent non-character keys like:

- `[Enter]`, `[Tab]`, `[Escape]`, `[Backspace]`
- `[ArrowUp]`, `[ArrowDown]`, `[ArrowLeft]`, `[ArrowRight]`
- `[Shift]`, `[Ctrl]`, `[Alt]`, `[Meta]` (Windows/Command)
```

#### Utility APIs

```javascript
//clear()
await user.clear(screen.getByRole('textbox'))


//selectOption(), deselectOption()

await user.selectOptions(screen.getByRole('listbox'), ['1'. 'C'])
expect(screen.getByRold('option'), {name: 'A'}).selected).toBe(true)


//upload
const file = new File(['hello'], 'hello.png', {type: 'image/png'})
const input = screen.getByLabelText(/upload fiule/i)

await user.upload(input, file)
expect(input.files[0]).toBe(file)

```

#### Convenience APIs

```javascript
click() // pointer([{target: element}, {keys: '[MouseLeft]', target: element}])


dblClick() // pointer([{target: element}, {keys: '[MouseLeft][MouseLeft]', target: element}])

tripleClick() // pointer([  {target: element},  {keys: '[MouseLeft][MouseLeft][MouseLeft]', target: element},])

hover() // pointer({target: element})

unhover() // pointer({target: element.ownerDocument.body})

tab() // keyboard('{Tab}')// with shift=truekeyboard('{Shift>}{Tab}{/Shift}')// with shift=falsekeyboard('[/ShiftLeft][/ShiftRight]{Tab}')
```
