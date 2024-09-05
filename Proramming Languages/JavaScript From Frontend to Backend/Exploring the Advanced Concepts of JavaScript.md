
### Classes and Objects

the fundamental to programming languages.

A `class` is used to represent any type of data. ex people, customer, cars.

An `object` will be a particular element of a class (an instance of a `class`)

#### Defining a `class`

what actions you want to perform on the type of data it represents? it is important for creation of a class.

Characteristics such a first name are called *properties* of the class, while actions are called *methods*.

```javascript
// creating a class
class Person {
	firstname = ''; // with default value => firstname = ""
	lastname = '';
	age = 0;
	display () {
		console.log("name: " + this.firstname)
	}
}
// creating an instance of it (object)
let p = new Person;
p.firsname = "Ahmad"
p.display()
// name: Ahmad
```

you can create objects without classes using braces `{}`
```javascript
let p = { firstname: 'ahmad', lastname: 'sharify'}
```

#### Constructor

is a function that will be called every time an instance is in the creation process. it can take any number of parameters. 

```javascript
class Person {
	lastname = '';
	firstname = '';
	age = 0;
	constructor(lastname, firstname, age){
		this.lastname = lastname;
		this.firstname = firstname;
		this.age = age;
	}
	display() {
		console.log(this.lastname + this.firstname + this.age)
	}
}

let p = new Person('sharify', 'wali', 21)
p.display()
```

### Merging one `object` with another

to create a new object from old object.

```javascript
let p = { lastname: 'sharify', firstname: 'ahmad'}
let p2 = p
// p2 with p point to same memory location, any changes to both of them, reflects to both.

// to copy: spread operator.
let p = { lastname: 'sharify', firstname: 'ahmad'}
let p2 = {...p}; 
// now p and p2 different but p2 has properties of p
let p3 = {...p2, city: "New York"}
// p3 has all values of p2 with additional value.
```

### Arrays

`Arrays` store a collection of data, ordered according to their index.

Array corresponds in JavaScript to an Array class object. We Therefore use `new Array` instruction. or bracket notation `[]`

#### Creating an `array`

```javascript
let tab = ["Element 1", 'Element 2']
// or
let tab = new Array('Element 1', 'Element 2')

// for empty arrays:
let empty = [];
// or
let empty = new Array();
```

#### Accessing array elements

1. By its Index

```javascript
let tab = ['Element 1', 'Element 2']
tab[0]
// `Element 1`
```

2. Accessing an element with `for()` or `while()` loop

```javascript
let tab = ["Element 1", "Element 2", "Element 3", "Element 4", "Element 5"]
for (let i = 0; i < tab.length; i++) console.log("tab[" + 1 + "]=", tab[i])
```

3. Accessing an element with `forEach(callback)` method

it is a defined method in `Array class`, it used to browse the elements of an array by transmitting each of the elements of the array to a function passed as a parameter. 

> `Callback` function
	The Function in the parameters is known as a callback function.

```javascript
let tab = ["Element 1", "Element 2", "Element 3", "Element 4", "Element 5"]

tab.forEach(function (elem, i) {
	console.log("tab[" + i + "]=", elem)
})
```

#### Adding items to the Array

1. Adding an element by index
```javascript
let tab = ['Element 1']
tab[1] = 'Element 2'
// note that creating an element to a greater index, it makes undefined values in the array
```

2. Adding an element using the `push()` method
```javascript
let tab = ['Element 1', 'Element 2']
tab.push('Element 3')
```

#### Deleting Array elements

1. Deleting the value of the element in the array, while retaining the element in the array

```javascript
let tab = ['Element 1', 'Element 2', 'Element 3']
delete tab[0] // it assignes undefined value to tab[0]
// tab = [undefined, 'Element 1', 'Element 2']
```

2. Deleting an element from an Array
`splice(begin, count)` method indicate from which index you want to delete, and the number of consecutive elements you want to delete.

```javascript
let tab = ['Element 1', 'Element 2', 'Element 3']
tab.splice(0, 1)
// tab = ['Element 2', 'Element 3']
// or
tab.splice(1, 2)
// tab = ['Element 1']
```

#### Filtering elements in an Array

1. `filter(callback)`

The `tab.filter(callback(element, index))` method returns a new array while keeping only the desired elements of the tab array. so the original array is not modified.

it is called for each elements of the array and it must return `true` if we decide to keep the element. otherwise the element is excluded.

```javascript
tab = ['Element 1', 'Element 2', 'Element 3']

tab = tab.filter(function (element, index) {
	if (index >= 2) return true;
})
// tab = ['Element 3']
```

2. `map(callback)
the `tab.map(callback(element, index))` method is used to return a new array from the elements of initial `tab` array. which must return for each element a new element that will replace the original element.

```javascript
let tab = ['Element 1', 'Element 2', 'Element 3']
tab = tab.map(function (element, index) {
	return element.toUpperCase()
})
```

