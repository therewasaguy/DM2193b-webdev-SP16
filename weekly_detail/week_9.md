# Friday 4/8

## JavaScript

### Review
##### Return
Every JS function/method will `return` something, whether you tell it to or not. By default, JavaScript functions return `undefined`. But we will often create functions that return some value.

##### Types
When we use JavaScript to access DOM elements, their values will typically be a string. For example, this element's value will be a string

```
<input id="num" type="number">
```

The below example uses jQuery, and the [`typeof`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/typeof) operator which lets us check the type of our variables.

```
var val = $('#num').val();
console.log( typeof val );
```

We can convert a String to a Number using the Number(), parseFloat() or parseInt() methods.
- **`parseInt()`** returns the first integer value that it finds within a string. For example it can parse the number `20` from this: `parseInt("20px")`. It does not do any math, so `parseInt("20.999")` will also return 20, and so will `parseInt("20 * 5")`
- **`parseFloat()`** looks for floating point values (ie. `parseInt("20.999")` --> `20.999`
- **`Number()`** converts a string to a number.

When a function is unable to convert a value to a number, it returns `NaN` which means that the value is "Not a Number".

### `Math.random()`
[The `Math` object](http://www.w3schools.com/js/js_math.asp) has special mathematical methods. We'll use some of them:
- `Math.random()` - generate a random float between 0.0 and 1.0
- `Math.round()` - round to the nearest integer
- `Math.floor()` - round down

```
// return either a 1 or a 0
function yesOrNo() {
  return Math.round(  Math.random()  );
}
```

```
// return a number greater than 0 and lower than the limit
function randomNumber( limit ) {
  return Math.floor(  Math.random() * limit );
}
```

##### Random from Array
Using the `randomNumber` function we created above, we can access a random item from an array.

```
var students = ["Yuening", "Polina", "Nicole", "James C", "Susie", "Joon Hee", "George", "Stephen", "Tyler", "Eric", "James T", "Grace", "Echo", "Camille", "Zhijian", "Joy", "Jamie", "Cindy" ];

function randomStudent() {
    var index = randomNumber(students.length);
	return students[index];
}
```

##### Shuffling an Array
JavaScript Arrays don't have a built-in "shuffle" method. So there are many approaches we could take to shuffling an array.

The Fisher–Yates shuffle algorithm is the most efficient and most truly random approach. Mike Bostock, creator of the D3 library, explains here: https://bost.ocks.org/mike/shuffle/

You're encouraged try your own shuffling method here: https://bost.ocks.org/mike/shuffle/compare.html

The [lodash.js](https://lodash.com/) library is a useful tool for these types of array operations, and it has a Fisher–Yates shuffle method. Let's use it!

```
<!-- lodash -->
<script src="https://cdn.jsdelivr.net/lodash/4.8.2/lodash.min.js"></script>

```

```
students = _.shuffle(students);
console.log(students);
```

lodash also has a [random](https://lodash.com/docs#random) method - you can check out the documentation [here](lodash.com). 

## Bootstrap

Here's the code we'll use to make a grid of buttons. Look at the CSS for each class.

```
<div class="row">
    <div id="pick" class="btn well col-xs-12 col-md-3">
        <h3>Random Student</h3>
    </div>
    <div id="shuffle" class="btn well col-xs-12 col-md-3 col-md-push-1">
        <h3>Shuffle</h3>
    </div>
    <div id="clear" class="btn well col-xs-12 col-md-3 col-md-push-2">
        <h3>Clear</h3>
    </div>
</div>
```

Notice how `btn` class center aligns text, and adds cursor, and active pseudoclasses. The `well` and `btn` both have rounded corners. How would we override these styles?


### Bootstrap JavaScript Components
Components use HTML `data-` attributes to pass data from elements that trigger a DOM event to the JavaScript event handler.

For example, let's add a [popover](http://getbootstrap.com/javascript/#popovers) that gives us more information when we hover over each button.

We can add HTML attributes for ```data-toggle```, ```data-content``` and `title`:
```
<div id="pick" class="btn well col-xs-12 col-md-3" data-toggle="popover" title="Pick" data-content="Pick a random student">       
 ```
 
 Certain bootstrap javascript components are "opt-in" meaning we must register event listeners when the page loads. We can do this using a CSS selector and jQuery:
```
$('[data-toggle="popover"]').popover();
```

The popovers can be initialized with an **[options object](http://getbootstrap.com/javascript/#popovers-options )** or additional `data-` attributes that override the default behavior. For example, the default behavior is to trigger the popover on click. These are buttons, so they should popover on hover, when the user is thinking about whether to click them. To do this, we can create an options object:

```
var options = {
  'trigger': 'hover
}

$('[data-toggle="popover"]').popover(options);

```

A shorter approach is to pass the option in directly to the popover() method, like this:

```
$('[data-toggle="popover"]').popover({
  'trigger': 'hover'
});
```


## Code from class
https://www.dropbox.com/sh/cpykct4f1mp79j5/AADkpiJ2v2HVSowwPktmQKq_a?dl=0

## HW: 
* [Final Project Proposals](https://therewasaguy.gitbooks.io/nyu-dm-webdev-spring2016-b/content/assignments/final.html):
  * Project Plan
  * Wireframe
  * Site Map
  * Style Guide
  * ~4 minute presentation
  * Post a file to Slack #hw channel that links all of the above and the file should be named `<your_name>_-_final_project_proposal`

More info about the Final Project can be found [here](https://therewasaguy.gitbooks.io/nyu-dm-webdev-spring2016-b/content/assignments/final.html).