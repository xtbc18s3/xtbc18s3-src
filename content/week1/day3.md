---
title: "Day 3: DOM, Arrays and Objects"
weight: 3
---

<date>Wednesday, June 27, 2018</date>

## Lecture Videos

Morning:

* [Playlist](https://www.youtube.com/playlist?list=PLuT2TqJuwaY8afDn9R0pVYZd9HzhsaP5V) | [Day 3, part 1](https://www.youtube.com/watch?v=opAPsCrpPCs&index=28&t=0s&list=PLuT2TqJuwaY8afDn9R0pVYZd9HzhsaP5V)

Afternoon:

* [Playlist](https://www.youtube.com/watch?v=czNa5ix1vFs&list=PLuT2TqJuwaY-b1gN7b0NmF3GQ9_KHCxYG) | [Day 3, part 1]()

## Topics
* Creating and appending DOM Elements
* Flexbox and CSS
* Arrays and Objects
* ES2015+ (ES6) - [Babel docs](https://babeljs.io/docs/en/learn/)
* `this`

#### Flexbox

* [A Complete Guide to Flexbox](https://css-tricks.com/snippets/css/a-guide-to-flexbox/)
* [Flexbox.io](https://flexbox.io/)
* [Flex-grow](https://css-tricks.com/almanac/properties/f/flex-grow/)

#### CSS

* [CSS Tricks](https://css-tricks.com/): A great place to search for tips and tricks in css

## Examples

#### DOM

If we start with the following markup:
{{< code html >}}
&lt;div id=&quot;my-div&quot;&gt;&lt;/div&gt;
{{< /code >}}
We can add additional markup to it programmatically using JavaScript.  One way is to create new HTML elements using `document.createElement`, and adding them by using `appendChild`.  Styling of the element can even be changed by manipulating the element's `style` property.

{{< code js >}}
// create an h1 and modify text content and color
const heading = document.createElement('h1')
heading.textContent = "This is the best heading I've ever seen"
heading.style.color = "red"

// get a reference to the existing div and add the heading as a child element
const div = document.querySelector('#my-div')
div.appendChild(heading)
{{< /code >}}

This will produce the following markup:
{{< code html >}}
&lt;div id=&quot;my-div&quot;&gt;
  &lt;h1 style=&quot;color: red;&quot;&gt;This is the best heading I've ever seen&lt;/h1&gt;
&lt;/div&gt;
{{< /code >}}

#### Arrays
Arrays are extremely useful data structures in JavaScript, as they can be easily iterated and transformed through methods like `map`, `filter`, and `reduce`. 

{{< code js >}}
let arrayOfFood = ['pasta', 'chicken parmigiana', 'spaghetti', 'meatballs']

const result = arrayOfFood.filter(food => food.length > 10)  // ['chicken parmigiana']

{{< /code >}}

#### Objects
Almost everything in JavaScript is an Object.  The easiest way to create new Objects is with the [object initializer](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Object_initializer), more commonly known as 'object literal' syntax.  Basically, use curly braces to make an object `{}` and fill in the properties that you want.

Objects contain `key`/`value` pairs that allow you to set and retrieve values from them.

{{< code js >}}
// create a new object and assign some properties
const myObject = {
  prop1: 'Hello there',
  prop2: 42
}

// access the values in several ways, usually 'dot' or 'square bracket' notation
myObject.prop1 // => 'Hello there'
myObject['prop1'] //=> 'Hello there'

// new key/value pairs can also be assigned with these notations
myObject.prop3 = 'New Value!'
myObject['prop4'] = 'Newest Value!'

console.log(myObject)
// { 
//   prop1: 'Hello there',
//   prop2: 42,
//   prop3: 'New Value!',
//   prop4: 'Newest Value!'
// }
{{< /code >}}

We know that we can iterate through an Array using `map` or `forEach`.  Can we do something similar with objects?  There are a few ways to do it, but one of the newest and easiest is the `Object.keys` method.  It iterates through the enumerable properties of an object, returning an array of the property keys. Once we have an array of keys, we can `map` over _that_ and access each of the object properties individually.

{{< code js >}}
const myObj = {
  a: 'hi',
  b: 42,
  c: [1, 2, 3]
}

const myObjKeys = Object.keys(myObj)    // ['a', 'b', 'c']

myObjKeys.map(key => myObj[key])        // ['hi', 42, [1, 2, 3]]
{{< /code >}}

### ES2015+ (ES6+)
* Inheritance (with the ES2015 `class` syntax; it's still _prototypal_ inheritance though) - [ES26 Classes](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Classes)

### `this`

The same function can have different values for `this` depending on how the function is called/invoked.

{{< code js >}}
const app = {
  sayYeah() {
    console.log(`Yeah, ${this}`)
  },
  
  toString() {
    return 'app object'
  }
}

// When invoked as a method
app.sayYeah() // "Yeah, app object"

// When invoked as an event handler
document
  .querySelector('button')
  .addEventListener('click', app.sayYeah)
  // "Yeah, [object HTMLButtonElement]"

// When manually set with bind
app.sayYeah.bind('w00t')() // "Yeah, w00t"
{{< /code >}}


## Presentations

* <a target="_blank" href="/03-events-functions-arrays-objects.pdf">Day 3 Review</a>

## Projects

### CodePen

[Morning](https://codepen.io/dstrus/professor/mKzKEj/) | [Afternoon]()

### Chrismess
[Morning](https://github.com/xtbc18s3/chrismess) | [Afternoon](https://github.com/xtbc18s3/chrismess/tree/afternoon)

## Homework

* In addition to building a list item and adding it to the DOM (as we are now), also store each flick in an array.
### Bonus Credit
* Add a _delete_ button to each list item that removes it from the list.

### Super Mega Bonus Credit
* Remove the flick from the array as well.

### Super Mega Bonus Credit Hyper Fighting
* Add a _favorite_ button to each flick as well that lets you mark your favorites.
* Display favorites differently.
* Be sure the favorites are recorded appropriately in the array.
