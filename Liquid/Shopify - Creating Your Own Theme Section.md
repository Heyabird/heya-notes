src: https://www.shopify.com/partners/blog/how-to-create-your-first-shopify-theme-section

**theme sections** - modular, customizable elements of a page

- #### static section
	- sections are added into liquid templates using the variable `{% section 'header' %}`
	- when you createa new section from the theme file editor, a scaffold is automatically created with schema, css, and JS tags. 
		- within schema tags we would add JSON, which defines how the Theme Editor "reads" our content
	```html
	<div id="textsection">
		<div class="simpletext">
			<h1> {{ section.settings.text-box }} </h1>
			<h3> {{ section.settings.text }} </h3>
		</div>
	</div>

	{% schema %}
	{
		"name": "Text Box",
		"settings": [
			{
				"id": "text-box",
				"type": "text",
				"label": "Heading",
				"default": "Title"
			},
			{
				"id": "text",
				"type": "richtext",
				"label": "Add custom text below",
				"default": "<p>Add your text here</p>"
			}
		]
	}
	{% endschema %}

	{% stylesheet %}
	{% endstylesheet %}

	{% javascript %}
	{% endjavascript %}
	```

- #### dynamic section
	- can be moved into different positions on the homepage by **adding presets**
		- presets define how the section appears on the Theme Editor; they must have a name and a category
	```html
	<div id="section-cta">
		<div class="container">
			<h3> {{ section.settings.text-box }} </h3>
			<a href="{{ section.settings.link }}" class="btn btn--cta">{{ section.settings.linktext }}</a>
		</div>
	</div>

	{% schema %}
	{
		"name": "Call to action",
		"settings": [
			{
				"id": "text-box",
				"type": "text",
				"label": "Heading",
				"default": "Title"
			},
			{
				"id": "link",
				"type": "url",
				"label": "Button link"
			},
			{
				"id": "linktext",
				"type": "text",
				"label": "Button text",
				"default": "Click here"
			}
		],
		"presets": [
			{
				"name": "Call to Action",
				"category": "CTA button"
			}
		]
	}
	{% endschema %}

	{% stylesheet %}
	{% endstylesheet %}

	{% javascript %}
	{% endjavascript %}
	```
	
- Section blocks
	![shopify-sections-chart](https://cdn.shopify.com/s/files/1/0533/2089/files/shopify-sections-chart.jpg?v=1540306266)