#Monday 4/18

## Style Guide & Grid System Discussion
References:
  - [Web Style Guide: Design Grids](http://webstyleguide.com/wsg3/7-page-design/7-design-grids.html)
  - [Starbucks Style Guide Promo Layouts](http://www.starbucks.com/static/reference/styleguide/)
  - [Google Material Design](http://www.google.com/design/spec/material-design/introduction.html#introduction-goals)

## API's (continued from week 10)

### Foursquare API
Foursquare has a [Search API](https://developer.foursquare.com/start/search) that accepts a few parameters. We can access it like this: 

```
https://api.foursquare.com/v2/venues/search
  ?client_id=CLIENT_ID
  &client_secret=CLIENT_SECRET
  &v=20130815
  &ll=40.7,-74
  &query=sushi
```

You can register for your API Key (client_id and client_secret) here:
https://foursquare.com/developers/apps

Once you have an API key, you can get search results as JSON by entering the url above and filling in the query parameters.

> aside: install pretty json chrome extension to make json look nice in your browser

Let's add an HTML search field
```
  <form id="4sq-search">
    <input type="text" id="search-query" placeholder="Search Foursquare">
    <input type="submit" value="submit">
  </form>
```

and add an event listener when we submit the form:

```
$(document).ready(setup);

function setup() {
  getLocation();
  $('#4sq-search').submit(search4sq);
}

function search4sq(e) {
  // dont refresh the page
  e.preventDefault();

  // to do...
}
```

You may remember we used a form to query the Spotify API [here](https://therewasaguy.gitbooks.io/nyu-dm-webdev-spring2016-b/content/weekly_detail/week_6.html). This time, rather than submit the form directly using the form's `action=""` attribute, we'll use JavaScript to make the actual query.


### AJAX
AJAX stands for Asynchronous JavaScript and XML. It is a way to load content onto your page without reloading the entire page. It is often used to fetch data from an API.

jQuery has an AJAX module that can help us make AJAX requests. http://api.jquery.com/jquery.ajax/

```
$(document).ready(setup);

function setup() {
  $('#4sq-search').submit(search4sq);
}

function search4sq(e) {
  // dont refresh the page
  e.preventDefault();

  // get searchQuery
  var searchQuery = $('#search-query').val();

  // construct the url to make our ajax request
  var url = api_url + '?client_id=' + myClientID
    + '&client_secret=' + mySecret
    + '&v=20130815'
    + '&ll=' + myLocation.latitude+ ',' + myLocation.longitude
    + '&query=' + searchQuery

  // make ajax request, with success and error callbacks
  $.ajax(url, {
    success: gotData,
    error: onError
  });

}

// callback to do something with the data
function gotData(data) {
  console.log(data);
}

// handle errors
function onError(err) {
  console.log(err);
}
```

We can loop through all the venues in the response data to add markers to the map like this:
```
function gotData(data) {
  console.log(data);

  // this is an array of venue JSON objects
  var venues = data.response.venues;


  // loop thru all the venues
  for (var i = 0; i < venues.length; i++) {

    // current venue
    var venue = venues[i];

    // add a marker to the map
    var marker = new google.maps.Marker({
      position: {
        lat: venue.location.lat,
        lng: venue.location.lng
      },
      map: map,
      title: venue.name
    });

    // add click listener
    marker.addListener('click', markerClicked);
  }
}
```

## Code from class
* [GitHub](https://github.com/therewasaguy/dm2193-4sq-googlemaps) 
* [Dropbox](https://www.dropbox.com/sh/uaud6iv1xdu6al4/AACn1DNpdSQdjJxH_HPqOW2xa?dl=0)

## Exercise Options:
- Customize the Google Maps Info Window to display custom information about the element you've clicked on
- Play with Bootstrap or Foundation components to display information about the search results and to style the page

## HW: 
- Read Brad Frost on "Atomic Web Design" http://bradfrost.com/blog/post/atomic-web-design/
- Read Customizing Bootstrap
https://www.smashingmagazine.com/2013/03/customizing-bootstrap/
- Read CSS Preprocessors: SASS vs LESS
https://www.keycdn.com/blog/sass-vs-less/


# Wednesday 4/20/2016 

## Discuss reading
![](http://bradfrost.com/wp-content/uploads/2013/06/atomic-design.png)
via [Brad Frost, "Atomic Web Design"](http://bradfrost.com/blog/post/atomic-web-design/#templates)

Let's compare Brad Frost's vision of a modular design system with the frameworks we've looked at so far, Bootstrap and Foundation.

## Customizing Bootstrap & Foundation

##### Add your own CSS
  - Example: Make dropdown menus show on hover
  - Use specific CSS selectors
##### Custom JS
  - Bootstrap JavaScript Components have Options Objects with default options that we can override

##### Custom Downloads
- Determine which components you need
- Customize variables

##### Variables
You can customize some of the variables on the "custom download" page. These variables are used by a **CSS pre-processor** and compiled to regular CSS.
- [Customize Bootstrap](http://getbootstrap.com/customize/)
- [Customize Foundation](http://foundation.zurb.com/sites/download.html/#customizeFoundation)


### CSS Pre-processors
CSS Pre-processors allow you to write stylesheets with some of the things CSS should have had in the first place, like **variables**, **mixins**, and **functions**. 

* variables - start with @ (less) or $ (sass)
* mixins 
* functions and if statements / logic

* SASS example:
  * selectors can be nested, i.e. `a` inside of a `nav` is a rule that applies to ```<a>``` elements inside of ```nav``` elements.
  * `$my_color` is a variable
  * `&` refers to the selector the `a`

```
$my_color: rgb(255,0,0);

nav {
     a{
      color: $my_color;
      &:hover {
        color: darken($my_color, 10%);
      }
     }
}
```
The two most popular CSS pre-processors are:

##### 1. SASS/SCSS - http://sass-lang.com/
- SASS stands for Syntactically Awesome StyleSheets and 
- SCSS stands for Sassy CSS. It refers to the syntax and file extension (`.scss`). You can use regular CSS syntax, but it has some nice special features as mentioned above.

##### 2. LESS - http://lesscss.org/
- Very similar to SCSS, but going out of style. 


Pre-processors let you write more consistent, readable stylesheets. For example, if we wanted to change the main color used throughout our style, we can do that by changing one variable rather than finding and replacing every single place we used that color. We can declare those variables in a file called "variables."

Pre-processors are used by both Bootstrap and Foundation.

- Bootstrap 2 and 3 are built with LESS, but v4 will use SCSS.
- Foundation is built with SASS/SCSS

### Compiling CSS from SCSS
If you want to customize Boostrap or Foundation, you are invited to modify the source code and compile:
* Bootstrap 3 has a [variables.less](https://github.com/twbs/bootstrap/blob/master/less/variables.less) file. Bootstrap 4 is switching to use SASS and has a [_variables.scss](https://github.com/twbs/bootstrap/blob/v4-dev/scss/_variables.scss) file. If you want to use scss for Bootstrap 3, there is an official SASS version [here](https://github.com/twbs/bootstrap-sass/). 
* Foundation has a [_global.scss](https://github.com/zurb/foundation-sites/blob/develop/scss/_global.scss) file

You can also take advantage of these powerful features to introduce more powerful CSS for your own project. You'll just need a tool that can "process" less/sass (compile to regular CSS) so that it can run in a web browser.

##### Compass
The easiest option is to use [compass.app](http://compass.kkbox.com/). This is an application that can "watch" folders for changes to .scss files and compile them into .css.

Create a Bootstrap or Foundation project. Compass will watch changes to the .scss files inside of the folder, and generate a regular .css file in the stylesheets folder.

Place an index.html in the root of the folder and link up the stylesheet

```
<!DOCTYPE html>
<html>
<head>
	<title>Hello SASS</title>

	<!-- Latest compiled and minified Bootstrap core CSS -->
	<link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.6/css/bootstrap.min.css">

	<!-- our custom style, generated from scss -->
	<link rel="stylesheet" href="stylesheets/styles.css">

</head>
<body>

    <!-- code here -->

	<script src="https://code.jquery.com/jquery-2.2.3.min.js" integrity="sha256-a23g1Nt4dtEYOj7bR+vTu7+T8VP13humZFBJNIYoEJo=" crossorigin="anonymous"></script>
	<script src="javascripts/bootstrap.js"></script>

</body>
</html>
```

#### In Class Exercise
Customize Foundation or Bootstrap, and experiment with SCSS to design some custom UI organisms. 

#### Online resources
We can generate Bootstrap or Foundation stylesheets and .scss variables from an image.

* Pick an image and upload it to http://www.lavishbootstrap.com/

#### Further Reading
* [Compiling SASS in Sublime Text](http://www.hongkiat.com/blog/sublime-text-compiling-sass/) 
* [An introduction to SASS/SCSS](http://callmenick.com/post/an-introduction-to-sass-scss)
* [Excellent getting started tutorial with interactive examples](https://scotch.io/tutorials/getting-started-with-sass)

<span id="koala"></span> 
### SASS with Koala (addendum) 
For those who had issues with Compass, try [Koala](http://koala-app.com/) (thanks George for the recommendation!) which seems like a better maintained alternative.

If you created a Bootstrap SASS project with Compass, Koala will throw an error because it is trying to import compass-specific modules. We'll go over this in class on Monday.

So let's make a Bootstrap SASS project from scratch. Here's a recommended workflow:

- Create a file structure for yourself like this:

```
my_project/
    index.html
    js/
    css/
    scss/
        style.scss
    vendor/
```

- Open Koala and drag the project folder into the sidebar.
- Right click on the project folder icon, and choose Project Settings --> New Settings --> For SASS.
- This will create `koala-config.json` which you can edit in a text editor. 
- Uncomment and modify the mappings to fit your project structure. For example, our source (src) will be "scss" folder and our destination (dest) will be the css folder:
```
	"mappings": [
		{	
			"src": "scss",
			"dest": "css"
		}
	],
 ```
- modify the "ignores" array to ignore the following files and folders: 
```
	"ignores": ["*.css", "*.js", "vendor"],
```
- Download the SASS port of Bootstrap from [here](https://github.com/twbs/bootstrap-sass) (here is the [zip file](https://github.com/twbs/bootstrap-sass/archive/v3.3.6.zip)). Unzip it and place it in your vendor folder.
- Edit your style.scss file to import Bootstrap:
```
@import "../vendor/bootstrap-sass-3.3.6/assets/stylesheets/bootstrap";
```
Check out the style.css file that was created in your CSS folder: it is Bootstrap! That one line imports all of Bootstrap from the .scss file located at vendor/bootstrap-4-dev/scss/bootstrap.
- Open that scss file: It simply imports .scss files in order. 
- Add a line after `@import "variables";` where you can import your custom variables. Call it `@import "../../../scss/custom-variables";` This is the only modification that we will make to Bootstrap's actual source code, allowing us to override Bootstrap's default variables as needed from our own file that lives in the scss folder.
- Create a file in `scss/` folder called `_custom-variables.scss`. This is where you can override Bootstrap's default variables.





## HW (due Monday)
* **Organism Analysis:** Pick a website and identify three of its "organisms" (aka components, as defined by Brad Frost). What CSS classes does the site use to describe these organisms? How does the user interact with them? Create a post in the Slack #HW channel, title it #hw11a.
* **Read** Dan Mall's short article on [Element Collages](http://danielmall.com/articles/rif-element-collages/). Browse some of the collages on [this page](http://rif.superfriend.ly/) like Design System, Element Exploration, Header, Footer, Donate Dropdown, Donate Button, Navigation on small screens. 
* **Organism Collage:** Customize Bootstrap or Foundation to incorporate the colors, fonts and grid system described by your Style Guide. Create a collage of three (or more) of the "molecules" or "organisms" that you plan to use in your website. These could be Bootstrap/Foundation components, or custom element combinations. Post a link to your website in the Slack #HW channel with hashtag #hw11b.
* **Browse** The website of [Stefan Kaltenegger](http://www.stefankaltenegger.com/), who will be our guest on Monday to talk about his work as an interaction designer and developer for web and mobile. 