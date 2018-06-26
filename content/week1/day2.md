---
title: "Day 2: Git and The DOM"
weight: 2
---

<date>Tuesday, June 26, 2018</date>

## Lecture Videos

Morning:

* [Playlist](https://www.youtube.com/playlist?list=PLuT2TqJuwaY8afDn9R0pVYZd9HzhsaP5V) | [Day 2, part 1](https://www.youtube.com/watch?v=1-CvNYMy_hY&index=9&list=PLuT2TqJuwaY8afDn9R0pVYZd9HzhsaP5V&t=0s)

Afternoon:

* [Playlist](https://www.youtube.com/watch?v=czNa5ix1vFs&list=PLuT2TqJuwaY-b1gN7b0NmF3GQ9_KHCxYG) | [Day 2, part 1]()

## Topics

### Git

* [Git Guide](http://rogerdudler.github.io/git-guide/)
* [Git Basics](https://git-scm.com/book/en/v2/Getting-Started-Git-Basics)
* [Understanding Git (part 1): Explain It Like I'm Five] (https://hackernoon.com/understanding-git-fcffd87c15a3)

<div class="img github-flow"></div>

### DOM

* Basic DOM manipulation
  * `document.querySelector`/`document.querySelectorAll` - [MDN Docs](https://developer.mozilla.org/en-US/docs/Web/API/Document/querySelector)
  * `.textContent` - [MDN Docs](https://developer.mozilla.org/en-US/docs/Web/API/Node/textContent)
  * `.innerHTML` - [MDN Docs](https://developer.mozilla.org/en-US/docs/Web/API/Element/innerHTML)
* Developer console
  * `console.log`
  * `debugger` - [W3Schools docs](https://www.w3schools.com/js/js_debugging.asp)
* Basic [event](https://www.w3schools.com/js/js_events.asp) handling
  * [Events in JavaScript](https://www.kirupa.com/html5/javascript_events.htm) - blog post with more detail than we discussed in class
  * `.addEventListener()` - [MDN docs](https://developer.mozilla.org/en-US/docs/Web/API/EventTarget/addEventListener)
  * `.preventDefault()` - [MDN Docs](https://developer.mozilla.org/en-US/docs/Web/API/Event/preventDefault)
  * `.target` - [MDN Docs](https://developer.mozilla.org/en-US/docs/Web/API/Event/target)

### Other Topics

* [Template literals](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Template_literals)
* [Google Fonts](https://fonts.google.com/)

## Examples

#### Template literals

Template literals are string literals that allow embedded JavaScript expressions. Surround the string literal with \`\` (backticks), and use the variable placeholders inside `${ }` (a dollar sign and curly braces), and they will be replaced with their respective values.

{{< code js >}}
const name = 'Dana'
const hometown = 'Youngstown, OH'

console.log(`Hello, I'm ${name}. I'm from ${hometown}.`)   // "Hello, I'm Dana. I'm from Youngstown, OH."
{{< /code >}}

#### Google Fonts

Google has a catalog of web fonts that you can use in your projects. You can import the font in your `index.css` file like the code below from _Chrismess_.

{{< code css >}}
@import url('https://fonts.googleapis.com/css?family=Lato');

body {
  font-family: 'Lato', Helvetica, Arial, sans-serif;
}
{{< /code >}}

## Presentations

* <a target="_blank" href="/day02.pdf">Review: JavaScript Elements and Attributes</a>

## Projects

### Chrismess
[Morning](https://github.com/xtbc18s3/chrismess) | [Afternoon](https://github.com/xtbc18s3/chrismess/tree/afternoon)

## Homework

* Give the function `changeHeading` a more accurate name.
* Add a second field to the form.
* Display the value of that field in the list.

## Bonus Credit

* Display the second field in a separate HTML element than the flick name. For example:

```html
<li>
  <span class="flickName">Jurassic Work</span>
  <span class="year">2015</span>
</li>
```

* See if you can then style each field differently.

## Super Mega Bonus Credit

* Use more than one function. (Break `changeHeading` into multiple functions, as appropriate.)
