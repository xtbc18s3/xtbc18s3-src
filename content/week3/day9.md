---
title: "Day 9: React Router"
weight: 2
---

<date>Tuesday, July 10, 2018</date>

## Lecture Videos

Morning:

* [Playlist](https://www.youtube.com/playlist?list=PLuT2TqJuwaY8afDn9R0pVYZd9HzhsaP5V) | [Day 9, part 1](https://www.youtube.com/watch?v=QP3ePI710Ws&list=PLuT2TqJuwaY8afDn9R0pVYZd9HzhsaP5V&index=115)

Afternoon:

* [Playlist](https://www.youtube.com/watch?v=czNa5ix1vFs&list=PLuT2TqJuwaY-b1gN7b0NmF3GQ9_KHCxYG) | [Day 9, part 1]()

## Topics

#### React
* [React.Fragment](https://reactjs.org/docs/fragments.html)
* [Conditional Rendering](https://reactjs.org/docs/conditional-rendering.html)

#### Routing
* React Router
  * `<Router />`
  * Links and NavLinks
  * Routes
  * `<Switch>`: [(Training Docs)](https://reacttraining.com/react-router/web/api/Switch)
  * `history`

## Examples

### Routing

[React Router](https://github.com/ReactTraining/react-router) provides a routing solution that allows us to change what UI we render based on the current URL.  The router is a _Higher Order Component_ that wraps a React app and allows us to navigate without additional requests and responses to and from the server.

#### Router Setup

Setting up React Router is easy. For web projects, install `react-router-dom`

{{< term >}}
yarn add react-router-dom   //this installs react router with yarn
{{< /term >}}

or

{{< term >}}
npm install --save react-router-dom   //this installs react router with npm
{{< /term >}}

Then, in your `ReactDOM.render` call, attach the Router as your base element, wrapping the root-level `<App />` component.  The whole app is now contained within the Router component, so we can take advantage of it anywhere.

**index.js**

{{< code jsx >}}
import React from 'react'
import ReactDOM from 'react-dom'
import { BrowserRouter as Router } from 'react-router-dom'
import App from './App'

ReactDOM.render(
  &lt;Router&gt;
    &lt;App /&gt;
  &lt;/Router&gt;,
  document.getElementById('root')
)
{{< /code >}}

#### Routes

The core of React Router is the `<Route />` component.  It allows you to specify what UI to render when a particular URL is matched.  For instance, if we wanted to render a `<Users />` component when we matched a `/users` URL, we could make the following Route:

{{< code jsx >}}
&lt;Route path='/users' component={Users} /&gt;
{{< /code >}}

If you don't want to render a whole component, a Route can alternatively accept a `render` prop, which accepts a function that returns JSX:

{{< code jsx >}}
&lt;Route path='/users' render={() => &lt;h1&gt;Users Path!&lt;/h1&gt;} /&gt;
{{< /code >}}

One important thing to keep in mind is that if we define a Route's path as `/users`, that will match both `/users` _and_ `/users/123`, because both begin with `/users`.  If we want the Route to match only when the path is _exactly_ `/users`, we can add the prop `exact` to our Route component.

{{< code jsx >}}
&lt;Route exact path='/users' component={Users} /&gt;
{{< /code >}}

#### Links

React Router also provides `<Link />` and `<NavLink />` components to make it easy to generate links to Routes. If we want to generate a Link that goes to `/about`, we can do the following:

{{< code jsx >}}
&lt;Link to='/about'&gt;About&lt;/Link&gt;
{{< /code >}}

NavLinks are similar, but provide some additional functionality.  The main difference is that they will add an `activeClassName` to the rendered link if the current URL matches the `to` property of the NavLink.  This allows active links to be styled differently than inactive links.

{{< code jsx >}}
&lt;NavLink to='/'&gt;Home&lt;/NavLink&gt;    // rendered link tag will have '.active' class when URL is '/'
{{< /code >}}

#### History

The `history` object is maintained and updated by the Router to keep track of where the user has navigated within the app.  It is passed to every component contained within the Router as part of the component's `props`.  It has a variety of helpful properties and methods that provide information and navigation. Here are just a few:

{{< code js >}}
history.length             // number of history entries
history.location           // provides the current location
history.push(path)         // navigates to a new path
history.go(n)              // navigates n steps through history stack
history.goBack()           // go back one step (history.go(-1))
history.goForward()        // go forward one step (history.go(1))
history.block(prompt)      // block navigation
{{< /code >}}

#### Fetch

> The Fetch API provides a JavaScript interface for accessing and manipulating parts of the HTTP pipeline, such as requests and responses.  It also provides a global `fetch()` method that provides an easy, logical way to fetch resources asynchronously across the network.

[_MDN - Using Fetch_](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API/Using_Fetch)

If we need to get data from a remote server (or send some to one), there are several ways to do it.  In vanilla JS, there is `XMLHttpRequest`, jQuery provides `$.ajax`, and there are a variety of other packages and libraries that provide their own version.  Luckily, there is a new kid in vanilla JS town - the _Fetch API_.

`fetch()` is a globally available, easy to use way to asynchronously send and receive data.  The simplest usage of fetch is to simply provide it with the URL of the request, and it will perform a `GET` request by default.  The `fetch()` function returns a promise that resolves when the data is received.  Once it is received, we can process and use the data with functions provided to the promise's `.then()` callbacks.

{{< code js >}}
fetch('https://api.mywebsite.com/users')    // fetch users data from 'mywebsite' api
  .then(response => response.json())        // parse the response json into JavaScript object(s)
  .then(users => console.log(users))        // log the parsed users to the console
  .catch(error => console.warn(error))      // if any errors occur, log them to the console
{{< /code >}}

{{% aside info "Fetch does more than just fetch" %}}
If no second argument is provided to `fetch()`, it defaults to a standard `GET` request.  However, the second argument can be a configuration object, allowing it to use different HTTP methods, set Headers, include Credentials, etc.  To find out more, check out [the docs](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API).
{{% /aside %}}

## Projects

#### Chatarang 
* [Morning](https://github.com/xtbc18s3/chatarang) | [Afternoon](https://github.com/xtbc18s3/chatarang-afternoon)

#### API Party 
* [Morning](https://github.com/xtbc18s3/api-party) | [Afternoon]()

## Homework

#### API Party

Your assignment, should you choose to accept it (and you should), is to add some more routes to the API Party and fetch data from your favorite APIs. The API you choose is up to you, but be sure to get some data and try to display it in a visually-pleasing way.

In case you don't have a favorite API, here are some suggestions:

* [Google Maps](https://developers.google.com/maps)
* [The Pokéapi](https://pokeapi.co)
* [OpenWeatherMap](https://openweathermap.org/api)
* [Spotify](https://developer.spotify.com/web-api/)
