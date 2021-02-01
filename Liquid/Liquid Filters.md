#### Defining Custom Filters
- Basically, a filter is just a method that takes at least one parameter and returns a processed string.
```ruby
module MyFilters 
	def headline(input) 
		"<h1>#{input}</h1>" 
	end 
end
```
- In order for the Rails application to find your custom filters, you need to store them in the directory `/app/filters`. For the example above, the path would be `/app/filters/my_filters.rb`.
- To use the above example in a template you would type the following:
```ruby
{{ "Some Interesting Headline" | headline }}
```
- This would produce:
```html 
<h1>Some Interesting Headline</h1>
```

#### Existing Filters
- abs - returns the absolute value of number (or number represented in a string)
	```liquid
	{{ -17 | abs }}
	=> 17
	```
- append / prepend
	```liquid
	{% assign filename = "/index.html" %}
	{{ "website.com" | append: filename }}
	=>
	website.com/index.html
	```
- at_least, at_most
- capitalize / upcase / downcase
	```liquid
	{{ "title" | capitalize }}
	```
- ceil / floor / round
	```liquid
	{{ 1.2 | floor }}
	=> 1
	```
- compact - removes any `nil` from array
- concat - concactenates multiple arrays
- default - show default value if value on left is empty, false, or nil
- divided_by / minus / modulo / plus / times
- first / last
- join - combines items in array to a string using the argument as a separator
	```liquid
	{% assign beatles = "John, Paul, George, Ringo" | split: ", " %}
	{{ beatles | join: " and " }}
	```
- lstrip - removes all whitespaces from left side of string except spaces in between words / rstrip / strip (left and right)
- map - creates an array of values by extracting the values of a named property from another object.
	```liquid
	{% assign all_categories = site.pages | map: "category" %}

	{% for item in all_categories %}
	- {{ item }}
	{% endfor %}
	```
	```
	Output:
	- business
	- celebrities
	- lifestyle
	- sports
	- technology
	```
- remove / remove_first
- replace / replace_first
	```liquid
	{{ "Take my protein pills and put my helmet on" | replace: "my", "your" }}
	```
- reverse
	```liquid
	{% assign my_array = "apples, oranges, peaches, plums" | split: ", " %}
	{{ my_array | reverse | join: ", " }}
	```
- size - returns the number of characters in a string or the number of items in an array.
- slice
	```liquid
	{{ "Liquid" | slice: 2 }}
	=> q

	{{ "Liquid" | slice: 2, 5 }}
	=> quid

	{{ "Liquid" | slice: -3, 2 }}
	=> ui
	```
- sort / sort-natural (case-insensitive)
	```liquid
	{% assign my_array = "zebra, octopus, giraffe, Sally Snake" | split: ", " %}

	{{ my_array | sort | join: ", " }}
	```
- split - divides a string into an array using the argument as a separator
	```liquid
	{% assign beatles = "John, Paul, George, Ringo" | split: ", " %}

	{% for member in beatles %}
	  {{ member }}
	{% endfor %}
	```
- strip_html - removes any html tags from a string
- truncate / truncatewords
- uniq - removes any duplicate elements in an array
	```liquid
	{% assign my_array = "ants, bugs, bees, bugs, ants" | split: ", " %}
	{{ my_array | uniq | join: ", " }}
	=> 
	ants, bugs, bees
	```
- url_encode / url_decode
- where - creates an array including only the objects with a given property value, or any truthy value by default.
	- example: using `where`, you can create an array containing only the products that have a `"type"` of `"kitchen"`.
	```liquid
	All products:
	{% for product in products %}
	- {{ product.title }}
	{% endfor %}

	{% assign kitchen_products = products | where: "type", "kitchen" %}

	Kitchen products:
	{% for product in kitchen_products %}
	- {{ product.title }}
	{% endfor %}
	```