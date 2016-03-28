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

## Sublime Text Features & Packages
* **[Snippets](http://docs.sublimetext.info/en/latest/extensibility/snippets.html)**
  * Reusable code snippets that you can trigger with a `tabTrigger`.
  * Snippets have an optional `scope`, for example you might have a scope for javascript files (`source.js`) and html files (`text.html`). [Here is a list of the available scopes](https://gist.github.com/iambibhas/4705378).
* **Package Control**
  * This is an extension that makes it easy to search and install Sublime Text Packages. 
  * Install Package Control here: https://packagecontrol.io/installation
  * Then access it via Tools > Command Palette, and start typing Package Control.
  * Let's install some packages:
    * **[HTML/CSS/JS Prettify](https://packagecontrol.io/packages/HTML-CSS-JS%20Prettify)** - Make you code look nicer
    * **[HTML5 Snippets](https://packagecontrol.io/packages/HTML5)** - Syntax highlighting + Snippets
    * **[jQuery Snippets](https://packagecontrol.io/packages/jQuery)** - Syntax highlighting + Snippets
    * Browse more [here](https://packagecontrol.io/browse/popular)

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