# Built in accessibility features when using native HTML elements

This is a list of built in accessibility features of html elements in browsers.

This is not to discourage making anything custom, but a good list for things to consider for any custom implementations.

I don't know all of this by heart and research takes time. Please send in suggestions. What is this list missing?

## General

- If styling fails for whatever reason, these elements have some base styles, so content is still readable if the markup is good.
- If scripts fail for whatever reason, links and regular forms will still work without any scripts.

## Elements

## `<html`>

Not necessarily related to the html element itself, but to how a browser handles web pages.

- When you navigate to a page, focus gets set to the beginning of the page
- When you go back, scroll position gets set back to where it was.
- In some browsers, the text you have input to input elements gets preserved when you go back. (verify this)

## `<title`>

- Gets announced when you navigate to a page.

## `<a>`

- Focusable [1]
- Gets announced as a link by screen readers
- You can open links to a new window or tab. (most browsers)
- You can see the url you're about to go to. (most desktop browsers)

## `<button>`

- Focusable [1]
- Gets announced as a button by screen readers
- Click event gets triggered when the user interacts with the element, even if via keyboard or screen reader. Pointing device doesn't matter.

## `<form>`

- Shift+enter on desktop opens a new window and submits the form there. If focus is on the submit button in the original form, shift+enter also triggers a click event on the button, but not a submit event on the form. Not necessarily an accessibility feature, but native built in behaviour still.
- Screen readers have a form mode when focused inside a form to help interact with forms
- You can submit a form with the enter key if focus is in an input.
- Easy event handling. You can listen to the submit event to react to any way the user submits the form. (Pressing enter submits the form. Submit button click event triggers form submit event. No need for click or keydown handlers.)


## `<label>`

- When you associate a label with an input (input, select, textarea) element, the label gets announced by screen readers.
- Increased click area. When you click on the label, focus moves to the associated input element.

## `<input>, <select>, <textarea>`

- Focusable [1]
- Screen reader users can get a list of all form elements
- Type attribute can give you additional features, like a specific keyboard or a different way to select input content.

## `<h1>, <h2>, ...`

- Screen reader users can navigate a page by headings.

## `<table>`

## `<img>`

- Alt attribute gets announced by screen readers [2]

---------



## Why it matters

1. Anyone using a screen reader, keyboard or anything else without a pointer (like a mouse or a finger) can understand where on the page they are at.
2. Visually impaired users can get a better understanding of content with good alt attributes.
