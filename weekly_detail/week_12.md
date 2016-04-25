# Monday 4/25

## Guest [Stefan Kaltenegger](stefankaltenegger.com) 

## Review HW
* Use Randomizer http://therewasaguy.github.io/dm2193-random/ ([source code](https://github.com/therewasaguy/dm2193-random))

## Animation & Tweening
**Tween** - "Short for in-betweening, the process of generating intermediate frames between two images to give the appearance that the first image evolves smoothly into the second image. Tweening is a key process in all types of animation, including computer animation. Sophisticated animation software enables you to identify specific objects in an image and define how they should move and change during the tweening process."
(via [webopedia](http://www.webopedia.com/TERM/T/tweening.html))

## Let's review
Some animation options that we have already covered:

* #### CSS Transitions

```
div {
    transition-property: width;
    transition-duration: 2s;
    transition-timing-function: linear;
    transition-delay: 1s;
}
```

* #### jQuery animations

```
$('#myButton').hide(2);
```

## setInterval

You can schedule events over time using JavaScript.

Schedule an event to happen at `millis` in the future:
```
setTimeout(someFunction, millis);
```

Run repeatedly every `millis` milliseconds:
```
setInterval(someFunction, millis);
```

Assign the interval to a variable...
```
var myInterval = setInterval(someFunction, millis);
```

if you want to cancel it later:
```
clearInterval(myInterval);
```

## GreenSock Animation Platform (GSAP)
GreenSock is a set of JavaScript libraries for animation, including TweenLite/TweenMax and TimelineLite/Timeline/Max. 

*The max versions have additional plugins that you would have to include seprately if you use the Lite versions.*

Download and find the CDN links [here](http://greensock.com/get-started-js#loading) and include it in your page:

```
<script src="https://cdnjs.cloudflare.com/ajax/libs/gsap/1.18.0/TweenMax.min.js"></script>
```

#### Tweening JS Object Properties
We can tween numeric properties of JavaScript objects. The most common is [`.to`](http://greensock.com/docs/#/HTML5/GSAP/TweenLite/to/) where you don't care about the starting value, just the value you're transitioning to.
```
var obj = {
	count: 0
};

// obj.count --> 100 over the course of 20 seconds
var tween = TweenLite.to(obj, 20, {
	count: 100,
});
```

To view the values, we could log them using a setInterval:

```
var myInterval = window.setInterval( function() {
  console.log(obj.count);
 }, 300);
```

#### Tweening HTML Element / CSS Properties

```
<button id="red-bar" style="background-color:red;"></button>
```

In JavaScript:
```
var tween = TweenLite.to('#red-bar', 5, {
  width: "100%"
});
```

Here, we gave tween a css selector, `"#red-bar"`. Alternately, we could also pass in
- a jQuery element `$('#red-bar')`
- a DOM element `document.getElementbyId('red-bar')`

#### Easing
The Tweens can be linear, or non-linear. There are many easing functions to choose from to get different types of transition effects. Let's play with them on GreenSock's website!

[![http://greensock.com/get-started-js#easing
](ease-viz.png)](http://greensock.com/get-started-js#easing)

http://greensock.com/get-started-js#easing


#### Controlling Tweens
Every time you create a Tween, you can assign it to a variable which gives you more control. For example, you can pause, reverse, and change the speed. Read more [here](http://greensock.com/get-started-js#controlling).

#### Timeline
GreenSock's Timeline is for grouping and sequencing multiple Tweens.

```
//create a TimelineLite instance
var tl = new TimelineLite();
```

Instead of calling TimelineLite, you can append tweens directly to the timeline:
```
tl.to("#red-bar", 5, {
  width: "100%"
});
```

By default, tweens trigger in sequence, one after the other. You can give them offsets by passing in a third option like this:

```
tl.to("#red-bar", 1, {opacity:0.5}, "+=0.75");
```

Use timeline.call(myFunction) to call functions at moments during the timeline.

```
tl.call(myFunction);
```

Read more:
http://greensock.com/get-started-js#sequencing



Resources:
* [Docs for TweenLite](http://greensock.com/docs/#/HTML5/GSAP/TweenLite/TweenLite/)
* Interactive examples on [CodePen](http://codepen.io/collection/ifybJ/) - http://greensock.com/jump-start-js
* Longer more detailed intro - https://greensock.com/get-started-js
* Download - https://greensock.com/gsap
* Cheat Sheet - [link](https://ihatetomatoes.net/wp-content/uploads/2015/08/GreenSock-Cheatsheet2.png)

