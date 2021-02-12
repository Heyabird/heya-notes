# 4. Data Structures: Objects and Arrays
- Properties
	- Almost all JavaScript values have properties. The exceptions are `null` and `undefined`
	- Reading a property that doesn't exist will give you `undefined`.
	- Use `.` or `[]` to access property.
		- When using a dot, the word after the dot is the literal name of the property. When using square brackets, the expression between the brackets is _evaluated_ and converted to a string to get the property name.
- Methods
	- Properties that contain functions are generally called _methods_ of the value they belong to, as in “`toUpperCase` is a method of a string”.

#### Array 
```javascript
	let listOfNums = [4,5,6]
```
- Arrays are just a kind of object specialized for storing sequences of things. If you evaluate `typeof []`, it produces `"object"`.
#### Objects
```javascript
	let day1 = {
	  squirrel: false,
	  events: ["work", "touched tree", "pizza", "running"]
	};
```
- Object.keys - returns property names
```javascript
console.log(Object.keys({x: 0, y: 0, z: 2}));
// → ["x", "y", "z"]
```
- Object.assign
```javascript
 let objectA = {a: 1, b: 2};
Object.assign(objectA, {b: 3, c: 4});
console.log(objectA);
// → {a: 1, b: 3, c: 4}
```

#### Mutability
- Objects are mutable. You _can_ change their properties, causing a single object value to have different content at different times.
- numbers, strings, and Booleans are all _immutable_—it is impossible to change values of those types. You can combine them and derive new values from them, but when you take a specific string value, that value will always remain the same.
- With objects, there is a difference between having two references to the same object and having two different objects that contain the same properties. Consider the following code:
	```javascript
	let object1 = {value: 10};
	let object2 = object1;
	let object3 = {value: 10};

	console.log(object1 == object2);
	// → true
	console.log(object1 == object3);
	// → false
	```
- const - though a `const` binding to an object can itself not be changed and will continue to point at the same object, the _contents_ of that object might change.
	```javascript
	const score = {visitors: 0, home: 0};
	// This is okay
	score.visitors = 1;
	// This isn't allowed
	score = {visitors: 1, home: 1};
	```
- When you compare objects with JavaScript’s `==` operator, it compares by identity: it will produce `true` only if both objects are precisely the same value. Comparing different objects will return `false`, even if they have identical properties.

#### Array Loops
```javascript
for (let i = 0; i < JOURNAL.length; i++) {
  let entry = JOURNAL[i];
  // Do something with entry
}
```
above written in more modern version:
```javascript
for (let entry of JOURNAL) {
  console.log(`${entry.events.length} events.`);
}
```

#### Array Methods
- `includes`
- `push` / `pop` - add / remove elemennt at the end of array
- `unshift` / `shift` - add / remove element at the start of array
- `index of`
	```javascript 
	console.log([1, 2, 3, 2, 1].indexOf(2));
	// → 1
	console.log([1, 2, 3, 2, 1].lastIndexOf(2));
	// → 3
	```
- `slice` - start and end indices and returns an array that has only the elements between them. The start index is inclusive, the end index exclusive.
	```javascript 
	console.log([0, 1, 2, 3, 4].slice(2, 4));
	// → [2, 3]
	console.log([0, 1, 2, 3, 4].slice(2));
	// → [2, 3, 4]
	```
- `concat` - glue arrays together to create a new array, similar to what the `+` operator does for strings.

#### Strings and their built-in properties
```javascript
console.log("coconuts".slice(4, 7));
// → nut
console.log("coconut".indexOf("u"));
// → 5
// a string’s `indexOf` can search for a string containing more than one character, whereas the corresponding array method looks only for a single element.
console.log("  okay \n ".trim());
// → okay
console.log(String(6).padStart(3, "0"));
// → 006
let sentence = "Secretarybirds specialize in stomping";
let words = sentence.split(" ");
console.log(words);
// → ["Secretarybirds", "specialize", "in", "stomping"]
console.log(words.join(". "));
// → Secretarybirds. specialize. in. stomping
console.log("LA".repeat(3));
// → LALALA
let string = "abc";
console.log(string.length);
// → 3
console.log(string[1]);
// → b
```

#### Rest Parameters
It can be useful for a function to accept any number of arguments. For example, `Math.max` computes the maximum of _all_ the arguments it is given.
```javascript
function max(...numbers) {
  let result = -Infinity;
  for (let number of numbers) {
    if (number > result) result = number;
  }
  return result;
}
console.log(max(4, 1, 9, -2));
// → 9
```

You can use a similar three-dot notation to _call_ a function with an array of arguments.
```javascript
let numbers = [5, 1, 7];
console.log(max(...numbers));
// → 7
```
- This “spreads” out the array into the function call, passing its elements as separate arguments

#### Destructuring
```javascript
let {name} = {name: "Faraji", age: 23};
console.log(name);
// → Faraji
```

#### JSON (JavaScript Object Notation )
- A popular serialization format
- In order to conveniently send data to another computer over the network, we can _serialize_ the data. That means it is converted into a flat description.
- JSON looks similar to JavaScript’s way of writing arrays and objects, with a few restrictions. All property names have to be surrounded by double quotes, and only simple data expressions are allowed—no function calls, bindings, or anything that involves actual computation. Comments are not allowed in JSON.
```javascript 
{
  "squirrel": false,
  "events": \["work", "touched tree", "pizza", "running"\]
}
```
`json.stringify` takes a JS value and returns a JSON-encoded string. `json.parse`  takes a JSON-encoded string and returns a JS value.

<hr>

# 5. Higher Order Functions
Abstractions - hide details and give us the ability to talk about problems at a higher (or more abstract) level.

#### Higher Order Functions
 - allow us to abstract over _actions_, not just values.

```javascript
function greaterThan(n) {
  return m => m > n;
}
let greaterThan10 = greaterThan(10);
console.log(greaterThan10(11));
// → true
```

- forEach
```javascript
["A", "B"].forEach(l => console.log(l));
// → A
// → B
```

#### Filtering arrays
```javascript
function filter(array, test) {
  let passed = [];
  for (let element of array) {
    if (test(element)) {
      passed.push(element);
    }
  }
  return passed;
}

console.log(filter(SCRIPTS, script => script.living));
// → [{name: "Adlam", …}, …]
```
```javascript
console.log(SCRIPTS.filter(s => s.direction == "ttb"));
// → [{name: "Mongolian", …}, …]
```

#### Transforming with Map
```javascript
function map(array, transform) {
  let mapped \= \[\];
  for (let element of array) {
    mapped.push(transform(element));
  }
  return mapped;
}
```

#### Summarizing with reduce (a.k.a. fold)
```javascript
function reduce(array, combine, start) {
  let current = start;
  for (let element of array) {
    current = combine(current, element);
  }
  return current;
}
console.log(reduce([1, 2, 3, 4], (a, b) => a + b, 0));
// → 10
```
- standard array method reduce
	- If your array contains at least one element, you are allowed to leave off the `start` argument. The method will take the first element of the array as its start value and start reducing at the second element.
	```javascript
	console.log([1, 2, 3, 4].reduce((a, b) => a + b));
	// → 10
	```

#### Some
- tests whether any element matches a given predicate function
```javascript
	if (script.ranges.some(([from, to]) => {
		  return code >= from && code < to;
		})) {
```
#### FindIndex
- finds the position of the first element that matches a predicate 
```javascript
    let known = counts.findIndex(c => c.name == name);
```

<hr>

# 6. The Secret Life of Objects
Object Oriented Programming
#### Encapsulation
	- separating interface from implementation
- Methods: properties that hold function values
#### Prototype
- = another object that is used as a fallback source of properties
- most objects have a prototype. use `getPrototypeOf()` to check.
- Object.prototype is the root of all prototypes and provides a few methods availablee for objects, such as `toString()`
- Functions derive from Function.prototype, and arrays from Array.prototype.
- You can use `Object.create` to create an object with a specific prototype.
	```javascript
	let protoRabbit = {
	  speak(line) {
		console.log(`The ${this.type} rabbit says '${line}'`);
	  }
	};
	let killerRabbit = Object.create(protoRabbit);
	killerRabbit.type = "killer";
	killerRabbit.speak("SKREEEE!");
	// → The killer rabbit says 'SKREEEE!'
	```
#### Classes
- Prototypes can be used like classes
	- A **class** defines the shape of a type of object—what methods and properties it has. Such an object is called an _instance_ of the class.
		- JS class is a constructor function with a prototype property
	- Constructor - makes sure that the object has all the properties that instances of a certain class should have
		```javascript
		function makeRabbit(type) {
		  let rabbit = Object.create(protoRabbit);
		  rabbit.type = type;
		  return rabbit;
		}
		```
	- If you put the keyword `new` in front of a function call, the function is treated as a constructor.
	- all functions automatically get a property named `prototype`, which by default holds a plain, empty object that derives from `Object.prototype`
	- By convention, the names of constructors are **capitalized** so that they can easily be distinguished from other functions
	- Starting from 2015, we can now use `class` to create constructors:
		```javascript
		class Rabbit {
		  constructor(type) {
			this.type = type;
		  }
		  speak(line) {
			console.log(`The ${this.type} rabbit says '${line}'`);
		  }
		}

		let killerRabbit = new Rabbit("killer");
		let blackRabbit = new Rabbit("black");
		```
	