# Built in user facing features of html elements in browsers

Some discussion on what you get for free by using native html elements. All these behaviours may not be common or even always necessary and implementations vary between browsers and platforms. This is mostly good base knowledge to know before doing anything custom.

I've focused mainly on elements that directly affect user interaction. Many points concern only screen readers on the surface, but using native elements ensures that pages are better machine readable too. There may be a lot of different ways these elements are meaningful, like for SEO or performance, but I'm focusing on user interactions and accessibility here.

The focus is also more on the current state of affairs in browsers, not the ideal situation according to specs.

This article is not made to discourage you making custom implementations. It is is more a list of considerations that you might want to keep in mind and to help show what you can get from native elements. Some of these features you might even want to enhance or replace in your own custom implementations.

I don't know all of this by heart and research takes time. Please send in suggestions. What do you think is missing?

## Sources

- The categorization is the same as in [MDN web docs](https://developer.mozilla.org/en-US/docs/Web/HTML/Element).
- [HTML elements Screen reader compatibility](https://www.powermapper.com/tests/screen-readers/elements/)
- [Designing for Screen Reader Compatibility](https://webaim.org/techniques/screenreader)

## General

- If styling fails for whatever reason, native elements have some base styles provided by the browser, so well made markup will usually still produce an understandable web page for users even without any styles.
- If scripts fail for whatever reason, links and regular forms will still work without any scripts.

## Main root

### `<html>`

You can set the page language with the `lang` attribute. This will let browsers, search engines and screen readers know what language a page is to be in without any detective work on their part.

You can use the lang attribute on any element, if your page includes content in many languages.

[Using the HTML lang attribute](https://developer.paciellogroup.com/blog/2016/06/using-the-html-lang-attribute/)

Some more notes that are not necessarily related to the html element itself, but to how a browser handles whole web pages.

- When you navigate to a page, focus gets set to the beginning of the page
- When you go back, scroll position gets set back to where it was.
- In some browsers, the text you have input to input elements gets preserved when you go back. (verify this)

If you have a JavaScript front end app, you should take these into account when displaying new pages. In some cases it may not be needed to have these behaviours and in some cases you might have better state preservation with a front end app.

A normal web page has many consistent default behaviours, like scrolling one viewport length with the spacebar in desktop browsers. When implementing custom actions (keyboard shorcuts, gestures) test your site with your target browsers and platforms with and without your custom implementation so that if you overwrite any default behaviours, it's intentional.

## Document metadata

### `<base>`

The HTML `<base>` element specifies the base URL to use for all relative URLs in a document. There can be only one `<base>` element in a document.

Set `target` attribute to define a browsing context to display the result when links or forms cause navigation, for `<a>` or `<form>` elements without an explicit target attribute. The attribute value targets a browsing context (such as a tab, window, or `<iframe>`). This applies to anchor links too.

```
<base href="https://www.example.com/">
<base target="_blank">
<base target="_top" href="https://example.com/">
```

For example, given `<base href="https://example.com">`

...and this link: `<a href="#anchor">Anker</a>`

...the link points to `https://example.com/#anchor`

### `<title>`

The HTML Title element (`<title>`) defines the document's title that is shown in a browser's title bar or a page's tab.

Gets announced by screen readers when you navigate to a new page. If you change pages in javascript without a full page reload, take care that you announce the new page to your users.

## Content sectioning

### `<header>`, `<main>`, `<section>`, `<nav>`, `<article>`, `<aside>`, `<footer>`

Screen readers support varies, but they include supported elements when navigating by landmark. This makes sense because the header, footer, nav, article, section and aside elements all Map to ARIA landmarks. These elemnents have an implicit role, so when navigating to them, screen readers announce them for what they are.

TODO: common page structure example.

### `<h1>`

Same applies to headings as other landmark elements. Screen reader users can navigate a page by headings. Even if you want to style headings in a custom way, make sure your page has a logical heading structure from h1 downwards.

Screen reader users often use the list of headings to navigate pages.

## Text content

### `<ul>`, `<ol>`, `<li>`, `<dl>`, `<dd>`, `<dt>`

List elements get announced as lists by screen readers and can be navigated.

### `<hr>`

Announced as a separator by screen readers.

## Inline text semantics

### `<a>`

- Focusable, so anyone using a screen reader, keyboard or anything else without a pointer (like a mouse or a finger) can understand where on the page they are at.
- Destination url is usually shown by browsers in some kind of preview
- You can open links to a new window or tab. (most browsers)
- You can see the url you're about to go to. (most desktop browsers)
- You can copy and share the url of a link
- Gets announced as a link by screen readers
- Screen reader users can get a list of links on the page an navigate by that
- Screen readers also announce if the link will open in a new window, desktop users usually get a hint about that too
- Search engines understand links, they don't understand plain clickable divs
- You can use the target attribute to get browsers to open links in new tabs
- Users can open links in new tabs with the mouse, finger, keyboard or screen reader

If you do anything custom with links, there's a lot to test on different platforms, so if you do something custom, be sure to at least be intentional if you override default functionality.

### `<sub>`, `<sup>`

Subscript₁ & superscript² text. Styled nicely by default.

## Image and multimedia

### `<video>`, `<track>`

Provide subtitles for video with the track element.

There's also the `<audio>`, but you can't add subtitle tracks to it directly.

### `<img>`

Screen readers will read an images `alt` attribute to users, so they can know what the image is about.

## Table content

## `<table>`, `<caption>`, `<thead>`, `<tbody>`, `<tfoot>`, `<tr>`, `<th>`, `<td>`

Tables have helpful navigation modes and announcements in assistive software.

`<caption>` can be used to give users a summary of what a table contains, both for visual and non-visual users.

## Forms

### `<form>`

- Screen readers have a form mode when focused inside a form to help interact with forms
- Easy event handling. You can listen to the submit event to react to any way the user submits the form. (Pressing enter submits the form. Submit button click event triggers form submit event. No need for click or keydown handlers.)
- You can submit a form with the enter key if focus is in an input.

- Special behaviours and shortcuts for power users. Like shift+enter on desktop opens a new window and submits the form there. If focus is on the submit button in the original form, shift+enter also triggers a click event on the button, but not a submit event on the form. Might be more of a strange legacy behaviour, but good to know still.

### `<button>`

- Focusable, so anyone using a screen reader, keyboard or anything else without a pointer (like a mouse or a finger) can understand where on the page they are at.
- Gets announced as a button by screen readers
- Click event gets triggered when the user interacts with the element, even if via keyboard or screen reader. Pointing device doesn't matter.

### `<fieldset>`, `<legend>`

Groups fields together both visually and for screen readers.

### `<label>`, `<input>, <select>, <textarea>`

- When you associate a label with an input (input, select, textarea) element, the label gets announced by screen readers.
- With labels you get increased click area. When you click on the label, focus moves to the associated input element.
- Focusable, so anyone using a screen reader, keyboard or anything else without a pointer (like a mouse or a finger) can understand where on the page they are at.
- Screen reader users can get a list of all form elements
- Type attribute can give you additional features, like a specific keyboard or a different way to select input content.
- Standard controls accross platforms, include a large number of conventions that you should follow and be careful not to override when doing custom impelementation
  - Text editing, selections, copy & paste etc etc.


## Interactive elements

### `<details>`, `<summary>`

You can use the details, summary element pair to make and expander without any styling of javascript.

