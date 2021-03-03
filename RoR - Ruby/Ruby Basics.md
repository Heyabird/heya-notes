- Variables
	```ruby
	myVar = 48 
	```

- Puts vs. Print
	```ruby
	print "Hello"  
	puts "This is written in a new line"  
	```

- Comment
	```ruby
	# I am a single line comment.  

	=begin  
	I am a multi line comment.  
	I can take as many lines as needed.  
	=end
	```
#### Short-Circuit Evaluation
- With `||`, if the expression on the left evaluates to true, it will return `true`. Otherwise, it will check if the expression on the right evaluates to true. If so, the expression returns `true`; otherwise, it will return `false`.
- With `&&`, both the expression on the left and the expression on the right have to evaluate to true in order to return `true`.

#### Conditional Assignment Operator (`||=`)
- assigns a real value to a varaible only when its current value is `false` or `nil`.

#### Control Flow
- if, elsif, end
	```ruby
	print "enter a number: "  
	num = gets.chomp  
	num = num.to_i;  

	if num == 5  
	 print "number is 5"  
	elsif num == 10  
	 print "number is 10"  
	else  
	 print "number is something other than 5, 10, or 11"  
	end
	```
- unless
	```ruby
	print "Enter a number"  
	number = gets.to_i  
	unless number > 10  
	 puts "number is less than 10."  
	end
	```
- case
	```ruby
	case tv_show  
	 when "Archer"  
	 puts "I don't like the voice of Archer."  
	 when "Bob's Burgers"  
	 puts "I love the voice of Bob Belcher."  
	 else  
	 puts "I don't know who voices this cartoon."  
	end
	```
- Ternary Operator
```ruby
	puts tacos_eaten >= 5 ? "Sir, you've had enough!" : "Keep eating tacos!"
```

#### Looping
- `next`
	```ruby
	for i in 1..4  
	 next if i % 2 == 0  
	 puts i  
	end  

	# Output:  
	# 1  
	# 3   
	```
- `while`
- `times`
	```ruby
	3.times { puts ""Codecademy"" }  

	# Output:  
	# Codecademy  
	# Codecademy  
	# Codecademy  
	```
- `range`
- `loop`
- `until`
- `for`

#### Array
```ruby
	numbers = [1,2]
```

#### << (Concactenation Operator)
- push method alternative
	```ruby
	array = [1, 2, 3]  
	array << 4  
	print array  
	#Output => [1, 2, 3, 4]
	```

#### Hash 
- keys & values
	```ruby  
	profile = {  
	 "name" => "Magnus",  
	 "profession" => "chess player",  
	 "grandmaster?" => true  
	}
	```
- Accessing value (bracket notation)
	- Ruby doesn't have dot notation
	```ruby
	puts profile["name"] # => Magnus
	```
- creating a Hash
```ruby
	#Creating a hash through literal notation:  
	lunch = {  
	 "protein" => "chicken",  
	 "organic?" => true  
	}  

	#Creating a hash through Hash.new  
	lunch = Hash.new  
	puts lunch # => {}
```
- adding a pair (Bracket Notation)
```ruby
	teammates = Hash.new  
	teammates["forward"] = "Messi"
```

#### Symbols
- immutable names primarily used as hash keys or for referencing method names
	```ruby
	my_bologna = {  
		:first_name => "Oscar",  
		:second_name => "Meyer"
	}  
	```
- key symbols and their values can also be defined with colon
	```ruby
	my_progress = {
		first_name: "Oscar",
		last_name: "Meyer"
		}
	```

#### .Each
- Ruby method; used to iterate over arrays and hashes
```ruby
colors = ["red", "blue"]

colors.each { |color| puts color }
#Output  
#red  
#blue

polygons = {
	"pentagon" => 5,
	"hexagon" => 6, 
	"nonagon" => 9
}

polygons.each do |shape, sides|
	puts "A #{shape} has #{sides} sides."
end
#Output
# A pentagon has 5 sides.
# A hexagon has 6 sides.
# A nonagon has 9 sides.
```

#### .Select
- Ruby method; used to grab specific values from a hash that meet the criteria
```ruby
	olympic_trials.select { |name, time| time < 10.05}
```

#### .each_key, .each_value
```ruby
eren_jaeger.each_key { |key| puts key }
eren_jaeger.each_value { |value| puts value }
```

#### Sorting
- Combined Comparison Operator
	```ruby
	puts "keanu" <=> "adrianna" # 1
	puts 1 <=> 2 # -1  
	puts 3 <=> 3 # 0
	```
- `.sort`
	```ruby
	my_array = [3, 4, 8, 7, 1, 6, 5, 9, 2]  
	my_array.sort!  
	#Attaching an ! to the end of .sort or any other Ruby method modifies the original array.  
	print my_array  
	# => [1, 2, 3, 4, 5, 6, 7, 8, 9]  
	#If you didn't use !, print my_array returns the original array.
	```
#### splat (`*`)
- indicates that a param can have an unknown # of arguments
	```ruby
	def extra_curriculars(*clubs)  
	 clubs.each { |club| puts "After school, I'm involved with #{club}" }  
	end  

	extra_curriculars("chess club", "gymnastics", "anime club", "library services")
	```

<hr>
source: Codecademy Ruby Cheatsheets