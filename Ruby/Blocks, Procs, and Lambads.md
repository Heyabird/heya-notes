#### Block
- Ruby blocks are little anonymous functions that can be passed into methods.
- enclosed in a `do` / `end` statement or between curly braces `{}`.
	```ruby
	2.times do  
	 puts "I'm a code block!"  
	end
	
	3.times { puts "So am I"}
	```
- A Ruby block is useful because it allows you to save a bit of logic (code) & use it later.

#### Block Parameter
- In Ruby, a method can take a *block* as a parameter
	```ruby
	# The block, {|i| puts i}, is passed the current array item each time it is evaluated. This block prints the item.  
	[1, 2, 3, 4, 5].each { |i| puts i }
	```

#### Ruby Proc
- In Ruby, a _proc_ is an instance of the Proc class and is similar to a block. As opposed to a block, a _proc_ is a Ruby object which can be stored in a variable and therefore reused many times throughout a program.

#### Ruby Lambda
- In Ruby, a _lambda_ is a special _proc_ object. Unlike a _proc_, a _lambda_ requires a specific number of arguments passed to it, and it `return`s to its calling method rather than returning immediately.
- Two ways to write a lambda:
	```ruby
	say_something = -> { puts "this is a lambda"}
	say_something_else = lambda { puts "this is a lambda"}
	```

#### Proc vs. lambda
-   Lambdas are defined with `-> {}` and procs with `Proc.new {}`.
-   Procs return from the current method, while lambdas return from the lambda itself.
-   Procs don’t care about the correct number of arguments, while lambdas will raise an exception.
	 ```ruby
		t = Proc.new { |x,y| puts "I don't care about arguments!" }
		t.call
		# "I don't care about arguments!"
	```

#### `.call` Method
- In Ruby, a proc and a lambda can be called directly using the `.call` method.
```ruby
proc_test = Proc.new { puts "I am the proc method!" }  
lambda_test = lambda { puts "I am the lambda method!"}  
  
proc_test.call # => I am the proc method!  
lambda_test.call # => I am the lambda method!
```

#### Closures
- Ruby procs & lambdas also have another special attribute. When you create a Ruby proc, it captures the current execution scope with it. This concept, which is sometimes called [closure](https://en.wikipedia.org/wiki/Closure_(computer_programming)), means that a `proc` will carry with it values like local variables and methods from the context where it was defined.
```ruby
  def call_proc(my_proc)
  count = 500
  my_proc.call
  end

  count = 1
  my_proc = Proc.new { puts count }

  p call_proc(my_proc) # What does this print?
```
- It would seem like `500` is the most logical conclusion, but because of the ‘closure’ effect this will print `1`.
- This happens because the proc is using the value of `count` from the place where the proc was defined, and that’s outside of the method definition.

<hr>

source: 
- [Codecademy Ruby Cheatsheets](https://www.codecademy.com/learn/learn-ruby/modules/learn-ruby-introduction-to-ruby-u/cheatsheet)
- [Ruby Guides](https://www.rubyguides.com/2016/02/ruby-procs-and-lambdas/#:~:text=Procs%20return%20from%20the%20current,lambdas%20will%20raise%20an%20exception.)