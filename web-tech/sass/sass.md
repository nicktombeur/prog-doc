**Links**

  * [Documentation](http://sass-lang.com/documentation/file.SASS_REFERENCE.html)
  * [Sass vs. LESS](http://css-tricks.com/sass-vs-less/)

Always, always check the CSS output of your Sass before using it on a live site.

<br />

**Comments**

```scss
// These comments will

// not be output to the

// compiled CSS file

/* This comment will */
```

<br />

**Import**

The CSS @import has been avoided because of parallel downloading.

@import with .scss or .sass happens during compile rather than client-side.

<br />

**Partial**

If you create a file "buttons.scss" and import it into the file "application.scss", the application file will also include the buttons. But it will also generate a file for buttons (buttons.css).

To prevent this we use partials.

Adding an underscore creates a partial ( _buttons.scss ). 

Partials can be imported, but will not compile to .css.

Note: you don't have to write the underscore in the import statement.

<br />

**Nesting selectors**

Example:

```scss
.content {
    border: 1px solid #fff;
    h2 {
        margin: 20px 0;
    }
    p {
        font-size: 1.5em;
    }
}
```

While nesting, the & symbol references the parent selector.

Very useful for pseudo classes and pseudo elements (see CSS for explanation).

Example:

```css
.content {
    /* ... */
    .callout {
        /* ... */
    }
    &.callout {
        /* ... */
    }
}
```

compiles to:

```css
.content {
    /* ... */
}
.content .callout {
    /* ... */
}
.content.callout {
    /* ... */
}
```

Note: difference between .content .callout and .content.callout

  * .content .callout
    * looks for callout inside content
  * .content.callout
    * looks for element that has both classes

Selectors can also be added before the & reference.

Example:

```scss
.sidebar {
    float: right;
    width: 300px;
    .users & {
        width: 400px;
    }
}
```

<br />

**Nesting properties**

Certain properties with matching namespaces are nestable.

Example:

```scss
.btn {
    text: {
        decoration: underline;
        transform: lowercase;
    }
}
```

compiles to:

```css
.btn {
    text-decoration: underline;
    text-transform: lowercase;
}
```

Nesting is easy, but dangerous. Do not nest unnecessarily.

Try limiting your nesting to 3 or 4 levels and consider refactoring anything deeper.

<br />

**Variables**

Native CSS variable support is still in its infancy, but Sass affords us a way to set reusable values.

Variable names begin with $.

```scss
$base: #fff;

p {
    color: $base;
}
```

!default can be used to provide a default value if a value isn't defined elsewhere.

Example:

application.scss

```scss
$rounded: 5px;

@import "buttons";
```

_buttons.scss

```scss
$rounded: 3px !default;

.btn {
    border-radius: $rounded;
}
```

If there is no var rounded in our application.scss, we provide a default value of 3px.

Types:

  * Booleans
    * true, false
  * Numbers - can be set with or without units
    * 4px, 1.5, ...
  * Colors
    * purple, rgba(0, 255, 0, 0.5), #fff
  * Strings - can be set with or without quotes
    * 'Helvetica Neue', Arial, "Loading..."
  * Lists - comma seperated or spaces
    * $authors: nick, dan, drew;
    * $margin: 40px 0 20px 100px;
  * Null
    * $shadow: null;

Use variable into selectors, propert names, and strings.

Example:

```scss
$side: top;

sup {
    position: relative;
    #{$side}: -0.5em;
}
.callout-#{$side} {
    background: #333;
}
```

<br />

**Lists**

  * length - number of items in a list
    * length($authors)
  * append - adds a value to the end of a list
    * append($authors, jos)
  * join - combines two lists together
    * join($authors1, $authors2)
  * index - returns a value's list position or false
    * index($authors, jos)
  * nth - return the item at list position n
    * nth($authors, 3)
  * zip - combines lists in comma-separated pairs
    * zip($authors, $co-authors)

Note: lists are 1-based, not zero-based.

<br />

**Mixin**

Blocks of reusable code that take optional arguments.

```scss
@mixin box-sizing($x: border-box) { (we set border-box as default)
    -webkit-box-sizing: $x;
    -moz-box-sizing: $x;
    box-sizing: $x;
}
.btn-a {
    @include box-sizing;
}
.btn-b {
    @include box-sizing(content-box);
}
```

Tip: be careful with mixins. There may be no repeating blocks of code in your Sass, but they might leak to your CSS. Try to prevent this.

Multiple arguments:

You must pass all the needed variables unless you provided a default argument. Then this argument becomes optional. Optional vars have to be set at the end of our chain of arguments.

If you use keyword arguments, you're allowed to pass them in any order.

```scss
@mixin button($radius, $color: #000)

@include button($color: #fff, $radius: 5px);
```

Passing valid, comma-separated CSS as a single value.

We can do this by adding ... to an argument. This creates a variable argument (vararg).

```scss
@mixin transition($val...)

@include transition(color 0.3s ease-in, background 0.5s ease-out);
```

Variable arguments in reverse:

```scss
@mixin button($radius, $color) {
    border-radius: $radius;
    color: $color;
}

$properties: 4px, #000;

.btn-a {
    @include button($properties...);
}
```

<br />

**Extend**

Sass will track and automatically combine selectors for us.

```scss
.btn-a {
    background: #777;
    border: 1px solid #ccc;
    font-size: 1em;
    text-transform: uppercase;
}
.btn-b {
    @extend .btn-a;
    background: #ff0;
}
```

compiles to:

```css
.btn-a, btn-b {
    background: #777;
    border: 1px solid #ccc;
    font-size: 1em;
    text-transform: uppercase;
}
.btn-b {
    background: #ff0;
}
```

Note: nested selectors will be added to.

Pitfalls:

  * Since .btn-b extends .btn-a, every instance that modifies .btn-a also modifies .btn-b.
  * Stylesheet bloat, if these extra styles aren't needed
  * We can counteract with placeholder selectors

<br />

**Placeholder selectors**

Are denoted with a %. They can be extended, but never become a selector of their own.

```scss
%btn {
    background: #777;
    ...
}
.btn-a {
    @extend %btn;
}
.btn-b {
    @extend %btn;
    background: #ff0;
}
.sidebar .btn-a {
    text-transform: lowercase;
}
```

.btn-b is no longer scoped in the last selector.

Tip: Versions of IE prior to 9 have a limit of 4095 selectors-per-CSS file limit.

<br />

**Directive**

Functions

```scss
@function fluidize($target, $context) {
    @return ($target / $context) * 100%;
}
.sidebar {
    width: fluidize(350px, 1000px);
}
```

Function arguments = same rules as mixin arguments.

Using @if, we can conditionally output code.

@else provides a fallback if everything evaluates false or null.

@else if allows for multiple comparisons.

Comparisons:

  * ==
  * !=
  * > *
  * >= *
  * < *
  * <= *

    * numbers only

@each directive allows us to loop through each list item.

@each $author in $authors { }

Example:

```scss
$tools: socket, wrench, bolt;

@each $tool in $tools {
    .tool-#{$tool} {
        background: url('#{$tool}.png') no-repeat;
    }
}
```

@for loop

```scss
@for $i from 1 through 3 { }
```

@while loop

```scss
$i: 1;

.something {
    @while $i < 4 {
        $i: $i + 1; 
    }
}
```

Example:

```scss
@mixin button($color, $rounded: false) {
    color: $color;
    @if $rounded {
        border-radius: $rounded;
    }
}
.btn-a {
    @include button(#000);
}
.btn-b {
    @include button(#333, 4px);
}
```

* * *

When to use:

  * Mixins
    * Similar sets of properties used multiple times with small variations
  * Extend
    * Sets of properties that match exactly
  * Functions
    * Commonly-used operations to determine values

* * *

<br />

**Number Operations**

  * \+ addition
  * \- subtraction
  *     * multiplication
  * / division
    * The trickiest of the number operations, due to font:
      * font: normal 2em/1.5 Helvetica, sans-serif.
    * Triggering division:
      * variable involved - $size / 10
      * parenthesis - (100px / 20)
      * Another arithmetic operation - 20px * 5 /2
  * % modulo

Tip: Sass defaults to returning (up to) five digits after a decimal point.

<br />

**Pre-defined math utilities**

  * round($number) - round to closest whole number
  * ceil($number) - round up
  * floor($number) - round down
  * abs($number) - absolute value
  * min($list) - minimum list value
  * max($list) - maximum list value
  * percentage($number) - convert to percentage
    * Tip: can be used for our fluid calculation (see Mobile). > percentage(target / context);

<br />

**Color**

  * Easier recall through variables
  * Faster representation using shorthand
  * Simplified alternation via color utility functions
    * addition
      * $color-base + #112233;
    * subtraction
      * $color-base - #112233;
    * multiplication
      * $color-base * 2;
    * division
      * $color-base / 2;

Tip: where possible, use color utility functions instead of color arithmetic: easier to predict and maintain.

Shortcuts:

  * rgba($color, 0.8);
  * rgba(#000, 0.8);

Functions:

  * lighten
    * color: lighten($color, 20%);
  * darken
    * color: darken($color, 20%);
  * saturate
    * color: saturate($color, 20%);
  * desaturate
    * color: desaturate($color, 20%);
  * mix
    * color: mix(#ffff00, #107fc9);
    * color: mix(#ffff00, #107fc9, 30%); --> amount of first color
  * grayscale
    * color: grayscale($color);
  * invert
    * color: invert($color);
  * complement
    * color: complement($color);
  * And many more...

lighten and darken adjustments are linear.

color: lighten(#eee, 7%) will output to color: white;

The scale_color function changes one or more color aspects relative to the start value.

color: scale_color(#eee, $lightness: 7%) will output to color: #efefef

Keywords:

  * $red
  * $green
  * $blue
  * $saturation
  * $lightness
  * $alpha

<br />

**Responsive**

Example for media queries:

```scss
@mixin respond-to($val, $query) {
    @media ($val: $query) {
        @content;
    }
}
.sidebar {
    @include respond-to(max-width, 600px) {
        float: right;
        width: 30%;
    }
}
```

Responsive pitfalls

  * declarations outside @media cannot be extended inside
    * @media(min-width: 700px) { @extend .sidebar; } does not work!
    * extending something in the same media query is ok
  * Matching media queries are not combined
    * Sometimes, manual combination is best

* * *

<br />

**Indented syntax**

Indented syntax (.sass) relies on whitespace to simplify.

```sass
.content
    border: 1px solid #ccc
    padding: 20px
    h2
        font-size: 3em
```

Mixin declaration

```sass
=box-sizing($x)
    -webkit-box-sizing: $x
    -moz-box-sizing: $x
    box-sizing: $x
.content
    +box-sizing(border-box)
```

Single-line if

if(condition, "true value", "false value")

Example: background: if($theme == dark, #000, #fff)
