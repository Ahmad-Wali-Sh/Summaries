This is not a style guide. It’s a guide to producing
readable, reusable, and refactorable software in JavaScript.

> Don’t beat yourself up for first drafts that need improvement.
> Beat up the code instead!

### Variables

1. Use Meaningful and pronounceable variable names
2. Use the same vocabulary for the same type of variable
3. Use Searchable Names
4. Avoid Mental Mapping
5. Don’t add unneeded context
6. Use default parameters instead of short circuiting or conditionals

```javascript
// Meaningfull names
const currentDate = moment().format('YYYY/MM/DD')

// Same vocabulary
getUser(); // not getUserInfo(), getClientData()

// Searchable names
const MILLISECONDS_PER_DAY = 60 * 60 * 24 * 1000; // 86400000

// Avoid Mental Mapping
locations.forEach(location => { // not l, for location
dispatch(location);
});

// Don’t add unneeded context
const Car = {
	carMake: 'Honda', // correct: make
	carModel: 'Accord', // correct: model
}

// default parameters instead of short circuiting or conditionals
function createMicrobrewery(name = "Hipster Brew Co.") {
// ...
}
```

### Functions

1. Function arguments (2 or fewer ideally), destructure it if necessary 
2. Functions should do one thing, isolate to one action
3. Function names should say what they do
4. Functions should only be one level of abstraction
5. Remove duplicate code
6. Set default objects with `Object.assign`
7. Don’t use flags as function parameters
8. Avoid Side Effect
9. Don’t write to global functions
10. Favor functional programming over imperative programming
11. Encapsulate conditionals
12. Avoid negative conditionals
13. Avoid conditionals
14. Avoid type-checking
15. Don’t over-optimize
16. Remove dead code

```javascript
// function arguments (2 or fewer) or destructuring it
function createMenu ({title, body, buttoonText, cancellable}) {
 // ...
}
createMenu({
	title: 'Foo', 
	body: 'Bar', 
	buttonText:'Baz', 
	cancellable: true
});
```

```javascript
// Functions should do one thing (important)
function emailActiveClients (clients) {
	clients.filter(isActiveClient).forEach(email)
};
function isActiveClient(client) {
	const clientRecord = database.lookup(client);
	return clientRecord.isActive();
}
```

```javascript
// Function Names should say what they do
function addMonthToDate (month, date) {
 // ...
}
const date = new Date();
addMonthToDate(1, date);
```

```javascript
// avoid duplicate code, abstraction right is critical, use SOLID
function showEmployeeList(employees) {
	employees.forEach(employee => {
	const expectedSalary = employee.calculateExpectedSalary();
	const experience = employee.getExperience();

	const data = {
		expectedSalary,
		experience
	};
	switch (employee.type) {
		case "manager":
			data.portfolio = employee.getMBAProjects();
			break;
		case "developer":
			data.githubLink = employee.getGithubLink();
		break;
	}
	render(data);
	});
}
```

```javascript
// Set default objects with Object.assign
const menuConfig = {
	title: "Order",
	buttonText: "Send",
	cancellable: true
};

function createMenu(config) {
	let finalConfig = Object.assign({
			title: "Foo",
			body: "Bar",
			buttonText: "Baz",
			cancellable: true
			}, config);
	
	return finalConfig
		// config now equals: {title: "Order", body: "Bar", buttonText: "Send",
		// cancellable: true}
}

createMenu(menuConfig);
```

```javascript
// Don’t use flags as function parameters
function createFile(name) { // aginst createFile(name, temp) for flag for temp
	fs.create(name);
}
function createTempFile(name) {
	createFile(`./temp/${name}`);
}
```

```javascript
// Avoid Side Effect 1
const addItemToCart = (cart, item) => {
	return [...cart, { item, date: Date.now() }];
};
// Avoid Side Effects 2
function splitIntoFirstAndLastName(name) {
	return name.split(" ");
}
const name = "Ryan McDermott";
const newName = splitIntoFirstAndLastName(name);
```

```javascript
// Encapsulate conditionals 
function shouldShowSpinner(fsm, listNode) {
	return fsm.state === "fetching" && isEmpty(listNode);
}
if (shouldShowSpinner(fsmInstance, listNodeInstance)) {
// ...
}
```


### Objects and Data Structures

1. Use getters and setters
2. Make objects have private members

```javascript
// Use Getters and Setters

function makeBankAccount() {
	// this one is private
	let balance = 0;
		// a "getter", made public via the returned object below
	function getBalance() {
		return balance;
	}
		// a "setter", made public via the returned object below
	function setBalance(amount) {
		// ... validate before updating the balance
		balance = amount;
	}
	return {
		getBalance,
		setBalance
	};
}
const account = makeBankAccount();
account.setBalance(100)
```

```javascript
// Make Objects have private memebers

function makeEmployee(name) {
	return {
		getName() {
			return name;
		}
	};
}
const employee = makeEmployee("John Doe");
console.log(`Employee name: ${employee.getName()}`); // Employee name: John Doe
delete employee.name;
console.log(`Employee name: ${employee.getName()}`); // Employee name: John Doe
```


### Classes

1. Prefer ES2015/ES6 classes over ES5 plain functions
2. Use method chaining
3. Prefer composition over inheritance

```javascript
// Prefer ES2015/ES6 classes over ES5 plain functions
class Animal {
	constructor(age) {
		this.age = age;
	}
	move() {
	}
}

class Mammal extends Animal {
	constructor(age, furColor) {
		super(age);
		this.furColor = furColor;
	}
	liveBirth() {
	}
}

class Human extends Mammal {
	constructor(age, furColor, languageSpoken) {
		super(age, furColor);
		this.languageSpoken = languageSpoken;
	}
	speak() {
	}
}
```

```javascript
// Use Method chaining
class Car {
	constructor(make, model, color) {
		this.make = make;
		this.model = model;
		this.color = color;
	}
	setMake(make) {
		this.make = make;
		// NOTE: Returning this for chaining
		return this;
	}
	setModel(model) {
		this.model = model;
		// NOTE: Returning this for chaining
		return this;
	}
	setColor(color) {
		this.color = color;
		// NOTE: Returning this for chaining
		return this;
	}
	save() {
		console.log(this.make, this.model, this.color);
		// NOTE: Returning this for chaining
		return this;
	}
}
const car = new Car("Ford", "F-150", "red").setColor("pink").save() // important part
```

```javascript
// Prefer compostion
class EmployeeTaxData {
	constructor(ssn, salary) {
		this.ssn = ssn;
		this.salary = salary;
	}
}
class Employee {
	constructor(name, email) {
		this.name = name;
		this.email = email;
	}
	setTaxData(ssn, salary) {
	this.taxData = new EmployeeTaxData(ssn, salary);
	}
}
```

### SOLID

1. Single Responsibility Principle (SRP)
2. Open/Closed Principle (OCP)
3. Liskov Substitution Principle (LSP)
4. Interface Segregation Principle (ISP)
5. Dependency Inversion Principle (DIP)

```javascript
// SRP
function calculateSalary(employee) {
    return employee.hoursWorked * employee.hourlyRate;
}

function generateReport(employee, salary) {
    let report = /*...*/;
    console.log(report);
}
```

```javascript
// OCP, Open to extend, close to modify
function processPaymentWithPayPal(price, accountDetails) {
    /*...*/
    console.log('Payed with PayPal.');
}
```

```javascript
// LSP
function makeRequest(url, errorHandler) {
    fetch(url)
        .then(response => response.json())
        .catch(error => errorHandler.handle(error))
    }

// We can have several functions to handle errors
const consoleErrorHandler = function handle(error){
    console.log(error)
}

const externalErrorHandler = function handle(error){
    sendErrorToExternalService(error)
}

makeRequest(url, consoleErrorHandler);
makeRequest(url, externalErrorHandler);

```

```javascript
// ISP, no class should be forced to implement interfaces or methods that it will not // use.
class Product {
    constructor() { /* */ }

    getDetails() { /* */ }
    saveToDb() {/* */ }
    displayInFrontEnd() { /* */ }
}

class DigitalProduct extends Product{
    // saveToDb() is extended but not necessary }
}

// Refactor

class Product {
    constructor() { /* */ }

    getDetails() { /* */ }
    displayInFrontEnd() { /* */ }
}

class PhysicalProduct extends Product {
    constructor() {
        super()
    }
    saveToDb() { /* */ }
}

class DigitalProduct extends Product{
    // saveToDb() is not extended
}
```

```javascript
// DIP, High level functionality and classes should not depend on low-level function /n //(MySQLConnetion)
class MySqlConnection {
    connect() { /* */ }
}

class PasswordReminder {
    constructor() {
        this.dbConnection = new MySQLConnection();
    }
}

// Refactor
class MySqlConnection {
    connect() { /* */ }
}
class PostgreSqlConnection {
    connect() { /* */ }
}

class PasswordReminder {
    constructor(connection) {
        this.dbConnection = connection
    }
}

```


### Test

1. Single concept per test

```javascript
import assert from "assert";
describe("MomentJS", () => {
	it("handles 30-day months", () => {
		const date = new MomentJS("1/1/2015");
		date.addDays(30);
		assert.equal("1/31/2015", date);
	});
	it("handles leap year", () => {
		const date = new MomentJS("2/1/2016");
		date.addDays(28);
		assert.equal("02/29/2016", date);
	});
	it("handles non-leap year", () => {
		const date = new MomentJS("2/1/2015");
		date.addDays(28);
		assert.equal("03/01/2015", date);
	});
});
```

### Concurrency 

1. Use Promises, not callbacks
2. Async/Await are even cleaner than Promises

```javascript
import { get } from "request-promise";
import { writeFile } from "fs-extra";

async function getCleanCodeArticle() {
	try {
		const body = await get(
			"https://en.wikipedia.org/wiki/Robert_Cecil_Martin"
		);
		await writeFile("article.html", body);
		console.log("File written");
	} catch (err) {
	console.error(err);
	}
}
getCleanCodeArticle()
```


### Error Handling

> Thrown errors are a good thing!

1. Don’t ignore caught errors
2. Don’t ignore rejected promises

```javascript
try {
	functionThatMightThrow();
} catch (error) {
	// One option (more noisy than console.log):
	console.error(error);
	// Another option:
	notifyUserOfError(error);
	// Another option:
	reportErrorToService(error);
	// OR do all three!
}
```



### Formatting 

> DO NOT ARGUE over formatting

1. Use consistent capitalization
2. Function callers and callers should be close

### Comments 

1. Only comment things that have business logic complexity
2. Don’t leave commented out code in your codebase
3. Don’t have journal comments
4. Avoid positional markers