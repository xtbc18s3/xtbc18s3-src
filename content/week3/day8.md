---
title: "Day 8: Firebase Authentication"
weight: 1
---

<date>Monday, July 9, 2018</date>

## Lecture Videos

Morning:

* [Playlist](https://www.youtube.com/playlist?list=PLuT2TqJuwaY8afDn9R0pVYZd9HzhsaP5V) | [Day 8, part 1](https://www.youtube.com/watch?v=-jN2fDc6ezg&list=PLuT2TqJuwaY8afDn9R0pVYZd9HzhsaP5V&index=99)

Afternoon:

* [Playlist](https://www.youtube.com/watch?v=czNa5ix1vFs&list=PLuT2TqJuwaY-b1gN7b0NmF3GQ9_KHCxYG) | [Day 8, part 1]()

## Topics

### React
* Lifecycle Methods: [Chart](http://projects.wojtekmaj.pl/react-lifecycle-methods-diagram/)

### Firebase Authentication

* 'firebase/auth'
* `authWithPopup`
* Signing in and out
* Handling auth state changes
* [Database rules](https://firebase.google.com/docs/database/security/quickstart?authuser=0)
* [GitHub OAuth](https://github.com/settings/applications/new)

### Deployment
* [Firebase Hosting](https://github.com/facebook/create-react-app/blob/master/packages/react-scripts/template/README.md#firebase)

## Examples

## Authentication

Firebase isn't just a real-time database. It can also provide authentication services via email/password, phone, or common third-party services like Github, Facebook, and Google. For _Chatarang_, we set up authentication via Google.

### Step 1: Enable Google authentication in Firebase

Go to your Firebase console and click on the "Authentication" tab in the "Develop" sidebar, then click on "Sign-in method."  You'll see a list of the authentication methods allowed by Firebase. Click on "Google" and then enable with the toggle switch.

### Step 2: Add Firebase auth to your app

_Note: This step assumes you already have your Firebase database added to your app._ 

Import `firebase/auth` into your app's firebase setup.  Enable firebase auth and also create an instance of `GoogleAuthProvider`.

**base.js**

{{< code lang="js" line="4,17,18" class="line-numbers" >}}
import Rebase from 're-base'
import firebase from 'firebase/app'
import 'firebase/database'

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
const db = firebase.database(app)
const base = Rebase.createClass(db)

export default base
{{< /code >}}

### Step 3: Set up the SignIn Component

Import `auth` and the `googleProvider` into whatever component handles the sign-in process. Call `signInWithPopup` on the `auth` object, passing the provider as a parameter. This will launch a popup screen that will prompt the user to sign in using the provider you have specified.

**SignIn.js**

{{< code jsx >}}
import React, { Component } from 'react'
import { auth, googleProvider } from './base'

class SignIn extends Component {
  state = {
    email: '',
  }

  authenticate = () => {
    auth.signInWithPopup(googleProvider)
      .then(result => this.props.handleAuth(result.user))
      .catch(error => console.log(error))
  }

  render() {
    return (
      &lt;button className="SignIn" onClick={this.authenticate}&gt;
        Sign In With Google
      &lt;/button&gt;
    )
  }
}

export default SignIn
{{< /code >}}

### Step 4: Handling auth state changes (and page refreshes)

Once the user has authenticated via the popup, the state of our authorization has changed (we now have an authenticated user). Other events that can cause auth state changes are signing out, timeouts, and page refreshes.  We should probably set up something to listen for these events.  In the `componentWillMount` lifecycle hook that runs when the Component is first getting loaded, we can call the `onAuthStateChanged` method provided on the global `auth` object to set up such a listener.

**App.js**

{{< code js >}}
// ...

componentWillMount() {
    const user = JSON.parse(localStorage.getItem('user'))

    if (user) {
      this.setState({ user })
    }

    auth.onAuthStateChanged(
      user => {
        if (user) {
          this.handleAuth(user)
        } else {
          this.handleUnauth()
        }
      }
    )
  }

// ...
{{< /code >}}

#### Step 5: Finishing sign-in

What the `authHandler` callback does is up to you, but for _Chatarang_, we had it do pretty typical things - save the user ID to state, and initialize syncing our local state for 'rooms' with the data stored on Firebase.

**App.js**

{{< code js >}}
// ...

handleAuth = (oauthUser) => {
    const user = {
      email: oauthUser.email,
      uid: oauthUser.uid,
      displayName: oauthUser.displayName,
    }
    this.setState({ user })
    localStorage.setItem('user', JSON.stringify(user))
  }

// ...
{{< /code >}}

#### Step 6: Signing out

Signing out when using Firebase for authentication is also simple - just call `auth.signOut()`!

**App.js**

{{< code js >}}
// ...

 signOut = () => {
    auth.signOut()
  }

  handleUnauth = () => {
    this.setState({ user: {} })
    localStorage.removeItem('user')
  }

// ...
{{< /code >}}

### Rules

For your Firebase database, you can set up rules (written in JSON) that specify the conditions under which data is allowed to be read or written.  By default, a newly generated project will require that a user be authenticated to read or write _any_ data.

{{< code js >}}
{
  "rules": {
    ".read": "auth != null",
    ".write": "auth != null"
  }
}
{{< /code >}}

If you do not have authentication set up yet, these values can be set to `true`.  This allows _anyone_ to read or write any data in the database.  This can be convenient, but probably not a good idea long-term (and you _will_ get a warning if you do that).

Additional rules can be applied per endpoint:

{{< code js >}}
{
  "rules": {
    "emails": {
      ".read": true,
      ".write": "auth != null"
    },
    "texts": {
      ".read": true,
      ".write": "auth != null"
    },
    "users": {
      "$userId": {
        ".read": "auth != null && auth.uid == $userId",
        ".write": "auth != null && auth.uid == $userId"
      }
    }
  }
}
{{< /code >}}

The above [rules](https://firebase.google.com/docs/database/security/quickstart?authuser=0) translate to:

* texts and emails can be read by anyone, but only written by authenticated users
* users data can be read and written only by an authenticated user whose `uid` matches the `$userId` of that item

### Deploying

Now that Chatarang has routing, deployment gets a bit more complicated.  Our app is a single-page application, so the server that our app is deployed to needs to always return `index.html` (the one page in our single-page app).  However, if we type `https://{yourdomainhere}/notes` in the address bar, the server will try to find a file called `notes.html` to send back (which it won't find, of course).  So how do we get it to always respond with `index.html` and let our client-side router handle the routing?

#### Firebase

Firebase _does_ allow for the server to be configured to always return `index.html`, so that is the option we chose during class.  To do so, we first need to install Firebase's CLI tools.

{{< term >}}
npm install -g firebase-tools
{{< /term >}}

Once the Firebase tools are installed, we can use them to login, initialize a firebase project, and deploy.  (Note, make sure you have made a production build with `npm run build` before deploying).

{{< term >}}
firebase login
firebase init
firebase deploy
{{< /term >}}

{{% aside info "Firebase Init" %}}
`firebase init` will prompt you to answer a bunch of questions about how you want to configure the app you are deploying.  For more information about how to answer those questions, check out the `create-react-app` README [here](https://github.com/facebookincubator/create-react-app/blob/master/packages/react-scripts/template/README.md#firebase).
{{% /aside %}}

If you receive this message...

> Error: Cannot run login in non-interactive mode. See login:ci to generate a token for use in non-interactive environments.

...run this command instead:

```firebase login --interactive```

## Projects

#### Chatarang 
* [Morning](https://github.com/xtbc18s3/chatarang) | [Afternoon](https://github.com/xtbc18s3/chatarang-afternoon)

## Homework
* Set the current room when you click a room in the sidebar.

### Bonus Credit

* Sync the list of rooms with Firebase (using `base.syncState()`).

### Super Mega Bonus Credit

* Sync each room's messages separately.

### Super Mega Bonus Credit Hyper Fighting

* Add a form to create new rooms.
