---
title: "Day 7: React Components & Firebase"
weight: 3
---

<date>Thursday, July 5, 2018</date>

## Lecture Videos

Morning:

* [Playlist](https://www.youtube.com/playlist?list=PLuT2TqJuwaY8afDn9R0pVYZd9HzhsaP5V) | [Day 7, part 1](https://www.youtube.com/watch?v=sAnOHv_W4G4&list=PLuT2TqJuwaY8afDn9R0pVYZd9HzhsaP5V&index=82)

Afternoon:

* [Playlist](https://www.youtube.com/watch?v=czNa5ix1vFs&list=PLuT2TqJuwaY-b1gN7b0NmF3GQ9_KHCxYG) | [Day 7, part 1]()

## Topics

### React

* Methods as props
* [Conditional Rendering] (https://reactjs.org/docs/conditional-rendering.html#___gatsby)
* [If-Else in JSX](https://react-cn.github.io/react/tips/if-else-in-JSX.html)

### JavaScript

* [Destructuring assignment](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment)
* [Spread operator](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_syntax)
* [Ternary operators](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Conditional_Operator)

### Firebase

* [Firebase](https://firebase.google.com/)
* [`re-base` README](https://github.com/tylermcginnis/re-base)

## Examples

### [React](https://facebook.github.io/react/)

#### Methods as props

Sometimes one component needs to update another component's state. It can't do that directly, but it can call a method from that other component if it's available via a prop.

{{< code lang="jsx" line="5,23" class="line-numbers" >}}
import React from 'react'
import ReactDOM from 'react-dom'

const PartyButton = ({ celebrate, celebrations }) =&gt; {
  return &lt;button onClick={celebrate}&gt;Party! {celebrations}&lt;/button&gt;
}

class App extends React.Component {
  constructor() {
    super()
    this.state = {
      celebrations: 0,
    }
    this.celebrate = this.celebrate.bind(this)
  }

  celebrate() {
    const celebrations = this.state.celebrations + 1
    this.setState({ celebrations })
  }

  render() {
    return &lt;PartyButton celebrate={this.celebrate} celebrations={this.state.celebrations} /&gt;
  }
}

ReactDOM.render(&lt;App /&gt;, document.querySelector('main'))
{{< /code >}}

### JavaScript (ES6+)

#### Destructuring assignment

[Destructuring assignment](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment) syntax is a JavaScript expression that makes it possible to unpack values from arrays, or properties from objects, into distinct variables.

{{< code js >}}
const myObj = {
  a: true,
  b: 'Destructuring!'
}

let { a, b } = myObj

console.log(a) // => true
console.log(b) // => 'Destructuring!'
{{< /code >}}

### Firebase 
#### Database Setup / Auth

**base.js**

{{< code lang="js" line="4,17,18" class="line-numbers" >}}
import firebase from 'firebase/app'

// Initialize Firebase
const config = {
  apiKey: "YOUR API KEY",
  authDomain: "YOUR AUTH DOMAIN",
  databaseURL: "YOUR DATABASE URL",
  projectId: "YOUR PROJECT ID",
  storageBucket: "YOUR STORAGE BUCKET",
  messagingSenderId: "YOUR MESSAGING SENDER ID"
}

const app = firebase.initializeApp(config)
{{< /code >}}

Firebase isn't just a real-time database.  It can also provide authentication services via email/password, phone, or common third-party services like Github, Facebook, and Google. Read more about authentication using Firebase [here](https://firebase.google.com/docs/auth/).

## Projects

#### Chatarang 
* [Morning](https://github.com/xtbc18s3/chatarang) | [Afternoon](https://github.com/xtbc18s3/chatarang-afternoon)

## Homework

### ALL HYPER FIGHTING, ALL THE TIME!

* Add the [re-base](https://github.com/tylermcginnis/re-base) package to your project. At the command-line, type:

```shell
yarn add re-base
```

Confirm that `re-base` is now listed under `dependencies` in `package.json`.

* Update `base.js` to initialize and export `Rebase`.

_Hint_: `export default Rebase.createClass(db)`

* Use [`base.syncState()`](https://github.com/tylermcginnis/re-base#syncstateendpoint-options) to sync your messages with Firebase.

### Super Mega Bonus Credit Hyper Fighting

* Try to make authentication work with Firebase!
