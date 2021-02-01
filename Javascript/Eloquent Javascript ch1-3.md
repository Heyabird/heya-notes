# 1. Values
> To be able to work with such quantities of bits without getting lost, we must separate them into chunks that represent pieces of information. In a JavaScript environment, those chunks are called _values_.

- **Data types** - every value has a type, which determines its role.
	- Primitive:
		- Number - numerical value. uses 64 bits.
			- +Infinity, -Infinity
			- NaN - only value that is not equal to itself
		- String - in between single quotes, double quotes, or backtick quotes (template liteerals)
			- + allows concactenation
			- template literals can embed other values `half of 100 is ${100 / 2}` 
		- Boolean 
		- undefined - no meaningful value
	- Structural:
		- Object
		- Function
	- Structural Root primitive:
		- null 
```javascript
console.log(8 * null)
// → 0
console.log("5" - 1)
// → 4
console.log("5" + 1)
// → 51
console.log("five" * 2)
// → NaN
console.log(false == 0)
// → true
```

- _type coercion_ = when an operator is applied to the “wrong” type of value, JavaScript will quietly convert that value to the type it needs

Operators
- Arithmetic (+, -, *, /, %, ++, --) 
- Assignment (=, +=, -=, *=, /=, %=, **=)
- Comparison (==, ===, !=, !==, >, <, >=, <=, ?)
- Logical (||, &&, !)
	- || will return left value if true, if not return right value
	- && will return left value if false, if not return right value 
	-  _short-circuit evaluation_ = the part to their right is evaluated only when necessary
- Type (typeof, instanceof)

<hr>

# 2. Program Structure 
- Expression - a fragment of code that produces a value.
- Statement - full javascript "sentence", ended by a ';'.
- Bindings/variables - a way for programs to hold values
	```javascript
	let one = 1, two = 2;
	const three = 3;
	console.log(one + two + three);
	// → 6
	```
- Environment - a collection of bindings and values that exist at a given time
- Functions - a piece of program wrapped in a value. Such values can be _applied_ in order to run the wrapped program.
	```javascript
	console.log("test");
	```
- Control flow
	- straight line
	- conditional execution
		- if
		```javascript
		if (num < 10) {
			console.log("Small");
		} else if (num < 100) {
		  console.log("Medium");
		} else {
		  console.log("Large");
		}
		```
		- switch (code runs until it hits break)
		```javascript
		switch (prompt("What is the weather like?")) {
		  case "rainy":
			console.log("Remember to bring an umbrella.");
			break;
		  case "sunny":
			console.log("Dress lightly.");
		  case "cloudy":
			console.log("Go outside.");
			break;
		  default:
			console.log("Unknown weather type!");
			break;
		}
		```
	-  loop
		- while & do loops
		```javascript
		//while loop
		let number = 0;
		while (number <= 12) { 
			console.log(number);
			number = number + 2;
		}
		
		//do loop - same as while except always executes its body at least once 
		let yourName;
		do {
		    yourName = prompt("Who are you?");
		} while (!yourName);
			console.log(yourName);
		```
		- for loops
		 ```javascript
		for (i=0; i<arr.length; i++) {
			console.log(i);
		}
		```
		- break
		``` javascript
		for (let current = 20; ; current = current + 1) {
			if (current % 7 == 0) {
				console.log(current);
				break;
			  }
			}
			// → 21
		```
- Comments (//, /* */)

<hr>

# 3. Functions
#### Scopes
- global - bindings created outside a function
- local - bindings created inside a function
- _lexical scoping_

#### 1. Function definition/expression:
-  = a regular binding where the value of the binding is a function.
	```javascript
	const square = function(x) {
	  return x * x;
	};

	console.log(square(12));
	// → 144
	```
	- Functions as values: function and function name (square) are two different things.

#### 2. Function declaration:

```javascript
function square(x) {
  return x * x;
}
```
- Function declarations are not part of the regular top-to-bottom flow of control. They are conceptually moved to the top of their scope and can be used by all the code in that scope.
```javascript
console.log("The future says:", future());
function future() {
  return "You'll never have flying cars";
}
```
			- The preceding code works, even though the function is defined below the code that uses it.
#### 3. Arrow Functions

```javascript
const power = (base, exponent) => {
  let result = 1;
  for (let count = 0; count < exponent; count++) {
	result *= base;
  }
  return result;
};
```
- When there is only one parameter name, you can omit the parentheses around the parameter list. If the body is a single expression, rather than a block in braces, that expression will be returned from the function. So, these two definitions of `square` do the same thing:
```javascript
const square1 = (x) => { return x * x; };
const square2 = x => x * x;
```
- Arrow functions were added in 2015, mostly to make it possible to write small function expressions in a less verbose way.
- Differences between arrow and regular functions: https://dmitripavlutin.com/differences-between-arrow-and-regular-functions/

#### Call Stack 
- Every time a function is called, the current context is stored on top of this stack.  When a function returns, it removes the top context from the stack and uses that context to continue execution.
- Storing this stack requires space in the computer’s memory.

#### Optional Arguments
```javascript
function square(x) { return x * x; }
console.log(square(4, true, "hedgehog"));
// → 16
```
- Arguments in JS: If you pass too many, the extra ones are ignored. If you pass too few, the missing parameters get assigned the value `undefined`.
```javascript
function minus(a, b) {
  if (b === undefined) return -a;
  else return a - b;
}

console.log(minus(10));
// → -10
console.log(minus(10, 5));
// → 5
```
- Default argument value
```javascript
function power(base, exponent = 2) {
...
```

#### Closure
- = a function that references bindings from local scopes around it
```javascript
function multiplier(factor) {
  return number => number * factor;
}

let twice = multiplier(2);
console.log(twice(5));
// → 10
```
- In the example, `multiplier` is called and creates an environment in which its `factor` parameter is bound to 2. The function value it returns, which is stored in `twice`, remembers this environment. So when that is called, it multiplies its argument by 2.

#### Recursion
- = a function calling itself
```javascript
function power(base, exponent) {
  if (exponent == 0) {
    return 1;
  } else {
    return base * power(base, exponent - 1);
  }
}

console.log(power(2, 3));
// → 8
```

#### Growing Functions
