#Web Frameworks

## Angular

- Two-way data binding via dirty checking (which makes it slower than others).  --> ineffecient
- Unopinionated. You can achieve the same thing in a lot of different ways. Which can make bad code.
- Rapid prototyping.
- Directives are a powerful way to influence the DOM.
- Most testable.

## Ember

- Two-way data binding via accessor methods on objects. --> effecient
- Ember shines in teams. It's hard to write bad code.
- Verbose.
- Convention over configuration.
- Rapid prototyping.
- Computed properties. You can create properties thate are dependent on other properties.

## Backbone

- Two-way data binding like Ember but you have to do all the wiring yourself.
- Unopinionated. You can achieve the same thing in a lot of different ways. Which can make bad code.
- Easily extensible.
- Easy interacting with RESTful APIs.
- Tons of libraries.
- Great for large applications.

## React

- Two-way data binding like Backbone but it's easier with the provided helpers.
- Not MVC, self-described as the V in MVC. Pairs nicely with Backbone or other frameworks.
- Updates the page by constructing a virtual DOM and diffing it with the actual DOM. This makes it the most performant of the four in re-paints.
- Much like web components.
- Functional programming.
- Server-side rendering.
