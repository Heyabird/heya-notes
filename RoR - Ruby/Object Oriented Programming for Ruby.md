#### Class
```ruby
	class Child  
	 @@children = 0  
	 def initialize(name, birth_year)  
		 @name = name  
		 @birth_year = birth_year  
		 @@children +=1  
	 end  

	 def self.children_added  
	 return @@children  
	 end  

	end  

	naomi = Child.new("Naomi", 2006)  
	bertha = Child.new("Bertha", 2008)  

	puts Child.children_added # => 2
```

- Variables
	- constants (`MY_CONTANT = 9`) - available throughout the app
	- global variable (`$var`) - available throughout the app
	- class variable (`@@var`) - accessed by class and class instances
	- instance variable (`@var`) - available throughout the current instance of this class
	- local variable (`var`) - must be passed around to cross scope boundaries
- `.new` method
	- calling it creates a new **class instance**. Arguments to the class' `initialize` method can be passed in to the `.new` call.
	```ruby
		naomi = Child.new("Naomi", 2006)  
	```
-   `initialize` method
	-   runs when a new instance is created
#### Inheritance
-   `super` keyword
	-   used to directly access the attributes or methods of a superclass; a class with `super` will inherit the attributes or methods of a superclass
	```ruby
	class Trip
		def initialize(duration, price)
			@duration = duration
			@price = price
		end
	end
	
	class Cruise < Trip
		def initialize(duration, pricee)
			super
		end
	end
	```

#### attr_reader, attr_writer, attr_accessor
- `attr_reader` makes a variable readable, and  `attr_writer` makes a variable writable
	```ruby
	class Student
		attr_reader :name
		attr_writer :name
		def initialize(name)
			@name = name
		end
	end
	
	top_student = Student.new("Jyothi")
	puts top_student.name #=> Jyothi (attr_reader)
	top_student.name = "Anika" # (attr_writer)
	puts top_student.name #=> Anika 
	```
- `attr_accessor`
	- makes a variable both readable and writable
	```ruby
	class CollegeStudent  
		attr_reader :dorm  
		attr_accessor :major
	 ```
#### Module
- contains a set of methods, constants, or classes which can be accessed with the `.` operator similarly to classes. Unlike classes, it's impossible to create instances of a Ruby module.
```ruby
	module MyPizza
		FAVE_TOPPING = "Buffalo Chicken"
	end
```

- Namespace = a module that contains a group of related objects.
	- example: Math module (`::` is a scope resolution operator)
		```ruby
		puts Math::PI #=> 3.141592653589793
		```

-  `Require` keyword is used to fetch a certain module which isn't yet presented in the interpreter.
	```ruby
	require 'date'
	
	puts Date.today #=> 2021-02-19
	```
	
<hr>

#### [OOP Concepts](https://launchschool.com/books/oo_ruby/read/the_object_model)

1) **Abstraction**  - making the viewed interface as simple as possible
	- Example: [[Active Record]] being an abstraction of SQL
2) **Encapsulation** - hiding pieces of functionality and making it unavailable to the rest of the code base.
3) **Polymorphism** - the ability for different types of data to respond to a common interface.
	- **Mixin** - Another way (other than inheritance) to apply polymorphic structure to Ruby programs is to use a `Module`. Modules are similar to classes in that they contain shared behavior. However, you cannot create an object with a module. A module must be mixed in with a class using the `include` method invocation. This is called a **mixin**. After mixing in a module, the behaviors declared in that module are available to the class and its objects.
4) **Inheritance** - where a class inherits the behaviors of another class, referred to as the **superclass**. This gives Ruby programmers the power to define basic classes with large reusability and smaller **subclasses** for more fine-grained, detailed behaviors.
