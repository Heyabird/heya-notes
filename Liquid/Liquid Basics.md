# Liquid Basics
- like any template language, creates a bridge between an HTML file and a data store (Shopify).
- you can ask Shopify to populate a variable you create with all the products in a particular collection. you, as the designer, don't need to know anything about the store data itself
- ``{{ }}`` denotes output, `{% %}` denotes logic.
#### Objects & Variable Names
```liquid
{{ page.title }}
```
^(object.property)

#### [[Liquid Tags]]
**Tags** create the logic and control flow for templates
```liquid
{% if user %}
  Hello {{ user.name }}!
{% endif %}
```

#### [[Liquid Filters]]
**Filters** change the output of a Liquid object. They are used within an output and are separated by a `|`.
```liquid
{{ "/my/fancy/url" | append: ".html" }}
```
 ```
/my/fancy/url.html
```
```liquid
{{ "adam!" | capitalize | prepend: "Hello " }}
```
```
Hello Adam!
```

#### Operators
- basic (==, !=, >, < >=, <=, or, and)
- contains - checks for the presence of a substring inside a string or a string inside an array of strings
- order of operations happen right to left.

#### Truthy and falsy
- all values in Liquid are truthy except `false` and `nil` (even empty strings are truthy)

#### Types
You can initialize liquid variables with the `assign` or `capture` tags.
-  [String](https://shopify.github.io/liquid/basics/types/#string)
	```liquid
	{% assign my_string = "Hello World!" %}
	```
-  [Number](https://shopify.github.io/liquid/basics/types/#number)
-  [Boolean](https://shopify.github.io/liquid/basics/types/#boolean)
-  [Nil](https://shopify.github.io/liquid/basics/types/#nil)
-  [Array](https://shopify.github.io/liquid/basics/types/#array)
	- you can't initialize arrays in liquid, unless you assign a string and then apply `split`
	- accessing items in arrays:
		```liquid
		{% for user in site.users %}
			{{user}}
		{% endfor %}
		```
		```liquid
		{{ site.users[0] }}
		{{ site.users[1] }}
		{{ site.users[3] }}
		```
		
#### Whitespace control
In Liquid, you can include a hyphen in your tag syntax `{{-`, `-}}`, `{%-`, and `-%}` to strip whitespace from the left or right side of a rendered tag.
```liquid
{%- assign my_variable = "tomato" -%}
{{ my_variable }}
```
