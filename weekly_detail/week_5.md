# Week 5

## Monday Feb 22

### Responsive / Mobile First, CSS Transitions
* <a href="https://slides.com/jasonsigal/responsive">**Slides: Responsive Web Design & Mobile First**</a>
* Responsive vs Mobile First
* Meta [Viewport](https://developer.mozilla.org/en-US/docs/Mozilla/Mobile/Viewport_meta_tag)
* Media Queries

#### Fun with CSS3:

* **[Transition](http://www.w3schools.com/css/css3_transitions.asp)** - Transform almosst any CSS property by animating the change in value from one to the other. Here's a [Thimble example](https://d157rqmxrxj6ey.cloudfront.net/jasonsigal/36111/).

```
 /**
 property - name of the CSS property
 duration - in seconds, i.e. 2s
 **/
 .my-class {
     transition: background-color 1s
 }
 
```

* [**Transform**](https://developer.mozilla.org/en-US/docs/Web/CSS/transform) - Change the position or size of an HTML element. Options include `skew` `scale` `rotate` `translate` `scale3d` `rotate3d` `translate3d`. Here's a [Thimble example](https://d157rqmxrxj6ey.cloudfront.net/jasonsigal/36115/) combining scale and skew.

 ```
     .zoom-in {
         transform: scale(2);
     }
     .zoom-out {
         transform: scale(0.5);
     }
 ```

* **[Filter](http://www.w3schools.com/css/css3_filters.asp)** Apply a visuaul effect to an element. Not covered yet in class, but feel free to explore.
* **[Animation](http://www.w3schoolsom/css/css3_animations.asp)** Applyustom / complex animations withultiple "keyframes" over time. Notovered yet in class, but feel free to explore.
* Show & Tells: Polina and Echo

#### JavaScript preview. <small>Note: This is not required for the midterm, we'll cover more in depth after the break</small>
* HTML elements can trigger JavaScript functions. A great example is the html `onmousedown="nameOfFunction()"` attribute because it works on desktop and mobile. The function name is case sensitive. Here's a ([demo](http://www.w3schools.com/tags/ev_onclick.asp)).
* JavaScript lives inside of a script element in the `<head>` of the page:
        <script type="text/javascript">
            function myFunction() {
                // javascript goes here
            }
        </script>
* [document.getElementById("id-of-element")](http://www.w3schools.com/jsref/met_document_getelementbyid.asp) Returns the HTML element as a JavaScript object that we can manipulate.
* [classList.toggle("name-of-class-to-add-or-remove")](http://www.w3schools.com/jsref/prop_element_classlist.asp) Returns the HTML element as a JavaScript object that we can manipulate.

#### Code from class
https://d157rqmxrxj6ey.cloudfront.net/jasonsigal/36163/


#### More things that came up in class:
* &#9776; [CSS Tricks: Three line menu navigation](https://css-tricks.com/three-line-menu-navicon/). Find more special html/unicode characters [here](http://unicode-table.com/en/).
* Vendor Prefixes. Some newer CSS properties like `transition` `transform` `filter` `animation` and `flexbox` require vendor prefixes to render properly on all browsers. You can check at [shouldiprefix.com](http://shouldiprefix.com/#flexbox).


#### HW:
<ul>
    <li>Redo prototypes, make them responsive, prepare for user testing on Feb 29th (due 2/29)</li>
    <li>Read <a href="https://developers.google.com/web/fundamentals/design-and-ui/responsive/patterns/?hl=en">Responsive Patterns</a> and <a href="https://css-tricks.com/snippets/css/a-guide-to-flexbox/">Guide to Flexbox.</a> Try one of the examples on your own.</li>
    <li>Read <a href="http://css3.bradshawenterprises.com/">CSS3 Transform, Transition, Animation Tutorial</a></li>
</ul>
DUE: Style Guide<br/>

## Wednesday Feb 24
* CSS Transform, Transition, Filter, Animation (continued)
* Review: CSS Display property
    * By default, all HTML elements are either `display:inline` (e.g. `<span>`) or `display:block` (e.g. `<div>`).
    * `float` `clear`
* Flex Box basics:
    * Containers can have:
        * `display: flex`
        * `flex-flow: [flex-direction] | [flex-flow]`
            * `flex-direction: row | column | row-reverse | column-reverse | initial | inherit`
            * Default value is "row".
            * `flex-wrap: wrap | no-wrap | wrap-reverse` Default value is "nowrap".
    * Items within containers can have:
        * [flex](http://www.w3schools.com/cssref/css3_pr_flex.asp)
        * order
* Use `calc` to calculate dimensions (i.e. max-width) with both fluid (%) and fixed (px) numbers. Example syntax: `calc(50% - 10px)`. For example, this would be useful if you need to account for the margins that surround an element (or border and padding if your `box-sizing` is the default of `content-box` instead of `border-box`).
* Guest Claire Kearney-Volpe from [NYU's Ability Lab](http://abilitylab.nyu.edu/) on Web Accessibility and User-Centered Design ([slides](https://www.dropbox.com/s/fr4bs665j02jffl/webaccess.pptx?dl=0))

HW:
* Continue work on your midterm/prototypes, make them responsive, prepare for user testing on Monday