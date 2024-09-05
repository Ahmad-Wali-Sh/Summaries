# Big-O Notation

`Summary by Ahmad Wali Sharify`

## Space and Time Complexity

it is a measure of costing an Algorithm takes. by algebraic terms.

	- in Big-notation: n represent the number of inputs.
	"What will happen as n approaches infinity?"
	it tell how efficient your algorithm is.  
We Care about the Trend/Kind of function, not the actual concrete time data
 - we say this algorithm has O of 1 complexity 

![Alt text](https://t36964073.p.clickup-attachments.com/t36964073/4d5dac56-0761-4862-9881-af14aa1c9ac4/Capture.PNG)


<br>

## O(1): Constanst Time

Does not Change with Respect to input space. (constant time)
	
Ex: accessing an item in the array by its index.

or:

```javascript 
function sumUp(n) {
  return (n/2) * (n + 1) // 1
}
```

## O(n): Linear Time

linear time and applies to algorithms that must do n operations in the worst case scenario.

Ex: 
```javascript
function exampleLinear(n) {
        for (var i = 0; i < n; i++){ // 1
         console.log(i)              // n
         }
}
```

<br>

# Detecting Algorithm Big O

how to detect an algorithm Big O?

1. Define the function, T = 1, T = 1 + 1 + 1 + n or...
2. Find the fastest growing term, n
3. Remove the coefficient, T = n 