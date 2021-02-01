#### data-bind
- declaratively associate viewmodel properties with DOM elements


```html
<!-- This is a *view* - HTML markup that defines the appearance of your UI -->  
  
<p>First name: <strong data-bind="text: firstName">todo</strong></p>  
<p>Last name: <strong data-bind="text: lastName">todo</strong></p>
```

```javascript
// This is a simple *viewmodel* - JavaScript that defines the data and behavior of your UI  
function AppViewModel() {  
 this.firstName = "Bert";  
 this.lastName = "Bertington";  
}  
  
// Activates knockout.js  
ko.applyBindings(new AppViewModel());
```


#### make data editable (input, value, ko.observable)
- **ko.observable** - property that automatically will issue notifications whenever their value changes
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

#### for each
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