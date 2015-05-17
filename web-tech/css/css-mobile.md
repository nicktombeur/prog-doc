**Fluid layouts**

Don't use pixels but ems. We don't want to same size on every screen.

em

Relative to the font-size of the element (2em means 2 times the size of current font)

<br />

Default browser font-size should be around 16px. Therefore we set our default font-size to 16px;

```css
html {
    font-size: 16px;
}
```

<br />

1em is now equal to 16px. To make things easier we take 62.5% of 16 which is 10.

```css
body {
    font-size: 62.5%; /* 1em = 10px */
}
```

<br />

Now we can calculate our em as followed:

target font size / font size of containing element = result

e.g. 30px (for h1) / 10px (default font) = 3em

Note: no need to round up the numbers, keep the values_

<br />

Same calculation can be used for width, but since we use percentage we have to move 2 digits to the right.

e.g. 305px / 940px = 0.32446809 --> width: 32.446809%;

For flexible padding, we can also use the same calculation but we use the box-element as our context.

<br />

Downside of fluid layouts --> limitations with viewport size.

Tool for calculation: [flexible math](http://responsv.com/flexible-math/).

<br />

**Media queries**

```css
@media screen and (max-width: 320px) {
    body {
        font-size: 100%;
    }
}
```

Meaning: for any viewport <= 320px width, use these styles over our original styles.

Note: also possible to use min-width.

Best practice: place your media queries in group at the bottom of your stylesheet file.

<br />

If you use fluid layouts you only have to write 1 media query (the biggest size) for smartphones, because the site will scale.

Portrait

```css
@media screen and (orientation:portrait) { 
}
```

<br />

Landscape

```css
@media screen and (orientation: landscape) {
}
```

<br />

Examples: [mediaqueri.es](http://mediaqueri.es/)

**Adaptive design**

Adapt to the screen size of the devices.

Viewport defines break points.

<br />

**Responsive design**

Content defines break points.

For instance:

We notice our site gets a little cramped at a certain width (i.e. 870px), this is our first breakpoint that we're going to optimize (with media queries).

<br />

**Responsive images**

Create an image bigger than needed. This way we can scale it down.

```css
img {
    max-width: 100%;
}
about img {
    width: 29.6875%;
}
```

This can be done with any media-type.

```css
img, embed, object, video {
    max-width: 100%;
}
```

<br />

**Retina images**

= 1.5x - 2x the pixel density

```css
@media
only screen and (-webkit-min-device-pixel-ratio: 1.5),
only screen and (min-device-pixel-ratio: 1.5) {
    .logo {
        background-image: url(logo@2x.png);
        -webkit-background-size: 200px 200px;
        background-size: 200px 200px;
    }
}
```

We have to set the background-size equal to the size of the original image.

logo.png (200px) --> logo@2x.png (400px)

If you're worried about file size and loading all these files, take a look at [picturefill.js](https://github.com/scottjehl/picturefill).
