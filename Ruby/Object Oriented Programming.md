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
-   `initialize` method
	-   runs when a new instance is created
-   `super` keyword
	-   used to directly access the attributes or methods of a superclass; a class with `super` will inherit the attributes or methods of a supeerlcass