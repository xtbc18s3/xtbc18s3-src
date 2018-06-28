---
title: "Day 4: Vanilla JS, localStorage, and Deployment"
weight: 4
---

<date>Thursday, June 28, 2018</date>

## Lecture Videos

Morning:

* [Playlist](https://www.youtube.com/playlist?list=PLuT2TqJuwaY8afDn9R0pVYZd9HzhsaP5V) | [Day 4, part 1](https://www.youtube.com/watch?v=UwG60JJOnXU&list=PLuT2TqJuwaY8afDn9R0pVYZd9HzhsaP5V&index=37)

Afternoon:

* [Playlist](https://www.youtube.com/watch?v=czNa5ix1vFs&list=PLuT2TqJuwaY-b1gN7b0NmF3GQ9_KHCxYG) | [Day 4, part 1](https://www.youtube.com/watch?v=xzZf4sgpDgY&list=PLuT2TqJuwaY-b1gN7b0NmF3GQ9_KHCxYG&index=37)

## Topics
* [`this`](https://medium.com/tech-tajawal/javascript-this-4-rules-7354abdb274c)
* [.indexOf( )](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/indexOf), [.splice( )](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/splice), [.filter( )](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/filter), [.closest( )](https://developer.mozilla.org/en-US/docs/Web/API/Element/closest)
* Polyfills
  * [Definition from MDN](https://developer.mozilla.org/en-US/docs/Glossary/Polyfill)
  * [What is a Polyfill?](https://remysharp.com/2010/10/08/what-is-a-polyfill)
* CSS: [Font Awesome](https://fontawesome.com/), [transform](https://css-tricks.com/almanac/properties/t/transform/), [transition](https://css-tricks.com/almanac/properties/t/transition/)

### localStorage
* [Using `localStorage`](https://www.smashingmagazine.com/2010/10/local-storage-and-how-to-use-it/)
* `JSON.stringify`
  * [Using `JSON.stringify`](http://www.dyn-web.com/tutorials/php-js/json/stringify.php)
  * [API reference](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/JSON/stringify), including optional arguments for whitelisting properties and transforming the data as it's stringified
* `JSON.parse`
  * [Using `JSON.parse`](http://www.dyn-web.com/tutorials/php-js/json/parse.php)
  * [MDN Docs](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/JSON/parse)

### Deploying to GitHub Pages
* [GitHub Pages](https://pages.github.com/)
* [What is GitHub Pages?](https://help.github.com/articles/what-is-github-pages/)

## Examples

### localStorage

`localStorage` is storage in your web browser that conforms to Web Storage API. It is scoped by domain, meaning other websites cannot access data stored by your website and vice versa. The data in `localStorage` persists in the browser until removed, even if the browser is closed and re-opened.

To set an item, use `localStorage.setItem`, and retrieve data using `localStorage.getItem`. It is important to remember that values stored will always be strings, so it may be use necessary to use the `JSON.stringify` and `JSON.parse` methods to set and retrieve non-string data.  JSON stands for **J**ava**S**cript **O**bject **N**otation.  To learn more about JSON, click [here](https://www.w3schools.com/js/js_json_intro.asp).

{{< code js >}}
const myObject = {
  thisIsCool: true
}

localStorage.setItem('myObject', myObject)
localStorage.getItem('myObject') // => "[object Object]"
// localStorage saves the result of the implicit myObject.toString() call

localStorage.setItem('myObject', JSON.stringify(myObject))
// calling JSON.stringify converts the object to a JSON string representation
// so it can be stored in localStorage without loss of data

const retrievedObject = localStorage.getItem('myObject') // => "{"thisIsCool":true}"
JSON.parse(retrievedObject) // => {thisIsCool: true}
// JSON.parse converts the retrieved JSON string back into a JavaScript object
{{< /code >}}

## Projects

### Chrismess
[Morning](https://github.com/xtbc18s3/chrismess) | [Afternoon](https://github.com/xtbc18s3/chrismess/tree/afternoon)

## Homework

* Try the official [React Tutorial](https://reactjs.org/tutorial/tutorial.html)

### Super Mega Bonus Credit

* Have a great weekend!
