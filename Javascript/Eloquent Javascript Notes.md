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

# Function
-  A function definition is a regular binding where the value of the binding is a function.
	```javascript
	const square = function(x) {
	  return x * x;
	};

	console.log(square(12));
	// → 144
	```
	- Functions as values: function and function name (square) are two different things.
-  Scopes
	- global - bindings created outside a function
	- local - bindings created inside a function
	- _lexical scoping_
- Declaration Notation:
	```javascript
	function square(x) {
	  return x * x;
	}
	```
	