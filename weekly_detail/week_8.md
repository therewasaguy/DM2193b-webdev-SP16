# Monday 3/28

## More Events

To ensure that DOM has loaded before you start accessing elements, it is common to wrap code in an event handler.

The `document` has a `"DOMContentLoaded"` event that fires when DOM is parsed. This is better than the `window` `"load"` event, which also waits for CSS and images that we don't usually need to register our event handlers.

```
document.addEventListener('DOMContentLoaded', doStuff);

function doStuff() {
  // local variable
  var elt = document.getElementById('my-button');

  elt.addEventListener('click', function() {
    alert('you clicked me');
  });
}
```

#### Event Bubbling
Events bubble, but you can call the ```stopPropagation``` method to catch them.

Demo:
https://thimbleprojects.org/jasonsigal/47774/


## JavaScript Objects

##### Objects { }
Objects contain values with names. This is known as a "key : value" pair. Also known as **JSON (JavaScript Object Notation)**
```
var restaurantData = {
  name: "Morimoto",
  city: "New York",
  cuisine: "Japanese",
  thumbsUp: 4,
  thumbsDown: 1
}

console.log("the name of the restaurant is " + restaurantData.name + " and it is located in " + restaurantData.city);

// returns:
// the name of the restaurant is Morimoto and it is located in New York
```

## Sublime Text Features
* **[Snippets](http://docs.sublimetext.info/en/latest/extensibility/snippets.html)**
  * Reusable code snippets that you can trigger with a `tabTrigger`.
  * Snippets have an optional `scope`, for example you might have a scope for javascript files (`source.js`) and html files (`text.html`). [Here is a list of the available scopes](https://gist.github.com/iambibhas/4705378).


## jQuery

jQuery is a JavaScript library: A file with a ".js" extension that we can include in a script tag in our page.

We can link to it from [this CDN](https://code.jquery.com/) (Content Distribution Network)
`<script src="https://code.jquery.com/jquery-2.2.2.js"></script>`

or download it and include it in our project with a relative path:
`<script src="libs/jquery.js"></script>`

John Resig began work on jQuery in 2005. He wanted a more efficient way to **query** the DOM (using CSS selectors) and bind functions to DOM events. This is the core idea of jQuery.

#### jQuery syntax

** Basic syntax is: $(selector).action()**

* A $ sign to define/access jQuery
* A (selector) to "query (or find)" HTML elements
* A jQuery action() to be performed on the element(s)

*via [w3 schools](http://www.w3schools.com/jquery/jquery_syntax.asp)*

#### jQuery vs. pure JS queries

```
// pure JS
document.addEventListener('DOMContentLoaded', doStuff);

// jQuery
$(document).ready(doStuff);

// JS
document.getElementById('my-button');

// jQuery
$('#my-button');

// JS
document.getElementsByClassName('.hidden'); 

// jQuery
$('.hidden');

```

##### this
`$(this)` returns the current HTML element. In jQuery it is typically used in the context of an event handler (see below for some examples).


#### jQuery Events
Events have special functions in jQuery.

Some examples:
```
$("selector").click();
$("selector").dblclick();
$("selector").mouseenter;
$("selector").mouseleave();
$("selector").mousedown();
$("selector").mouseup();
$("selector").hover();
$("selector").focus();
$("selector").blur();
```

You can also use `.on('event')` or `.on(object)` (see [.on in jQuery documentation](http://api.jquery.com/on/)). Example using an object:

```
$("p").on({
    mouseenter: function(){
        $(this).css("background-color", "lightgray");
    }, 
    mouseleave: function(){
        $(this).css("background-color", "lightblue");
    }, 
    click: function(){
        $(this).css("background-color", "yellow");
    } 
});
```

More on jQuery Events: http://www.w3schools.com/jquery/jquery_events.asp


#### jQuery Effects
jQuery lets you animate using JS. It is not the fastest JS animation library—CSS transitions will typically be faster and are more trendy right now. But here's an example:

Toggle visibility
```
$(selector).hide(speed,callback);
$(selector).show(speed,callback);
$(selector).toggle(speed,callback);
```

Read more about jQuery Effects
http://www.w3schools.com/jquery/jquery_hide_show.asp



#### HW:
Do [jQuery w3 Schools tutorial](http://www.w3schools.com/jquery/) and browse the documentation at https://api.jquery.com/

Think about how to build off of our example from class to create a search filter.


---
# Wednesday 3/30

## GitHub checkin

## Sublime Text: Package Control
  * This is an extension that makes it easy to search and install Sublime Text Packages. Packages include snippets and can start servers.
  * Install Package Control here: https://packagecontrol.io/installation
  * Then access it via Tools > Command Palette, and start typing Package Control.
  * Let's install some packages:
    * **[HTML/CSS/JS Prettify](https://packagecontrol.io/packages/HTML-CSS-JS%20Prettify)** - Make you code look nicer
    * **[HTML5 Snippets](https://packagecontrol.io/packages/HTML5)** - Syntax highlighting + Snippets
    * **[jQuery Snippets](https://packagecontrol.io/packages/jQuery)** - Syntax highlighting + Snippets
    * Browse more [here](https://packagecontrol.io/browse/popular)

## Objects
Preview: Fetching JSON data from API's like [metaweather](https://www.metaweather.com/api/location/44418/) and [FourSquare](http://api.foursquare.com)

## Objects: In Class Exercise
1. Create an HTML document with the following JS in a `<script>` tag:
```
var flavors = [
	{
		"name": "Rocky Road",
		"id": "rocky_road",
		"ingredients": ["vanilla ice cream", "chocolate chips", "marshmallows", "almonds"],
		"allergies": ["dairy", "nuts"]
	},

	{
		"name": "Vanilla",
		"id": "vanilla",
		"ingredients": ["milk", "cream", "sugar", "vanilla extract"],
		"allergies": ["dairy"]
	},

	{
		"name": "Strawberry Sorbet",
		"id": "strawberry_sorbet",
		"ingredients": ["water", "strawberries", "lemon juice", "sugar", "vanilla extract"],
		"allergies": ["strawberries"]
	},

	{
		"name": "Chocolate",
		"id": "chocolate",
		"ingredients": ["milk", "cocoa", "egg yolks", "sugar", "vanilla extract", "semisweet chocolate"],
		"allergies": ["egg", "chocolate", "dairy"]
	}
];
```
2. Using JavaScript, display the following to the page:
  - All of Rocky Road's ingredients, separated by a "|"
  - The only allergy in Strawberry Sorbet 
  - The first ingredient in Strawberry Sorbet
  - The number of ingredients in Chocolate
  - The name of every flavor (for loop and array.length are needed)

## jQuery (cont'd)
Revisit search filter example (full code [here](https://www.dropbox.com/sh/1nromfghwgfh6hf/AAAXgVFDYrhGWsVtlGuR1RgLa?dl=0))

```
// event listener
$('#search').keyup( filterSearch );

// event handler
function filterSearch(e) {
    // get value of the DOM element that triggered this event
	var searchValue = $(this).val();

    // if there is a value...
	if (searchValue) {
		// hide element (in 200 ms) if its .allergy contains the searchValue
		$('.allergy:contains(' + searchValue + ')').parent().hide(200);

		// if it does not contain the search value, show the element (in 200 ms)
		$('.allergy:not( :contains(' + searchValue + ') )').parent().show(200);
	}
    
    else {
		// if there is no searchValue, show all elements with flavor class
		$('.flavor').show(200);
	}

}
```

## Intro to Frameworks:
* Bootstrap
* Foundation

#### [Slides](https://docs.google.com/presentation/d/194ZbRxecL0ep4oBtV3i4Mr4W2QwAhJiasAfJAsgtIDY/edit?usp=sharing)

##### Grid System, Media Queries / Breakpoints

##### Components


## HW:
* Read:
  * [Bootstrap vs Foundation comparison](http://www.sitepoint.com/grid-system-comparison-bootstrap-vs-foundation/)
* Do:
  * Bootstrap and/or Foundation tutorials on lynda.com, w3 Schools
* Make:
  * A single web page that uses jQuery and either Bootstrap or Foundation. It could be a preview of your final project, a revision of your calculator, or a fun little side project. Post to Slack #hw channel with #wk8b and include a link to the site + github.
* Prepare:
  * Final Project Proposals (due Monday April 11th):
    * Project Plan
    * Wireframe
    * Site Map
    * Style Guide

## Reminders
* Class meets on Friday 4/8 next week, 2:30-4:20 in **Room 807**
* Upcoming Events at IDM:
  * [Different Games Conference](https://www.eventbrite.com/e/different-games-conference-2016-tickets-23115571296)
  * Meet & Greet Portfolio (Juniors/Seniors only) - May 3rd, but register [here](https://docs.google.com/forms/d/1lxLf3wdHyJ9uYBoBeDC3dd0TB_w96KxG4n0I8yWRC_Q/viewform?c=0&w=1&usp=send_form) by April 1st