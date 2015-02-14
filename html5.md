
Useful links:

  * [MDN (Mozilla Developer Network)](https://developer.mozilla.org/en-US/docs/Web/HTML)
  * [Can I use ____ ?](http://caniuse.com/)

<br />

Traditionally presentational tags, the i, b, em and strong tags have been given new semantic meanings.

HTML4
  * **i tag** rendered an **italic** font style
  * **b tag** rendered a **bold** font style
  * **em tag** meant **emphasis**
  * **strong tag** meant **strong emphasis**

HTML5

**i tag** represents text in an **"alternative voice"** or **"mood"**

```html
<p><i>I hope this works</i>, he thought.</p>
```

**b tag** represents **"stylistically offset"** text

```html
<p><b class="lead">The event takes place this upcoming Saturday, and over 3,000 people have already registered.</b></p>
```

**em tag** now means **"stress emphasis"**

```html
<p>Make sure to sign up <em>before</em> the day of the event, September 16, 2013.</p>
```

**strong tag** now means **"strong importance"**

```html
<p>Make sure to sign up <em>before</em> the day of the event, <strong>September 16, 2013</strong>.</p>
```

**Script tag**

No type attribute needed.

```html
<script src="file.js"></script>
```

**Link tag**

Same as script tag, no type needed.

```html
<link rel="stylesheet" href="file.css">
```

* * *

**HTML5 Elements**

**Section**

Represents a generic document or application section.

Section vs. div

  * A div has no semantic meaning, but the section element does. It's used for grouping together thematically related content.

Ask yourself, "Is all of the content related?". If the answer is yes, you can use section.

**Header**

A group of introductory or navigational aids.

  * There can be many different headers on a page.
  * Usually appears at the top of a document or section, but is defined by its content rather than its position

HTML4

```html
<div class="header">
    <!-- ... -->
</div>
```

HTML5

```html
<header>
    <!-- ... -->
</header>
```

**Footer**

The footer element represents a footer for its nearest ancestor sectioning content or sectioning root element.

Like the header, the footer element is not position-dependent. It should describe the content it is contained within.

HTML4

```html
<div class="footer">
    <!-- ... -->
</div>
```

HTML5

```html
<footer>
    <!-- ... -->
</footer>
```

**Aside**

An aside element is appropriate when it is used to represent content that is not the primary focus of an article or page, but it is still related to the article or page.

  * When used within an article element, the aside contents should be related to that particular article it is contained within.
  * When used outside an article element, the aside contents should be specifically related to the site.

In short: aside is a sidebar.

HTML4

```html
<div class="sidebar">
    <!-- ... -->
</div>
```

HTML5

```html
<aside>
    <!-- ... -->
</aside>
```

Example using aside within a section:

```html
<section>
    <header>
        <h1>The heading of the section</h1>
        <p>This is content in the header.</p>
    </header>
    <p>This is some information within the section.</p>
    <aside>
        <p>Some secondary information.</p>
    </aside>
    <footer>
        <p>By "Author Name"</p>
    </footer>
</section>
```

**Nav**

The nav element represents a section of a page that links to other pages or to parts within the page: a section with navigation links.

HTML4

```html
<ul class="nav">
    <li>...</li>
</ul>
```

HTML5

```html
<nav>
    <ul>
        <li>...</li>
    </ul>
</nav>
```

**Article**

The article element represents a complete, or self-contained, composition in a document, page, application, or site and that is, in principle, independently distributable or reusable, e.g. in syndication.

The article element is another type of section. It is used for self-contained related content.

Determining if a particular piece of content is "self-contained":

  * Ask yourself if you would syndicate the content in an RSS or Atom feed.

Example uses:

  * A blog post
  * A news story
  * A comment on a post
  * A review

HTML4

```html
<div class="article">
    <!-- ... -->
</div>
```

HTML5

```html
<article>
    <!-- ... -->
</article>
```

**Main**

The main element represents the main content of the body of a document or application.

Don't:

  * include more than one main element in a document
  * include the main element inside of an article, aside, footer, header, or nav element

HTML4

```html
<div class="main">
    <!-- ... -->
</div>
```

HTML5

```html
<main>
    <!-- ... -->
</main>
```

**Figure/figcaption**

A common use of the figure tag is for an image within an article:

```html
<figure>
    <img src="image.jpg" alt="My Picture" />
    <figcaption>This is a caption for the picture.</figcaption>
</figure>
```

**Time**

The datetime attribute represent the machine-readable date/time of the <.time> element.

Example usage:

```html
<time>2013-09-16</time>
```

We use the datetime attribute to get our desired format:

```html
<time datetime="2013-09-16">09/16/2013</time>
```

* * *

**HTML5 Forms**

**New input types**

If a browser doesn't support the input type, it defaults to "text".

**Search**

```html
<input type="search" />
```

**Email/URL/tel**

Looks just like a regular text input, but with added usability on mobile devices.

```html
<input type="email" />

<input type="url" />

<input type="tel" />
```

**Date**

Shows a date-picker.

```html
<input type="date" />
```

**Number**

Shows increase/decrease-button.

```html
<input type="number" />
```

**Range**

Shows a slider to change value.

```html
<input type="range" />
```

**Month/Week**

Show date-picker to select month/week.

```html
<input type="month" />

<input type="week" />
```

**Time/Datetime-local**

Show increase/decrease-button to select time/datetime-local.

```html
<input type="time" />

<input type="datetime-local" />
```

**Color**

Button to show color-picker.

```html
<input type="color" />
```

**New form elements**

**Datalist**

Represents a set of option elements that represent predefined options for other controls.

Looks like normal text but gives auto-complete suggestions.

```html
<input type="text" list="browsers" />
<datalist id="browsers">
    <option value="Chrome">
    <option value="Firefox">
    <option value="Internet Explorer">
    <option value="Opera">
    <option value="Safari">
</datalist>
```

**Keygen**

Specifies a key-pair generator field used for forms.

When the form is submitted, the private key is stored locally, and the public key is sent to the server.

```html
<keygen name="security">
```

[More information.](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/keygen)

IE not supported !

**Output**

Represents the result of a calculation or user action.

```html
<form oninput="result.value=parseInt(a.value)+parseInt(b.value)">
    <input type="range" name="b" value="50" /> +
    <input type="number" name="a" value="10" /> =
    <output name="result"><./.output>
</form>```

IE not supported !

**New form attributes**

**Placeholder**

Allows you to specify a message that is shown inside the input, hidden when user starts typing, and returns when focus is lost on the input (when input is blank).

```html
<input type="text" placeholder="Enter your email ..." />
```

**Autofocus**

Automatically focus the specified input when the page is rendered.

```html
<input type="text" autofocus />
```

**Autocomplete**

Automatically complete values based on values that the user had entered before.

It is possible to have autocomplete "on" for the form, and "off" for specific input fields.

Works with form, text, search, url, tel, email, password, datepickers, range, and color.

```html
<input type="text" name="email" autocomplete="on">
```

**Required**

When the form is submitted, the user will be notified of an error if the field is left blank.

```html
<input type="text" required />
```

**Pattern**

Accepts a JavaScript regular expression that can be used to validate a form field to match the pattern.

```html
<input type="text" pattern="[0-9]{3}" />
```

**List**

See form element: datalist.

**Multiple**

It specifies that the user is allowed to enter more than one value in the input-element.

Works with the following input types: email, and file.

```html
<input type="file" name="img" multiple>
```

**novalidate**

Specifies that the form-data (input) should not be validated when submitted.

```html
<form novalidate><./.form>
```

**formnovalidate**

Specifies that the input-element should not be validated when submitted.

The formvalidate attribute overrides the novalidate attribute of the form-element.

```html
<input formnovalidate>
```

**form**

Specifies one or more forms an input-element belongs to.

Use a space-separated list of form ids.

```html
<form id="form1">
    <!-- ... -->
</form>

<input type="text" form="form1">
```

**formaction**

Specifies the URL that will process the input control when the form is submitted.

The formaction attribute overrides the action attribute of the form-element.

Can be used with submit and image.

```html
<form action="URL1">
    <input type="submit">
    <input type="submit" formaction="URL2">
</form>
```

**formenctype**

Specifies how the form-data should be encoded when submitting it to the server (only for forms with method="post").

Overrides the enctype attribute of the form-element.

Can be used with submit and image.

```html
<input type="submit" formenctype="multipart/form-data">
```

**formmethod**

Defines the HTTP method for sending form-data to the action URL.

Overrides the method attribute of the form-element.

Can be used with submit and image.

```html
<input type="submit" formmethod="post" formaction="URL">
```

**formtarget**

Specifies a name or a keyword that indicates where to display the response that is received after submitting the form.

Overrides the target attribute of the form-element.

Can be used with submit and image.

```html
<input type="submit" formtarget="_blank">
```
