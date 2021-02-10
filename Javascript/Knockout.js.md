#### Why use Knockout.js?
- a simple way to create responsive UI with a clean underlying data model.


Headline features:
- **elegant dependency tracking** - automatically updates the right parts of your UI whenever your data model changes.
- **declarative bindings** - a simple and obvious way to connect parts of your UI to your data model. You can construct a complex dynamic UIs easily using arbitrarily nested binding contexts.
- **trivially extensible** - implement custom behaviors as new declarative bindings for easy reuse in just a few lines of code.

#### MVVM and View Models
- **Model**: your app's stored data. Objects and operations in your business domain and is independent of UI. When using KO, you will usually make Ajax calls to some server-side code to read and write this stored model data.
- **View Model**: a pure-code representation of the data and operations on a UI. For ex, if you're implementing a list editor, your view model would be an object holding a list of items, and exposing methods to add and remove items.
- **View**: a visible, interactive UI representing the state of the view model. It displays information from the view model, sends commands to the view model (e.g., when the user clicks buttons), and updates whenver the state of view model changes.
- To create a view model with KO, just declare any JavaScript object. For example,
	```javascript
	var myViewModel = {
	 personName: 'Bob',
	 personAge: 123
	};
	```
	You can then create a very simple _view_ of this view model using a declarative binding. For example, the following markup displays the `personName` value:
	`The name is <span data-bind="text: personName"></span>`

#### ko.applyBindings
- To active Knockout, add `ko.applyBindings(myViewModel);` to a script block.
	- You can either put the script block at the bottom of your HTML document, or you can put it at the top and wrap the contents in a DOM-ready handler such as [jQuery’s `$` function](http://api.jquery.com/jQuery/#jQuery3).
- first param is the view model object you want to use with the declarative bindings it activates
- second param is optional and defines which part of the document you want to search for data-bind attributes
	- For example, `ko.applyBindings(myViewModel, document.getElementById('someElementId'))`. This restricts the activation to the element with ID someElementId and its descendants, which is useful if you want to have multiple view models and associate each with a different region of the page.

#### data-bind
- declaratively associate viewmodel properties with DOM elements


```html
<!-- This is a *view* - HTML markup that defines the appearance of your UI -->  
  
<p>First name: <strong data-bind="text: firstName">todo</strong></p>  
<p>Last name: <strong data-bind="text: lastName">todo</strong></p>
```

#### make data editable (input, value, ko.observable)
- **ko.observable** - property that automatically will issue notifications whenever their value changes
```javascript
var myViewModel = {
 personName: ko.observable('Bob'),
 personAge: ko.observable(123)
};
```
- not all browsers support JS getters and setters, so for compatibility, `ko.observable` objects are actually functions.
- Reading and writing
	- to read the observable's current value, just call the observable with no parameters. `myViewModel.personName()` will return `Bob`.
	- To write a new value to the observable, call the observable and pass the new value as a parameter. For example, calling `myViewModel.personName(Mary)` will change the name value to `Mary`.
	- To write values to multiple observable properties on a model object, you can use *chaining syntax*. For example, `myViewModel.personName('Mary').personAge(50)` will change the name value to `Mary` and the age value to `50`.
```html
<p>First name: <input data-bind="value: firstName" /></p> 
<p>Last name: <input data-bind="value: lastName" /></p>
```

```javascript
// This is a simple *viewmodel* - JavaScript that defines the data and behavior of your UI  
function AppViewModel() {  
 this.firstName = ko.observable("Bert");  
 this.lastName = ko.observable("Bertington");  
}  
  
// Activates knockout.js  
ko.applyBindings(new AppViewModel());
```

#### computing data
- **ko.computable** -  these are _observable_ (i.e., they notify on change) and they are _computed_ based on the values of other observables.
```javascript
this.fullName = ko.computed(function() { 
	return this.firstName() + " " + this.lastName(); 
}, this);
```

#### Adding more behavior
```html
<button data-bind="click: capitalizeLastName">Go caps</button>
```
```javascript
function AppViewModel() { 
	// ... leave firstName, lastName, and fullName unchanged here ... 
	this.capitalizeLastName = function() { 
		var currentVal = this.lastName(); // Read the current value 
		this.lastName(currentVal.toUpperCase()); // Write back a modified value 
	}; 
}
```

#### for each, ko.observableArray
```html 
<tbody data-bind="foreach: seats"> 
	<tr> 
		<td data-bind="text: name"></td> 
		<td data-bind="text: meal().mealName"></td> 
		<td data-bind="text: meal().price"></td> 
	</tr> 
</tbody>
```
```javascript
// Class to represent a row in the seat reservations grid  
function SeatReservation(name, initialMeal) {  
 var self = this;  
 self.name = name;  
 self.meal = ko.observable(initialMeal);  
}  
  
// Overall viewmodel for this screen, along with initial state  
function ReservationsViewModel() {  
 var self = this;  
  
 // Non-editable catalog data - would come from the server  
 self.availableMeals = [  
 { mealName: "Standard (sandwich)", price: 0 },  
 { mealName: "Premium (lobster)", price: 34.95 },  
 { mealName: "Ultimate (whole zebra)", price: 290 }  
 ];   
  
 // Editable data  
 self.seats = ko.observableArray([  
 new SeatReservation("Steve", self.availableMeals[0]),  
 new SeatReservation("Bert", self.availableMeals[0])  
 ]);  
}  
  
ko.applyBindings(new ReservationsViewModel());
```
<hr>

# Bindings

## Controlling Text and Appearance

#### `visible`
```javascript
<div data-bind="visible: shouldShowMessage">
	You will see this message only when "shouldShowMessage" holds a true value.
</div>

<script type="text/javascript">
var viewModel = {
	shouldShowMessage: ko.observable(true) // Message initially visible
};
</script>
```

#### `attr`
- The `attr` binding provides a generic way to set the value of any attribute for the associated DOM element. This is useful, for example, when you need to set the `title` attribute of an element, the `src` of an `img` tag, or the `href` of a link based on values in your view model, with the attribute value being updated automatically whenever the corresponding model property changes.
`<a data-bind="attr: { href: url, title: details }">`

## Control Flow
#### `with` and `using`
- The `with` and `using` bindings create a new [binding context](https://knockoutjs.com/documentation/binding-context.html), so that descendant elements are bound in the context of a specified object.
-   The `with` binding will dynamically add or remove *descendant* elements depending on whether the associated value is `null`/`undefined` or not

## Form Fields
#### `click`
- The `click` binding adds an event handler so that your chosen JavaScript function will be invoked when the associated DOM element is clicked.
#### `submit`
- Instead of using `submit` on the form, you _could_ use `click` on the submit button. However, `submit` has the advantage that it also captures alternative ways to submit the form, such as pressing the _enter_ key while typing into a text box.

#### `value`
- The `value` binding links the associated DOM element’s value with a property on your view model. This is typically useful with form elements such as `<input>`, `<select>` and `<textarea>`.
<hr>

# Binding Context
A _binding context_ is an object that holds data that you can reference from your bindings. While applying bindings, Knockout automatically creates and manages a hierarchy of binding contexts.
- $parent
	- This is the view model object in the parent context, the one immeditely outside the current context. In the root context, this is undefined.
- $parents
- $root
	-   This is the main view model object in the root context, i.e., the topmost parent context. It’s usually the object that was passed to `ko.applyBindings`. It is equivalent to `$parents[$parents.length - 1]`.
- $data
	- This is the view model object in the current context. In the root context, `$data` and `$root` are equivalent. Inside a nested binding context, this parameter will be set to the current data item (e.g., inside a `with: person` binding, `$data` will be set to `person`). `$data` is useful when you want to reference the viewmodel itself, rather than a property on the viewmodel. Example: