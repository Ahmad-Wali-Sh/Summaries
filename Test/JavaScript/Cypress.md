with cypress, write e2e, component, integration and unit test tests fast, easier and more reliable.

- Time Travel
- Debuggability
- Automatic Waiting
- Spies, Stubs and Clocks
- Network Traffic Control
- Consistent Result
- Screenshots
- Cross Browser Testing
- Smart Orchestration
- Flake Detection

Cypress designed to run end-to-end tests in a browser like a real-user would.

`E2E`:
```javascript
it('add todos', () => {
	cy.visit('localhost:3000')
	cy.get('[new-todo]')
		.type('write code{enter}')
	cy.get('to-dos').should('have.length', 2)
})
```

`Component`:
```javascript
impot TodoList import './components/TodoList'

it('contains the correct number of todos', () => {
	cy.mount(<TodoList todos={todos}/>)
	cy.get('[data-testid="todos"]').should('have.length', todos.length)
})
```

`API`:
```javascript
it('add a todo', () => {
	cy.request({
		url: '/todos',
		method: 'POST',
		body: {
			title: 'write rest Api'
		}
	})
		.its('body')
		.should('deep.contain', {
			title: 'Write Rest API',
			completed: false
		})
})
```


installation:

```bash
npm install cypress --save-dev 
```

opening: 
```javascript
npx cypress open

// or

{
	"scripts": {
		"cy:open": 'cypress open'
	}
}
```

After opening launchpad:
1. E2E Testing - run whole application and visit pages and test
2. Component Testing - mount individual components of app and test them in isolation

### End-to-End Testing

Create new spec file where it can be used for testing application.

#### Writing Test

Steps:
1. Visit a Page `cy.visit()`
2. Query for an element `cy.contains()`
3. Click an Element `.click()`
4. Make an Assertion `should()`

example:
```javascript
describe('My First Test', () => {
	it('Visits the Kitchen Sink', () => {
		cy.visit('https://example.cypress.io')
		cy.contains('type').click()
		// should be on a new URL which
		// includes '/commands/actions'
		cy.url().should('include', './commands/actions')

		// get an input by class, type into it
		cy.get('.action-email').type('fake@email.com')
		// verify if input value is updated
		cy.get('.action-email').should('have.value', 'fake@email.com')
	})
})
```

> A solid Test generally covers 3 phases:
> 	1. Set Up the application state
> 	2. Take an Action
> 	3. Make an assertion about the resulting application state.
> or: Given, When, Then or Arrange, Act, Assert

---
### Testing Your App

1. Start Your Server
2. Visit Your Server
3. Configure Cypress

```javascript
// cypress.config.js
const { defineConfig} = require('cypress')

module.exports = defineConfig({
	e2e: {
		baseUrl: 'httl://localhost:3000'
	}
})
```

```javascript
// home_page_spce.cy.js
describe('The Home Page', () => {
	it('succecfully loads', () => {
		cy.visit("/")
	})
})
```

#### Seeding Data

- `cy.exec()` to run system commands
- `cy.task()` to run code in Node via the `setupNodeEvents` function
- `cy.request()` to make HTTP request

#### Stubbing the Server
you can stub JSON responses coming from server. with this, build out your application without the backend server. and don't synchronize the state browser. 


#### Logging in

```javascript
describe('Login page', () => {
	it('set auth cookie when logging in via form submission', () => {
		const username = 'admin'
		const password = 123456;

		cy.vist('/login')
		cy.get('input[name=username]').type(username)
		cy.get('input[name=password]').type(`${password}{enter}`)

		cy.url().should('include', '/dashboard')
		cy.getCookie('your-session-cokie').should('exist;)
		cy.get('h1').should('contain', 'Ahmad Wali')
	})
})
```

#### Custom Commands

```javascript
// in cypress/support/commands.js
Cypress.Commands.add('login', (username, password) => {
		cy.vist('/login')
		cy.get('input[name=username]').type(username)
		cy.get('input[name=password]').type(`${password}{enter}`)

		cy.url().should('include', '/dashboard')
		cy.getCookie('your-session-cokie').should('exist;)
		cy.get('h1').should('contain', 'Ahmad Wali')
})
// in spec file
it('does somthing on secured page', () => {
	cy.login('admin',123456)
})
```

`cy.session()` command a powerful performance tool that lets you cache browser context associated with your user.

```javascript
// cy.seesion(id, setup)
Cypress.Commands.add('login', (username, password) => {
	cy.session(
		username,
		() => {
		cy.vist('/login')
		cy.get('input[name=username]').type(username)
		cy.get('input[name=password]').type(`${password}{enter}`)

		cy.url().should('include', '/dashboard')
		cy.get('h1').should('contain', 'Ahmad Wali')
		},
		{
			validate: () => {
				cy.getCookie('your-session').should('exist')
			},
		}
	)
})
```



---

### Core Concepts 

Cypress can be simple:
```javascript
describe('Post Resource', () => {
	it('Creating a Post', () => {
		cy.visit('/posts/new')

		cy.get('input.post-title')
			.type('My First Post')
		cy.get('input.post-body')
			.type('Hello World')
		cy.contains('Submit')
			.click()
		cy.get('h1')
			.should('contain', "My First Post")
	})
})
```

#### Querying Elements

```javascript
// Query by jQuery

cy.get('.my-selector') // select elements with my-selector class
cy.get('*') // select all elements
cy.get('#myId') // select element with myID id
cy.get(this) // select the current HTML element
cy.get('p.intro') // select pelements with class=intro
cy.get('p:first') // select the first p element
cy.get('ul li:first') // select the first <li> element of the first <ul>
cy.get("ul li:first-child") // select the first <li> of all <ul>
cy.get("[href]") // select all elements with href attribute
cy.get("a[target='_blank']") // select all a elements with a target attribue equal to
cy.get("a[target!='_blank']") // all <a> target value NOT equal to "_blank"
cy.get("tr:even") // select all even <tr> elements
cy.get("tr:odd") // select odd <tr> elements 
cy.get(":button") // select all <button> and <input> with type button

// Querying by Text content
cy.contains('New Post')
cy.get('main').contains('New Post')
```

#### Chains of Commands

```javascript
cy.get('textarea.post-body').type('This is an excellent post.')
// or
.blur() // makes element blur
.focus() // focus on DOM element
.clear() // clear the value of an input or textarea
.check() // check checkboxes or radios
.uncheck() // uncheck checkboxes
.select() // select an option within a select, e.g: .select('user-1')
.dblclick() // double-click a DOM element
.rightclick() // Right-click a DOM element
```

#### Asserting about Elements

```javascript
cy.get(':checkbox').should('be.disabled')
cy.get('form').should('have.class', 'form-horizontal')
cy.get('input').should('not.have.value', 'US')
```

#### Using `.then()` to Act on A Subject

```javascript
cy
	.get('#some-link')
	.then(($myElement) => {
		const href = $myElement.prop('href')
		return href.replace(/(#.*)/, '')
	})
	.then((href) => {
		// the new subject
	})
```

#### Using Aliases to Refer to Previous Subjects

```javascript
cy.get('.my-selector')
	.as('MyElement')
	.click()

cy.get('@MyElement')
	.click()
```

#### Assertions 

Assertions describe the *desired* state of your elements, your objects, and your application.
*with cypress, you can test without assertion explicitly*

```javascript

// assertions with should()
cy.request('/users/1').its('body').should('deep.eq', { name: 'Wali'})
cy.get('tbody tr:first').should('have.class', 'active')


// assertions with and()
cy.get('#header a')
	.should('have.class', 'active')
	.and('have.attr', 'href', '/users') // and() is another should() name

// assrtions with Mocha and Chai
expect(true).to.be.true

```




