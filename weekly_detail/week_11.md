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

## In-Class Exercise Options:
- Customize the Google Maps Info Window to display custom information about the element you've clicked on
- Play with Bootstrap or Foundation components to display information about the search results and to style the page

## HW: 
- Read Brad Frost on "Atomic Web Design" http://bradfrost.com/blog/post/atomic-web-design/
- Read Customizing Bootstrap
https://www.smashingmagazine.com/2013/03/customizing-bootstrap/
- Read CSS Preprocessors: SASS vs LESS
https://www.keycdn.com/blog/sass-vs-less/