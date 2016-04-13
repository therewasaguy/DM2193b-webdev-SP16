# Wednesday 4/12

## Wrap up final project presentations
1. George
2. Eric
3. Zhijian

## API
API stands for application program interface. It's like the building blocks for software—a set of protocols to interact with the data that powers the application.

An API lets software developers interact with just the data/functionality they need. For example, if I was making an API for myself, I might allow anyone to send me snacks, and to get a list of all the snacks people have given me. I might also allow software developers to get my real name, but I would not allow anyone to give me a new name.

Software is often built with several API's that handle different aspects of the application. API's can be private (used internally) or public. Public API's make a small piece of functionality accessible to the public. Today we will use API's from Google, FourSquare, and built right into our web browsers to fetch nearby locations and display them on a map.

### Web API's
As we've seen, web browsers like Chrome, Safari, Firefox are all a little different. Browsers are built with different programming languages and each implementation has its own quirks. Fortunately, web developers do not have to interact directly with the web browser's source code. Instead, browser manufacturers have agreed upon a common set of **Web API's**. These API's provide standard methods for web developers access to a common set of features. Here is a [list of Web API's](https://developer.mozilla.org/en-US/docs/Web/API). These show up as objects attached to the browser's ```window``` and each object has special properties and methods.

\* *Note that some API's are not implemented across all browsers because browser manufacturers have not settled upon the standard.*


### Web API's: Geolocation
Web Browsers have a [Geolocation](https://developer.mozilla.org/en-US/docs/Web/API/Geolocation) API that lets us access the user's location.


> ##### Aside: running a local server
For security, the browser restricts access to the Geolocation API to servers. Servers use the ```http://``` or ```https://``` protocol. If we try to use it over the ```file:///``` protocol, it won't work (and we won't even see an error). Here are a few of the many ways to create a local server:

> 
- Sublime Text
  - Install [Sublime Server](http://learningcn.com/SublimeServer/) with Package Control.
  - Go to Project menu --> Add Folder to Project. The server will run out of this folder. 
  - Go to Tools --> Sublime Server --> Start Server
  - Right click or ctrl-click on your index.html file and choose View in Sublime Server
- Brackets:
  - File --> Live Preview. This opens the project in a browser window and starts a server out of the project folder.


> We will use a server for the rest of the day.

The `geolocation` API is a JavaScript object that is part of the `window.navigator` object:

```
window.navigator.geolocation
```

Some browsers have not implemented the API. We can make sure it exists like this:

```
function getMyLocation() {
 if (navigator.geolocation) {
  // TO DO
 } else {
  alert("Geolocation is not supported by this browser.");
 }
}
```

Geolocation has a method `getCurrentPosition()` that prompts the user for permission to access their current location. It is ***asynchronous***—the location is not available immediately, we have to wait. Just like a "click" event, getCurrentPosition accepts the name of a callback function. Let's call it `gotPosition`.


```
function getMyLocation() {
 if (window.navigator.geolocation) {
  window.navigator.geolocation.getCurrentPosition(gotPosition);
} else {
  alert("Geolocation is not supported by this browser.");
 }
}
```

If getCurrentPosition is successful, it calls our callback function, and passed in a JavaScript object with all the information we need about the user's position. Let's call that object `position`.

```
function gotPosition(position) {
  // let's check out this object
  console.log(position);
}
```

Inspect the `position` object in the developer console. It has an object called `coords`. We can access the user's latitude with `position.coords.latitude` and longitude with `position.coords.longitude`. Let's use this to display the position on a map!

### Google Maps API
Google Maps API is documented [here](https://developers.google.com/maps/documentation/javascript/).

It requires an **API Key**. The key allows a certain level of access, and allows Google to track your usage of their API.


Click on Get a Key here:
https://developers.google.com/maps/documentation/javascript/

Keep your API private—**never post API keys on GitHub**. Here are Google's [best practices for securing your API key](https://support.google.com/cloud/answer/6310037). You can also add specific hosts as allowed referrers like [this](https://www.dropbox.com/s/0jq1xi1aeay73dk/Screenshot%202016-04-12%2013.25.55.png?dl=0).

Once you have a key, include this script on your page. The callback is the name of a function to call once the script has loaded.

```
<script src="https://maps.googleapis.com/maps/api/js?key=YOUR_API_KEY"></script>
```

In our HTML, create an element with an ID that we can use to attach the map:

```
  <div id="map"></div>
```

In our CSS, give the element a width and a height:
```
    #map {
      height: 300px;
      width:300px;
    }
```

In our JS, let's create a new function called `initMap` that accepts geocoordinates, and call it from `gotPosition` function:

```
function gotPosition(position) {
  initMap(position.coords.latitude, position.coords.longitude);
}

// init the map inside of the #map div
function initMap(myLat, myLng) {
  var container = document.getElementById('map');
  
  // map is a global variable
  map = new google.maps.Map(container, {
    center: {
      lat: myLat,
      lng: myLng
     },
    zoom: 8
  });
}
```

#### Markers
Modify our initMap method to add a marker:

```
  // add a marker
  var marker = new google.maps.Marker({
    position: {
      lat: myLat,
      lng: myLng
    },
    map: map,
    title: 'My location'
  });
```
Read more about Marker at the Google Maps API documentation:
- Demo [here](https://developers.google.com/maps/documentation/javascript/examples/marker-simple).
- Documentation [here](https://developers.google.com/maps/documentation/javascript/3.exp/reference#Marker).

#### Info Windows
We'll use an Info Window to display information about markers when we click on them.

Even if we have multiple markers, the best practice is to have just one info window, and simply change its content and location. So let's create a global infoWindow and initialize it within our initMap function

```
  // infoWindow is a global variable
  infoWindow = new google.maps.InfoWindow({
    content: ''
  });
  
  // addListener is Google Maps' way of adding event handlers
  marker.addListener('click', markerClicked);
}
```

```
// callback when a marker is clicked
function markerClicked() {
  // this = the marker that triggered this event
  infoWindow.setContent(this.title);
  infoWindow.open(map, this);
}
```

Read more about Info Window at the Google Maps API documentation:
- Demo [here](https://developers.google.com/maps/documentation/javascript/infowindows).
- Documentation [here](https://developers.google.com/maps/documentation/javascript/3.exp/reference#InfoWindow).

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