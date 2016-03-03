# Monday 2/29
* Review Midterm Guidelines
* Office Hours reminder: by appointment, or [additional office hours on Wednesday](https://calendar.google.com/calendar/selfsched?sstoken=UUNfTDZzX1BtWUJxfGRlZmF1bHR8NWQxNmRiM2JiYTc4OTIwOGU5MTQ1MzFiNjBhOWFiZDg)
* Show & Tells: George, Camille, James C
* [User Testing](https://slides.com/jasonsigal/user-centered-design) (slides)
* User Test Responsive Prototypes
* HTML5 Audio/Video
* Intro to Git & GitHub
* Review Topics
* Non-Quiz...?


### HTML5 Audio & Video
* `<audio>` and `<video>` elements
* Some useful attributes:
    * `autoplay` `muted` `loop` `poster="path/to/image"`
* Useful resource: archive.org ([example](https://archive.org/details/20130601014733))
* Formats supported by various browsers. See sub-features for video [here](http://caniuse.com/#feat=video) and for audio [here](http://caniuse.com/#feat=audio). It is best to include multiple sources. Example:
```
<video autoplay loop muted poster="video/stock_flowers.jpg">
    <source src="video/stock_flowers.mp4">
    <source src="video/stock_flowers.ogv">
</video>
```

### Git / GitHub
* Git - Version Control
* Key vocab from the [GitHub Glossary](https://help.github.com/articles/github-glossary/#branch): 
  * **repository** - Project folder.
  * **commit** - A revision to a file or set of files. Add files before committing them.
  * **fork** - A personal copy of another user's repository that lives on your account
  * **clone** - A copy of a repository that lives on your computer instead of on a website's server.
  * **merge** - Combine changes. Git can merge changes automatically.
  * **push** - Send your committed changes to a remote repository
  * **pull** - Fetch changes and merge them
  * **pull request** - A request to merge (pull) changes
  * **remote** - A version of a repository that is hosted somewhere else, for example on GitHub's server.
* [GitHub](http://github.com) - a website to host "git repositories"
* In class exercise:
  * Fork my repo to your github account
  * Clone it to your computer
  * Edit the index.html to add a link to your GitHub account
  * Commit your changes
  * Push your committed changes to your fork
  * Submit a pull request from your fork to the original repo. I will merge in the changes.




### HW
* Read up on [GitHub](https://guides.github.com/)
* Post your project to your personal GitHub.
* Submitting a pull request to [this github repo](https://github.com/therewasaguy/class_github_video) that adds a link to your github account.
* Review the [Non-Quiz](https://www.dropbox.com/s/uw4yz9bg8nq0rhe/webdev2193NonQuiz1.pdf?dl=0) and come to the next class with any questions related to this or your midterm projects / self learning 

# Wednesday 3/2
## Grid Review
* [Example from class](https://www.dropbox.com/sh/3hpvsp2odfkjh42/AAAJ8NtZpxKa37UaHUXBkXfVa?dl=0)
* Based on [this Grid Tutorial](http://www.w3schools.com/css/css_rwd_grid.asp) recommended by Tyler

## Forms & User Input
Forms and Input elements allow the user to interact and submit information. Typically forms "submit" to a server with a GET or POST request.
* A `<form>` element wraps one or more elements that accept user input. Their `name` attribute determines the name for a set of name-value pairs (often referred to as "key-value pairs"). The form has two important attributes:
 * ```action``` attribute determines a url that the form will submit its data
 * ```method``` is an HTTP request method, either `get` (default) or `post`. A get request is the type of request we make with our browsers when we load a webpage, and the result will look something like this: http://formactionurl.com/?key=value&key2=value2. 
* `<input>` has a `type` attribute. There are many different types including
  * `text` - text input
  * `radio` - radio button. A set of radio buttons shares a `name` and only one of them can be selected. Each has a unique `value`. That value becomes the value for that name/key.
  * `color` colorpicker
  * `search`
  * `email`
  * `password`
  * `date`
  * `button` - same as a `<button>` element
  * `submit` - **button that submits the form**
  * Read more about types [here](http://www.w3schools.com/html/html_form_input_types.asp) and about input attributes [here](http://www.w3schools.com/html/html_form_attributes.asp).

* `<label>` is a way to label a form element. Its attribute `for="name"` determines the name of the input element it references.
* `<select>` - a dropdown with several `<option>` elements. The select has a ```name``` attribute, and can have a ```multiple``` attribute to allow selection of multiple options. Read more [here](http://www.w3schools.com/tags/tag_select.asp).

In our [example in class](https://www.dropbox.com/s/1euourpmllpe1bc/index.html?dl=0), we submitted a form to the Spotify API that looked like [this](https://api.spotify.com/v1/search?q=hello&type=artist).


```
  <form action="https://api.spotify.com/v1/search" method="GET">

    <!-- a text input fills out the q= value -->
    <label for="q">Enter a search query</label>
    <input name="q" type="text" placeholder="Enter Text">

    <br/>

    <!-- two radio buttons share the same name, to fill out the type of thing we're searching for, either type=artist or type=track -->
    <label for="type">Choose a type</label><br/>

    <label for="artist">Artist</label>
    <input id="artist" name="type" type="radio" value="artist">
    
    <label for="track">Track</label>
    <input id="track" name="type" type="radio" value="track">

    <input type="submit">
     Click to submit
    </input>
  </form>
```


##JavaScript (JS) <small>(We did not cover this, will cover it after Spring Break)</small>
If HTML is the content, and CSS is the presentation, then JS is the behavior of your website. JS adds interactivity—it can respond to user interaction—and it makes the site more dynamic.

Use JavaScript to **access and modify HTML/CSS content** from your website. For [example](https://d157rqmxrxj6ey.cloudfront.net/jasonsigal/35860/), we can change the class to apply a whole new set of CSS rules.

JavaScript also reacts to **events**, like mouse clicks, key presses, modifications to a form.

Finally, JavaScript is a programming language—a way to add traditional rules and computation to your website. For example, it can filter through content, and do math.

### Script
A script is a series of instructions. It might include blocks of code that respond to certain events, or run only in certain cases (i.e. if something is true, or false).

JavaScript typically goes inside the ```<head> </head>```, or at the bottom of the ```<body> </body>```, of our HTML pages. 

JS can be inside of a `<script>` tag like this:

```
<script type="text/javascript">
   console.log('Hello World');
</script>
```

Or, put your code in a separate file, and use the `src` attribute to link to that file like this:

```<script type="text/javascript" src="js/script.js"></script>``` (*note that you still need to close the `<script>` tag)

### JavaScript Console
The **console** is available in [Chrome](https://developer.chrome.com/devtools/docs/console), [Firefox](https://developer.mozilla.org/en-US/docs/Tools/Web_Console/The_command_line_interpreter) / [Firebug](http://getfirebug.com/logging), and other browsers. This is where you'll see error messages, and print messages using ```console.log('my message')```. It is **interactive**—it's a place to type JavaScript and test it out live in the browser. If you want to learn JavaScript, make good friends with the Console.


### Objects
Objects can have **Properties** (Variables that are part of the, **Events**, and **Methods** (Functions of an Object). For example ```console``` is an object, and ```console.log()``` is one of its methods.

##### Window Object
```window``` is a JavaScript object that represents the browser.

##### Document Object
`document` aka `window.document` is a JavaScript representation of the HTML content of your webpage. This is known as the Document Object Model, aka the [DOM](https://developer.mozilla.org/en-US/docs/Web/API/document) or DOM Tree. Image [CC-BY Marty Step](http://courses.cs.washington.edu/courses/cse190m/07sp/lectures/slides/08-dom.html) 

![](dom_tree.gif)

The document allows us to access Elements with methods like
`document.getElementById('my-id');` ([more info](https://developer.mozilla.org/en-US/docs/Web/API/Document/getElementById))


##### DOM Element Object
A few useful properties of all DOM element objects:
* `element.innerHTML` Sets or returns the content of an element
* `element.classList` Returns the className(s) of an element. The classList has useful methods: `add()`, `remove()`, and `toggle()`

### Variables
JavaScript variables store data whose value may vary (hence the name variable). Variables can be declared with a statement that gives them a name `var myName;`.

#### Variables & Data Types
Here are a few examples of assigning variables for different data types:

#####Strings
```
var myString = "some text"
var myString = 'some text'

// Use either single or double quotes, but be consistent. This is helpful if you want actual quotation marks to appear in the string like this:
var quote = 'Like Douglas Crockford said, "Obsolete comments are worse than no comments"';
```

#####Numbers
```
var x = 123 // integer
var y = 12.32139021 // float
```

#####Booleans
```
var raining = true;
var snowing = false;```

##### DOM Elements
Cache a reference for a "DOM Query":<br/>
```
var myDiv = document.getElementById('my-id');
var listItems = document.querySelectorAll('li.ingredients'); // CSS selector
```

##### Arrays [ ]
```
var students = ['Joon Hee', 'Stephen', 'Zhijian'];
var things = [3, 'dog', true, '3']; // arrays can mix types (be careful with this!)
```


##### Objects { }
Objects contain values with names. This is known as a "key : value" pair.
```
var restaurantData = {
  name: "morimoto",
  city: "New York",
  cuisine: "Japanese",
  thumbsUp: 4,
  thumbsDown: 1
}

console.log("the name of the restaurant is " + restaurantData.name + " and it is located in " + restaurantData.city);

// returns:
// the name of the restaurant is morimoto and it is located in New York
```

###Expressions
Expressions are a combination of values, variables and operators that convert to a value. For example, we can use arithmetic[ operators](http://www.w3schools.com/js/js_arithmetic.asp) like `+` `-` `/` `*`. Modulo (`%`) returns the division remainder, `++` increments and `--` decrements.

```
var x = 8 + 1;
var y = x % 2;
```

JavaScript also provides special methods for working with [Numbers](http://www.w3schools.com/js/js_number_methods.asp) and working with [Strings](http://www.w3schools.com/js/js_string_methods.asp).

##### Boolean / Comparison and Logical Operators
Evaluating whether a statement is true or false can be very powerful. Operators like `<` `>` `==` (equal) are very useful.

```
1 == "1" // evaluates to true
1 === "1" // evaluates to false, because a String and a Number are not strictly equal.
```

[Read more](http://www.w3schools.com/js/js_comparisons.asp)

### Events
`element.addEventListener('click', myFunction, false);`

### Functions
A function is a group of statements. When a property is part of an object, it's called a `method`.

Functions can accept parameters, like "name" in the example below.

```
function sayHi(name) {
  document.write("Hi, " + name);
}
```

Functions can also return a value with the keyword `return`

```
function addNumbers(num1, num2) {
  return num1 + num2;
}
```

We *call a function* like this: 
```
addNumbers(3, 5);
sayHi("Jason");
```


### Further Reading (over break)
* http://jsforcats.com/
* http://www.w3schools.com/js/js_datatypes.asp
* Many additional resources are listed in our [Readings & Resources](https://therewasaguy.gitbooks.io/nyu-dm-webdev-spring2016-b/content/readings_resources.html) page