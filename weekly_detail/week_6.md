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