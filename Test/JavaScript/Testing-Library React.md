`Summary: Ahmad Wali Sharify`
installation:

```bash
npm install --save-dev @testing-library/react @testing-library/dom
```

a very light-weight solution for testing React Components. 

Example:
```javascript
import {render, screen} from '@testing-library/react'
import userEvent from '@testing-library/user-event'
import '@testing-library/jest-dom'
import Fetch from './fetch'

test('loads and displays greeting', async () => {
	render(<Fetch url="/greeting"/>)

	await userEvent.click(screen.getByText('Load Greeting'))

	expect(screen.getByRole('heading')).toHavbeTextContent('hello threre')

})
```

### API

#### `render`

```javascript
function render (
	ui: React.ReactElement<any>,
	options?: {}
)
```

```javascript
import {render} from '@testing-library/react'

render(<div />)

// reulsts: DOM Testing Library Queries, renderer (for re-render), unmount
const { getByBableText, // All queries
	   renderer, 
	   unmount } = render(<NumberDisplay number={1} />)

rerender(<NumberDisplay number={2} />)  /// re-render with new prop
unmount() // unmount the element (component)

```

#### `cleanup`

Unmounts React tree that were mounted with render

```javascript
import { cleanup, render } from '@testing-library/react'
afterEach(cleanup)
```

#### `renderHook`

```javascript
import { renderHook } from '@testing-library/react'

test('return logged user', () => {
	const { result } = renderHook(() => useLoggedInUser())
	expect(result.current).toEqual({name: 'Alice'})
})
```