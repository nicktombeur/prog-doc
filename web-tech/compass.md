**Links**

  * [Help & Documentation](http://compass-style.org/help/)

Open-source CSS Authoring Framework.

Adds reusable patterns, utilities, and modules like vertical rhythm and spriting.

Comprises five main modules:

  * utilities
  * typography
  * CSS3
  * layout
  * reset

<br />

**Importing**

Use @import to make Compass available:

```sass
@import "compass" (utilities, typography, CSS3)
@import "compass/layout"
@import "compass/reset"
```

Tip: easiest to import them in your main Sass file. Unless you want to restrict which features are available.

Importing reset:

  * Only module that adds CSS code into your code.
  * Not ideal in production: unable to make tweaks to fit your site's specific needs.
  * Avoid if you plan on using Normalize.css
  * Can be used for quick examples and non-production versions

Compass provides mixins for CSS3 prefix properties, like -webkit, -moz, ...

```sass
@import "compass"

.content
    +box-sizing(border-box)
```

Check the browsers you intend to support to see if providing prefixes is still necessary.

There's a ton of helpers and utilities in Compass, but not everything is optimal or current.

Always be aware of the output!

<br />

**Helpers**

  * image-url and font-url are available post-configuration
    * background: image-url('bg-body.png') --> background: url('images/bg-body.png');
  * scale-lightness shortcuts our scale_color use
    * color: scale-lightness(#eee, 7%)
    * Tip: use a negative value to darken
  * scale-saturation also shortcuts scale_color
    * color: scale-saturation(#eee, 30%)
  * Opposite-position returns the opposite side (or pair)
    * opposite-position(top)
    * opposite-position(right bottom)
  * ...

<br />

**Utilities**

Contrast color returns a light or dark color based on an input color's lightness

contrast-color(input-color, dark-color, light-color, threshold)

Stretch outputs positioning for each side of a container

+stretch(top, right, bottom, left)

Image dimensions

height: image-height('a.png')

width: image-width('a.png')

Use inline-image to base64 embed images into CSS.

It embeds the image into CSS (no more loading flash).

~10% image size increase, but reduces HTTP request.

IE8+ (max 32KB), good mobile support

background: inline-image('a.png')

<br />

**Rythm**

<br />

Vertical (baseline grids)

Adds a baseline grid and allows it to manage spacing, line heights, and margins.

Begin with defining global variables and establish-baseline

```sass
@import "compass"

$base-font-size: 18px
$base-line-height: 30px
+establish-baseline
```

Change font size without disrupting the grid.

```sass
+adjust-font-size-to(50px)
```

Adjust the amount of vertical space occupied (line-height).

```sass
+adjust-leading-to(2)
```

Important: Rhythm mixins need to be notified of font size adjustments

```sass
blockquote
    +adjust-font-size-to(20px)
    +adjust-leading-to(2, 20px)
```

Add margin.

```sass
p
    +leader(1)
    +trailer(1)
h1
    +adjust-font-size-to(50px)
    +trailer(2, 50px)
```

Add padding.

```sass
h1
    +padding-leader(1)
    +padding-trailer(1)
```

Add border.

```sass
h1
    +trailing-border(<border-width>, <units-of-padding>, <font-size*>)
    +leading-border(<border-width>, <units-of-padding>, <font-size*>)
    +rhythm-borders(<border-width>, <units-of-padding>, <font-size*>)
```

Use Vertical Rhythm carefully, misuse or overuse can cause bloat.

Baseline grids are difficult to maintain (images, ...).

<br />

**Sprite**

Make sure you're using the appropriate solution: sprites, icon fonts or embedded images.

Automatic

```sass
@import "compass"
@import "icons/*.png"  <-- grabs all .png files in the icons folder
+all-icons-sprites  <-- icons = folder your images are in
```

Downside:

  * Lots of images = lots of selectors
  * Manual width/height setting needed

Manual

```sass
@import "compass"
$icons: sprite-map("icons/*.png")

i
    background: $icons
    display: inline-block

@each $i in sprite_names($icons)
    .icn-#{$i}
        background-position: sprite-position($icons, $i)
        +sprite-dimensions($icons, $i)
```
