### History

The JavaScript language was created in the mid 1990s to be executed in internet browsers.

The goal was to have the browser check as many things as possible and then transmit to server.

over the years, developers have had the idea of to use the same language on the client side and on the server side. this allowed the creation of the *Node.js* server.
### Types of variables used in JavaScript

- *Numerical* Values
	- Can be positive or negative even in decimal form
- *Boolean* Values
	- `true` or `false`, for expressing conditions.
- *Character* Strings
	- Character strings refer to values such as `"a"`, `"ABC"`
- *Arrays*
	- can contain values of any type, accessible by index varying from `0` to the length of the array `minus 1`
	- `let array = [1, 'bye']`
- *Objects*
	- similar to Arrays, used to store arbitrary information, but unlike arrays, you should specify a name to access each of these values. called *key or property*
	- `let person = { age: 43, lastName: "Sharify"}` is a *JavaScript Object Notation: (JSON)*
	- `person["age"]` returns 43

#### Declaring variables in JavaScript

JavaScript is a weakly typed language, which means that you can change the type of a variable at any time.

More strong typed language for JavaScript is *TypeScript*

Three types of defining variables in JavaScript:
- `const` constant values
- `let` scoped variables
- `var` non-scoped variables
### Writing conditions
```javascript
if (condition) {
	statements 1;
}
else if (condition) {
	statements 2;
}
else {
	statements 3;
}
// or
switch (variable) {
	case 'a': // if the variable equals a
		statements 1;
		break;
	case 'b':
		statements 2;
	default // the else statement
		statements 3;
}
```

#### Expressions used to write conditions

```txt
	=== equals 
	>= <= greater or smaller 
	&& AND (if two condition are true at the same time)
	|| OR (if one of two conditions are true at least)
	! Not (changes the condition boolean value)
```
### Creating processing loops

It is sometimes necessary to repeat an instruction or a block of instructions several times, 

2 types in JavaScript:
	- `while()`
	- `for()`
#### `while()`

a loop that continues as long as a condition true.

```javascript
let i = 0
while (i <= 5) {
	console.log("i = " + i)
	i++
}
```

#### `for()`
it offers a structure
`for (variable inicializing; condition; on_each_run) { statement }`

```javascript
	for (var i=0; i <= 5; i++) console.log("i = " + i)
```

### Using Functions
giving a name to a block of instructions so that it can be used in different places in the program. grouping set of instructions to carry out a particular task.

```javascript
function FunctionName () {
	statements;
}

function total_n_first_integers (n) {
	let total = 0;
	for (let i = 0; i <= n; i++){
		total += i;
	}
	return total
}
let total_10 = total_n_first_integers(10)
```

