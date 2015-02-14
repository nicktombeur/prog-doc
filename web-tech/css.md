
# General CSS

**Links:**

  * [css-tricks](http://css-tricks.com/)

Reset default browser styles, before styling. 

Example:

```css
html, body, h1, h2, h3, p, ol, ul, li a {
    padding: 0;
    border: 0;
    margin: 0;
    font-size: 100%;
    font: inherit;
}
```

Or use something like [this](http://meyerweb.com/eric/tools/css/reset/) or [normalize.css](https://necolas.github.io/normalize.css/).

Always add an alt to the image tag for accessibility (screen readers, etc).

Always set a background color in case the background image fails to load.

## Boxing

Padding can be used to adjust spacing within a container.

Margin can be used to adjust spacing between containers.

## Centering

  * Children inside a block-level tag: 
    * `text-align: center;`
  * Center an entire block-level tag: 
    * `margin: 0 auto;`
  * Inline-level tags (eg. img):
    * `display: block; margin: 0 auto;`

`
`

**Clearing floats**

The clearfix:

```css
.group:before, .group:after {
    content: "";
    display: table;
}
.group:after {
    clear: both;
}
.group {
    zoom: 1; /* IE6&7 */
}
```

**Priority of a selector (specificity)**

important < inline-css < id < class < element

Advised: keep amount of id's low. ([article](http://screwlewse.com/2010/07/dont-use-id-selectors-in-css/))

**Positioning**

Elements have a position value of static by default:

position: static / relative / absolute / fixed

Using a value other than static causes an object to become a positioned element.

Positioned elements may use the top, left, bottom, and right properties for placement.

  * Relative
    * Renders as static, but has ability to use top, left, bottom, and right.
  * Absolute
    * Takes an element out of the normal flow for manual positioning.
  * Fixed
    * Affixes an element to a specific place in the window, where it will stay regardless of scrolling.

**z-index**

Elements must be positioned for z-index to take effect. Use relative if you're not interested in moving the object.

[Understanding z-index](https://developer.mozilla.org/en-US/docs/Web/Guide/CSS/Understanding_z_index)

**DRY**

Don't Repeat Yourself.

  * Use shorthand style
    * margin: 15px 10px 0 20px;
  * Define it in the body element
  * Use a class
  * Selector combiation
    * p, h6, .something { font-size: 12px; }
  * Selector abstraction
    * Example:
```css
.button {
    background: #fff;
    border: 1px solid #000;
    color: #333;
    cursor: pointer;
}
.submit {
    background: #555;
}
```

```html
<input type="submit" class="button submit" />
<a href="a_page.html" class="button">A Page</a>
```

Remember: order matters here (cascading)!

**Display types**

  * Block elements
    * Stretch the full width of their container
    * Behave as though there is a line break before and after the element
    * Full box model can be manipulated
      * tags by default: div, p, ul, ol, li and h1 through h6
  * Inline elements
    * Typically found within block-level elements
    * Only take up the space of the content inside
    * Do not generate a line break before and after the content
      * tags by default: span, a, em, img, and strong
  * Inline-block
    * Same flow as an inline element but behave as a block element
      * no default display type
  * [And more...](http://www.w3schools.com/cssref/pr_class_display.asp)

**Collapsing Margins**

[More information.](http://www.w3.org/TR/CSS2/box.html#collapsing-margins)

**Image use**

  * Content should be marked up as inline images
  * Layout elements should be defined as background images

**Sprites**

Issues with swapping background images:

  * Adds an extra HTTP request
  * Image is not preloaded --> flashes

Therefore combine the image into one file (sprite) and use background-position.

Example:

```css
.logo {
    background: url(logo.png);
    display: block;
    height: 100px;
    width: 200px;
    text-indent: -9999px; --> used for accessibility (we give our logo a text and then hide it).
}
.logo:hover, .logo:focus {
    background-position: 0 -100px;
}
```

Advantages to the sprite approach:

  * Reduces number of HTTP requests
  * Removes loading flash / need for preload

Useful tool: [spritecow](http://www.spritecow.com/).

Alternative to sprites: [base64 encoding](http://davidbcalhoun.com/2011/when-to-base64-encode-images-and-when-not-to/).

**Pseudo classes**

Allow you to conditionally select an element based on state or position.

Examples:

  * :hover
  * :focus
  * :nth-child(even)
    * example of selecting 4th element: :nth-child(4n+1)

Article: [Meet the Pseudo Classes Selectors](http://css-tricks.com/pseudo-class-selectors/)

**Pseudo elements**

  * :before / :after
    * requires content (can be empty)
  * :first-letter / :first-line
  * ...

Article: [A Whole Bunch of Amazing Stuff Pseudo Elements Can Do](http://css-tricks.com/pseudo-element-roundup/)

**CSS3**

border-radius: 

` <top left> <top right> <bottom right> <bottom left>`

box-shadow: 

` <inset*> <offset-x> <offset-y> <blur-radius*> <spread-radius*> <color*>`

  * You can specify multiple box-shadows via a comma-separated list
  * You can also specify negative values

text-shadow: 

` <offset-x> <offset-y> <blur-radius*> <color*>` (note: exists before CSS3)

* = optional

**Box Sizing**

  * Context-box
    * default value
    * width and height are measured by including only the content, but not the border, margin, or padding.
  * Padding-box
    * width and height include the padding, but do not include the border or margin.
  * Border-box
    * width and height include the padding and border, but not the margin.

e.g.

box-sizing: border-box;

**Multiple backgrounds**

background: url(bg1.png) top left no-repeat, url(bg2.png) center right no-repeat;

**Gradients**

Linear gradient

linear-gradient(`<angle*> to <side-or-corner>, <color-stop>s`)

e.g. background: linear-gradient(to bottom, red, yellow);

  * angle: generally a degree (e.g. 45deg).
  * side-or-corner:
    * horizontal: left or right
    * veritcal: top or bottom

\--> We can specify the direction through an angle or a keyword.

Keywords:

  * to top --> 0deg
  * to bottom --> 180deg
  * to right --> 270deg
  * to left --> 90deg

Radial gradient

radial-gradient(`<shape*> <size*> at <position*>, <color-stop>s`)

e.g. background: radial-gradient(aqua, blue);

  * shape: circle or ellipsis (default).
  * size keywords (can also be a length or percentage):
    * closest-side
    * closest-corner
    * farthest-side
    * farthest-corner (default)
  * position: default is center.

e.g. background: radial-gradient(circle at top left, aqua, blue);

**Font face**

Example:

```css
@font-face {
    font-family: 'OpenSansRegular', Helvetica, Arial, sans-serif;
    src: url('OpenSansRegular-webfont.eot');
    font-style: normal;
    font-weight: normal;
}
```

use: `font-family: 'OpenSansRegular';`

`
`

` `

**Transform**

  * translate
    * transform: translate(`<tx>, <ty*>`);
    * transform: translateX(`<tx>`);
    * transform: translateY(`<ty>`);
  * rotate
    * transform: rotate(45deg);
  * scale
    * transform: scale(`<sx>, <sy*>`);
    * transform: scaleX(`<sx>`);
    * transform: scaleY(`<sy>`);
  * skew
    * transform: skewX(`<ax>`);
    * transform: skewY(`<ay>`);

**Transitions**

transition: `<property*> <duration*> <timing-function*> <delay*>`

  * timing-functions
    * ease
    * ease-in
    * ease-in-out
    * linear
    * cubic-bezier
    * step-start
    * step-end
    * steps()

* * *

**Tricks etc**

**Circle**

```css
.circle {
    width: 40px;
    height: 40px;
    border-radius: 50%;
}
```
