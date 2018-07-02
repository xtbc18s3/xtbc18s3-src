---
title: "Day 5: Intro to React"
weight: 1
---

<date>Monday, July 2, 2018</date>

## Lecture Videos

Morning:

* [Playlist](https://www.youtube.com/playlist?list=PLuT2TqJuwaY8afDn9R0pVYZd9HzhsaP5V) | [Day 5, part 1](https://www.youtube.com/watch?v=WcZqhIcFpac&t=0s&list=PLuT2TqJuwaY8afDn9R0pVYZd9HzhsaP5V&index=50)

Afternoon:

* [Playlist](https://www.youtube.com/watch?v=czNa5ix1vFs&list=PLuT2TqJuwaY-b1gN7b0NmF3GQ9_KHCxYG) | [Day 5, part 1](https://www.youtube.com/watch?v=vM5LX8tfSOM&list=PLuT2TqJuwaY-b1gN7b0NmF3GQ9_KHCxYG&index=49)

## Topics

### ES2015+ (ES6+)
* Modules (import/export) - [ES2015 modules on Babel](https://babeljs.io/learn-es2015/#ecmascript-2015-features-modules)

### [React](https://facebook.github.io/react/)
* [Imperative vs. Declarative](https://tylermcginnis.com/imperative-vs-declarative-programming/)
* Components
  * JSX - [Docs: Introducing JSX](https://facebook.github.io/react/docs/introducing-jsx.html)
  * Props - [Docs: Components and Props](https://facebook.github.io/react/docs/components-and-props.html)
  * State - [Docs: State and Lifecycle](https://facebook.github.io/react/docs/state-and-lifecycle.html)
* `create-react-app`
* Stateless Functional Components
  * [Stateless Functional Components in React](http://javascriptplayground.com/blog/2017/03/functional-stateless-components-react/)
  * [Functional Components vs. Stateless Functional Components vs. Stateless Components](https://tylermcginnis.com/functional-components-vs-stateless-functional-components-vs-stateless-components/)
  * [Nine Wins You Might Have Overlooked](https://hackernoon.com/react-stateless-functional-components-nine-wins-you-might-have-overlooked-997b0d933dbc)
* Property initializers (and arrow functions)

## Examples

### React

#### Basic App
A basic React application requires a minimum of four things:

1. An HTML file with at least one empty element
2. The React library
3. One or more React Component(s)
4. A JavaScript call to attach the React Component to the empty element in step one

A minimal example:

{{< code html >}}
&lt;-- index.html --&gt;
&lt;html&gt;
  &lt;head&gt;
    &lt;title&gt;Basic React App&lt;/title&gt;
    &lt;script src=&quot;App.js&quot;&gt;&lt;/script&gt;
  &lt;/head&gt;
  &lt;body&gt;
    &lt;div id=&quot;app&quot;&gt;&lt;/div&gt;
  &lt;/body&gt;
&lt;/html&gt;
{{< /code >}}

{{< code jsx >}}
// App.js
class App extends React.Component {
  render() {
    return (
      &lt;h1&gt;Hello, world!&lt;/h1&gt;
    )
  }
}

ReactDOM.render(&lt;App /&gt;, document.querySelector('#app'))
{{< /code >}}

The body of the HTML above contains only an empty `div` with an id of 'app'.  This is where we will tell React to render our app. The `App.js` file defines the `App` component, and also makes the call to `ReactDOM.render`, which attaches `<App />` to the `div#app` element.

React will 'fill in' the div with the return result of the `App` component's `render` method, in this case, the markup `<h1>Hello, world!</h1>`.

#### Props

React components can be thought of as JavaScript functions.  They take in arguments, called `props`, and return markup that gets rendered to the page. Props can be just about anything, including strings, booleans, functions, objects, etc...

{{< code jsx >}}
class App extends React.Component {
  render() {
    return (
      &lt;h1&gt;Hello, {this.props.name}!&lt;/h1&gt;
    )
  }
}

&lt;App name=&quot;Bob&quot; /&gt;
{{< /code >}}

By passing in the string `"Bob"` to the `App` component, we can access that value from within the `App` class as a property on `this.props`.

Our rendered output would then be:

{{< code html >}}
&lt;h1&gt;Hello, Bob!&lt;/h1&gt;
{{< /code >}}

#### State

Components receive _props_ as arguments and cannot change their values. Data that needs to change belongs in _state_.

State should be initialized in the constructor and updated via `setState`.

{{% aside danger Do Not Modify State Directly %}}
Always use `setState` to modify a component's state. The only time you should set state directly is in the constructor.
{{% /aside %}}

{{< code jsx >}}
class App extends React.Component {
  constructor() {
    super()
    this.state = {
      count: 0
    }
  }

  increment(ev) {
    count = this.state.count + 1
    this.setState({ count })
  }

  render() {
    return (
      &lt;button type="button" onClick={this.increment.bind(this)}&gt;
        Click to Increment
      &lt;/button&gt;
      &lt;p&gt;
        Button has been clicked {this.state.count} times
      &lt;p&gt;
    )
  }
}

&lt;App /&gt;
{{< /code >}}

#### Modules

With [modules](https://babeljs.io/learn-es2015/#ecmascript-2015-features-modules), you can define each component in separate files, importing them as needed.

**Header.js**

{{< code jsx >}}
class Header extends React.Component {
  render() {
    return (
      &lt;h1&gt;Hello, {this.props.name}!&lt;/h1&gt;
    )
  }
}

export default Header
{{< /code >}}

**App.js**

{{< code jsx >}}
import Header from './Header'

class App extends React.Component {
  render() {
    return (
      &lt;Header name=&quot;Bob&quot; /&gt;
    )
  }
}

export default App
{{< /code >}}

#### `create-react-app`

* [Documentation/README](https://github.com/facebook/create-react-app)

#### Stateless Functional Components

Not every React Component needs to have state.  Many simply render a bit of `props` and UI.  For such components, we don't need to instantiate a whole class that inherits from `React.Component`, we can simply write a function that accepts `props` as an argument and returns the markup we need.

For instance, in the previous example, the `Person` component can easily be re-written as a Stateless Functional Component.

{{< code jsx >}}
function Person (props) {
  return (
    &lt;li&gt;Hello, {props.person.name}!&lt;/li&gt;
  )
}

// Or...

const Person = (props) => &lt;li&gt;Hello, {props.person.name}!&lt;/li&gt;
{{< /code >}}

#### Property initializers

{{% aside info "Subject to minor changes" %}}
[Property initializers](https://github.com/tc39/proposal-class-public-fields) are a [Stage 3 proposal](https://tc39.github.io/process-document/) for ECMAScript, meaning that they're a candidate, but requires further refinement and feedback from implementations and users before it becomes part of the standard. Facebook itself is already using these techniques in production, however.
{{% /aside %}}

From the proposal:

> "Class instance fields" describe properties intended to exist on instances of a class (and may optionally include initializer expressions for said properties).

We can take advantage of this in React.

[**Read more: Using ES7 property initializers in React**](https://babeljs.io/blog/2015/06/07/react-on-es6-plus)

We can use a property initializer to set the initial value of state without writing a constructor:

{{< code jsx >}}
class Song extends React.Component {
  state = {
    versesRemaining: 5,
  }
}
{{< /code >}}

We can even set default props and use those in the initial state:

{{< code jsx >}}
class Song extends React.Component {
  static defaultProps = {
    autoPlay: false,
    verseCount: 10,
  }
  state = {
    versesRemaining: this.props.verseCount,
  }
}
{{< /code >}}

#### Property initializers + arrow functions

Combining property initializers and arrow functions gives us a convenient way to auto-bind `this`, since arrow functions inherit `this` from the scope in which they are declared (lexical scoping):

{{< code jsx >}}
class Something extends React.Component {
  handleButtonClick = (ev) => {
    // `this` is bound correctly!
    this.setState({ buttonWasClicked: true });
  }
}
{{< /code >}}

## Presentations

* <a target="_blank" href="/intro-to-react.pdf">Intro to React</a>

## Projects

#### Reactrobats 
* [Morning](https://codepen.io/dstrus/professor/ERMVGw/) | [Afternoon](https://codepen.io/dstrus/professor/aKMJLj/)

#### Dwarf Underground
* [Fork and clone this repository](https://github.com/xtbc18s3/dwarf-underground)
* [Morning](https://github.com/xtbc18s3/dwarf-morning) | [Afternoon](https://github.com/xtbc18s3/dwarf-afternoon)

## Homework

* Split the page into at least 6 total components

### Bonus Credit

* Split the page into at least 10 total components, including components *in* components

### Super Bonus Credit

* Render the four article links at the bottom of the screen using `map` and passing in the props they need

### Super Mega Bonus Credit

* Make a component that contains a text field for leaving a comment
* Have the text field appear only when the 'comments' link at the bottom of the article is clicked

### Super Mega Bonus Credit Hyper Fighting

* Actually display comments that are entered and submitted
