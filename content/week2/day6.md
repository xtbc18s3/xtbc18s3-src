---
title: "Day 6: React"
weight: 2
---

<date>Tuesday, July 3, 2018</date>

## Lecture Videos

Morning:

* [Playlist](https://www.youtube.com/playlist?list=PLuT2TqJuwaY8afDn9R0pVYZd9HzhsaP5V) | [Day 6, part 1](https://www.youtube.com/watch?v=xNvHMuOYc1Y&list=PLuT2TqJuwaY8afDn9R0pVYZd9HzhsaP5V&index=63)

Afternoon:

* [Playlist](https://www.youtube.com/watch?v=czNa5ix1vFs&list=PLuT2TqJuwaY-b1gN7b0NmF3GQ9_KHCxYG) | [Day 6, part 1]()

## Topics
* [React Documentation](https://reactjs.org/docs/getting-started.html)
* [`create-react-app`](https://github.com/facebook/create-react-app)
* [Google Fonts](https://fonts.google.com/)
* [CSS in JS](https://hackernoon.com/all-you-need-to-know-about-css-in-js-984a72d48ebc)
* Using `map` with components
* Forms
  * [Controlled](https://facebook.github.io/react/docs/forms.html) vs. [Uncontrolled](https://facebook.github.io/react/docs/uncontrolled-components.html)
  * [Form inputs in React](https://goshakkk.name/controlled-vs-uncontrolled-inputs-react/)
* [Mastering Markdown](https://guides.github.com/features/mastering-markdown/)

## Examples

#### Using `map` with Components

**Person.js**

{{< code jsx >}}
class Person extends React.Component {
  render() {
    return (
      &lt;li&gt;Hello, {this.props.person.name}!&lt;/li&gt;
    )
  }
}

export default Person
{{< /code >}}

**PersonList.js**

{{< code jsx >}}
import Person from './Person'

class PersonList extends React.Component {
  render() {
    const people = [
      { name: 'Dana', hair: 'blonde' },
      { name: 'Nichole', hair: 'long' },
      { name: 'Davey', hair: 'long gone' }
    ]
    return (
      &lt;div&gt;
        &lt;h2&gt;People&lt;/h2&gt;
        {
          people.map((person => &lt;Person person={person} /&gt;))
        }
      &lt;/div&gt;
    )
  }
}

export default PersonList
{{< /code >}}

* `map` with keys
  * [Key props on list items](https://reactjs.org/docs/lists-and-keys.html)

## Projects

#### Chatarang 
* [Morning](https://github.com/xtbc18s3/chatarang) | [Afternoon]()

## Homework

* Create and style more components, based on the `chat-static` content. There should be approximately one CSS file per component.

### Super Mega Bonus Credit Hyper Fighting

* Make a `SignIn` component with a form that takes a user name or email.
* When the form is submitted, save that user in the `state` of the `App` component.
* When `state.user` is not set, show the `SignIn` component.
* When `state.user` is set, show the `Main` component.

_Hint_: You need to figure out how to do **conditional rendering**.
