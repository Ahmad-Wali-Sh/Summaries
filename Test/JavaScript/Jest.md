`Summary: Ahmad Wali Sharify`
Jest is a delightful JavaScript Testing Framework with a focus on simplicity.

for installing:
```bash
npm install --save-dev jest
```

Simple Usage:

declaration of a function
sum.js:
```javascript
function sum(a, b) {  
return a + b;
}

module.exports = sum;
```

declaration of the test
sum.test.js
```javascript
const sum = require('./sum.js')
test('sum testing functionality', () => {
	expect(sum(1,2)).toBe(3)
})
```

with `npm test`
testing passes successfully.

---

### Matchers 
`expect()` function has some matchers to test values in different ways.


**`.toBe()`**
`expect(data).toBe(data)` checks for exact value and memory location.

**`.toEqual()
`expect(data).toEqual(data)` checks for exact value.

**`.toStrictEqual()
`expect(data).toStrictEqual(data)` checks for exact value not ignoring undefined properties

**`.not.***()
`expect(data).not.toBe(!data)` check the opposite of `toBe`.

#### Truthiness

`toBeNull` matches only `null`
`toBeUndefined` matches only `undefined`
`toBeDefined` is the opposite of `toBeUndefined`
`toBeTruthy` matches anything that an `if` statement treats as true
`toBeFalsy` matches anything that an `if` statement treats as false

#### Numbers

`toBeGreaterThan` checks if value is greater than.
`toBeGreaterThanOrEqual` checks if value is greater or equal
`toBeLessThan` checks if value is less than.
`toBeLessThanOrEqual` checks if value is less or equal
`toBeCloseTo` checks for floating numbers

#### Strings

`toMatch` checks string against a regular expression

```javascript
test('there is no I in team', () => { 
	expect('team').not.toMatch(/I/);
});

test('but there is a "stop" in Christoph', () => {  
	expect('Christoph').toMatch(/stop/);
});
```


#### Arrays and Iterables 

`toContain` check an array or iterable contains a particular item.

#### Exceptions

whether a particular function throws an error. you can use `toThrow`

#### Promises

Return a promise from your test, and Jest will wait for that promise to resolve.

```javascript
test('the data is peanut butter', () => {
	return fetchData().then(data) => {
		expect(data).toBe('peanut butter')
	}
})
```

#### Async/Await

Alternatively, you can use `async` and `await` in your tests.

```javascript
test('the data is peanut butter', async () => {
	const data = await fetchData();
	expect(data).toBe('peanut Butter')
})

//or

test('the data is peanut butter', async () => {  
	await expect(fetchData()).resolves.toBe('peanut butter');
});

test('the fetch fails with an error', async () => {  
	await expect(fetchData()).rejects.toMatch('error');
});
```


#### Callbacks

```javascript
test('the data is peanut butter', done => {  
	function callback(error, data) {
	    if (error) {
	        done(error);
	        return;
	    } 
	    try {   
	       expect(data).toBe('peanut butter');
	        done();   
	    } 
	    catch (error) {
	          done(error);
	    }}
	    fetchData(callback);
	    });
// done is actuly a parameters that is called to end the test
```


---

### Setup and Teardown

you can run some functions before testing occurs or after it.

#### Repeating Setup & One-Time Setup

if you want to repeatedly do something for many test, you can use `beforeEach` and `afterEach`.
or you can run a function in the beginning of a test process or after it one time.

```javascript

// Repeating Setup
beforeEach(() => {
	return inicializeDatabase(); // for promises
})

afterEach(() => {
	return deleteDatabase(); // for promises
})

// One-Time Setup
beforeAll(() => {
	return initializeCityDatabase()
})

afterAll(() => {
	return clearCityDatabase();
})

//not: you can use these in a scope like describe to do that in your describe block only
```

#### `.only`

a `test.only()` will temporarily just test one test in the entire project.


---

### Mocking Functions

Mock functions allow you to test the links between code by `erasing the actual implementation` of a function, `capturing calls to the function` (and the parameters passed in those calls), `capturing instances` of constructor functions when instantiated with new, and allowing `test-time configuration` of return values.


#### Using a Mock function

```javascript
//forEach.js
export function forEach(items, callback) {
	for (const item of items) {
		callback(item)
	}
}


//forEach.test.js
const forEach = require('./forEach');

const mockCallback = jest.fn(x => 42 + x)

test('foreach mock function', () => {
	forEach([0,1], mockCallback);

	// the mock function calls twice
	expect(mockCallback.mock.calls).toHaveLength(2);

	// the first argument of the first call to the function was 0
	expect(mockCallback.mock.calls[0][0]).toBe(0);

	// the first argument of the second call to the function was 1
	expect(mockCallback.mock.calls[1][0]).toBe(1);

	// the return value of the first call to the function was 42
	expect(mockCallback.mock.results[0].toBe(42));
})

// all mock functions have this special .mock property that have details on function calls and results
```


#### Mock Return Values

```javascript
const MyMock = jest.fn()

MyMock.mockReturnValueOnce(10).mockReturnValueOnce('x').mockReturnValue(true);

console.log(MyMock(), MyMock(), MyMock(), MyMock());
// > 10, x, true, true

const filterTestFn = jest.fn();

filterTestFn.mockReturnValueOnce(true).mockReturnValue(false);

const result = [11, 12].filter(num => filterTestFn(num));

console.log(result)
// > 11

console.log(filterTestFn.mock.calls[0][0]); // 11
console.log(filterTestFn.mock.calls[1][0]); // 12
```


### Mocking Modules

```javascript
//users.js

import axios from 'axios'

class Users {
	static all() {
		return axios.get('/users/json').then(resp => resp.data)
	}
}


//users.test.js
import axios from 'axios';
import Users from './users';

jest.mock('axios');

test('should fetch users', () => {
	const users = [{name: 'Bob'}]
	const resp = {data: users};
	axios.get.mockResolvedValue(resp);
	return Users.all().then(data => expect(data).toEqual(users));
})
```

#### Mock Implementation

```javascript
const myMockFn = jest
	.fn(()=> 'default')
	.mockImplementationOnce(() => 'first call')
	.mockImplementationOnce(() => 'second call')

console.log(myMockFn(),myMockFn(),myMockFn(),myMockFn())
// > 'first call', second call, default, default
```

#### Mock Names

```javascript
const myMockFn = jest
	.fn()
	.mockReturnValue('default')
	.mockImplementation(scalar => 42 + scalar)
	.mockName('add42');

// the test name will through mockName to quickly identify it.
```

#### Custom Matchers for Mock functions

`expect(mockFunc).toHaveBeenCalled()` check the mock function at least called once
`expect(mockFunc).toHaveBeenCalledWith(arg1, arg2)` check the mock function at least called with these parameters once.

`expect(mockFunc).toHaveBeenLastCalledWith(arg1, arg2)` check the last call of mock function to be with these arguments

`expect(mockFunc).toMatchSnapshot()` all calls and the name is written as a snapshot.


*These matchers are sugar for common forms of inspecting the `.mock` property. You can always do this manually yourself if that's more to your taste or if you need to do something more specific.*

---

### Snapshot Testing

Snapshots are for testing UI does not change unexpectedly.

renders a UI component -> takes snapshot -> compares to reference stored

you can use `react-test-renderer` for rendering UI component

```javascript
import renderer from 'react-test-renderer'
import Link from '../Link';

it('renderes correctly', () => {
	const component = renderer
		.create(<Link page="http://www.facebook.com">Facebook</Link>)
	const tree = component.toJSON()
	expect(tree).toMatchSnapshot();

	// manually trigger the callback
	renderer.act(() => {
		tree.props.onMouseEnter()
	})

	//re-render
	tree = component.toJSON()
	expect(tree).toMatchSnapshot()
})

// for first test, it will generate a snapshot file. and it should be commited into version control.
```

use `jest -u` or `jest --updateSnapshot` to update snapshot.

#### Inline Snapshots

inline snapshot behave identically to external snapshot (.snap) file but it is written automatically back into source code!


```javascript
it('renderes Link Correctly', () => {
	const tree = renderer
		.create(<Link page='www.instagram.com'>Instagram</Link>)
		.toJSON();
	expect(tree).toMatchInlineSnapshot();

})

// next time after test, file will look like this:
it('renderes Link Correctly', () => {
	const tree = rendere
		.create(<Link page='www.instagram.com'>Instagram</Link>)
		.toJSON();
	expect(tree).toMatchInlineSnapshot(`
	<a
		classname='normal'
		href='www.instagram.com'
		onMouseEnter={[Function]}
		onMouseLeave={[Function]}
	> Instagram </a>
	`);
})
```

#### Property Matchers

```javascript
it('matchers and pass', () => {
	const user = {
		createAt: new Date(),
		id: Math.floor(Math.random() * 20),
		name: 'Lebron James'
	}
	expect(user).toMathcSnapshot({
		createdAt: expect.any(Date),
		id: expect.any(Number)
	})
})
```

#### Best Practices for snapshot testing

1. Treat snapshots as code
2. tests should be deterministic
3. use descriptive snapshot names 

---
### Testing React Apps

1. Snapshot testing (described)
2. DOM Testing

#### DOM Testing

you can use react testing library, enzyme or TestUtils.
using @testing-library/react

```bash
npm install --save-dev @testing-library/react
```

```javascript
import {cleanup, fireEvent,render} from '@testing-library/react'
import CheckboxWithLabel from '../somewhere'

afterEach(cleanup);

it('CheckboxWithLabel changes the text after click', () => {
	const { queryByLabelText, getByLabelText} = render(
		<CheckboxWithLabel labelOn='On' labelOff='off' />,
	)
	expect(queryByLabelText(/off/i)).toBeTruthy();
	fireEvent.click(getByLabelText(//off/i));
	expect(queryByLabelText(/on/i)).toBeTruthy();
})

```