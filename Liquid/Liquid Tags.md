# Liquid Tags
#### Variable tags
- **assign** - creates a new variable
	```liquid
	{% assign foo = "bar" %}
	{{ foo }}
	```
- **capture** - captures the string inside of the opening and closing tags and assigns it to a variable
	```liquid
	{% capture my_variable %}I am being captured.{% endcapture %}
	{{ my_variable }}
	```
	```liquid
	{% assign favorite_food = "pizza" %}
	{% assign age = 35 %}

	{% capture about_me %}
	I am {{ age }} and my favorite food is {{ favorite_food }}.
	{% endcapture %}

	{{ about_me }}
	```
- **increment** - creates a new number variable, and increases its value by one every time it is called. The initial value is 0.
	- Variables created through the `increment` tag are independent from variables created through `assign` or `capture`.
	```liquid
	{% assign var = 10 %}
	{% increment var %}
	{% increment var %}
	{% increment var %}
	{{ var }}
	```
	=> 0, 1, 2, 10
- **decrement** - creates a new number variable, and decreases its value by one every time it is called. The initial value is -1.


####  Control flow
- **IF/ELSIF/ELSE**
```liquid
{% if customer.name == "kevin" %}
  Hey Kevin!
{% elsif customer.name == "anonymous" %}
  Hey Anonymous!
{% else %}
  Hi Stranger!
{% endif %}
```
- **UNLESS** (opposite of if)
```liquid
{% unless product.title == "Awesome Shoes" %}
  These shoes are not awesome.
{% endunless %}
```
- **CASE/WHEN**
```liquid
{% assign handle = "cake" %}
{% case handle %}
  {% when "cake" %}
     This is a cake
  {% when "cookie" %}
     This is a cookie
  {% else %}
     This is not a cake nor a cookie
{% endcase %}
```
- **FOR/ELSE** (else specifies a fallback case for a `for` loop which will run if the loop has zero length)
```liquid
{% for product in collection.products %}
  {{ product.title }}
{% else %}
  The collection is empty.
{% endfor %}
```
- **BREAK**
```liquid
{% for i in (1..5) %}
  {% if i == 4 %}
    {% break %}
  {% else %}
    {{ i }}
  {% endif %}
{% endfor %}
```
- **CONTINUE** - causes the loop to skip the current iteration when it encounters the `continue` tag.
```liquid
{% for i in (1..5) %}
  {% if i == 4 %}
    {% continue %}
  {% else %}
    {{ i }}
  {% endif %}
{% endfor %}
```
- **FOR (parameters) **
	- limit - limits loop for specified number of iterations
		```liquid
		{% for item in array limit:2 %}
		  {{ item }}
		{% endfor %}
		```
	- offset - begins the loop at specified index `offset:2`
	- range `{% for i in (3..5) %}`
	- reversed - reverses order of loop `{% for item in array reversed %}`
	- cycle - loops through a group of strings and prints them in the order that they were passed as arguments. `{% cycle "one", "two", "three" %}` or `{% cycle "second": "one", "two", "three" %}`
	- tablerow - generates HTML table
#### Comment blocks
```
Anything you put between {% comment %} and {% endcomment %} tags
is turned into a comment.
```
#### Raw
- temporarily disables tag processing
```liquid
{% raw %}
  In Handlebars, {{ this }} will be HTML-escaped, but
  {{{ that }}} will not.
{% endraw %}
```