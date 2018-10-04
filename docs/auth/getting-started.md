# Authentication - Getting Started

Firebase makes authentication super easy to implement out of the box whether you're looking for anonymous, email & password or social authentication.

For newcomers, although the API is simple, actually implementing it into the flow of your app may seem tricky. The following guide will run through a couple of scenarios which you'll likely find yourself coming across.

We'll only be using React Native & RNFirebase here to avoid any confusion, although you may want to hook this up with a state management tool like [Redux](http://redux.js.org/docs/introduction/) as your app becomes more complex.

RNFirebase uses the native Firebase SDKs so your authenticate state is saved to the device, meaning if you close the app and re-open the app, the user won't need to re-authenticate.

## Anonymous Auth

Even though your app might not require any authentication, wouldn't it be great if you could somehow keep track of your users, giving them a unique identifier?

This is exactly what anonymous auth does. It creates an account for the user without requiring them to authenticate.

> Ensure you've enabled `Anonymous` sign-in on the [Firebase console](https://console.firebase.google.com) under Authentication!

The best place to implement this would be in a "root" level component which contains the entire app, lets call this component `App`:

```jsx
import React from 'react';
import { View, Text } from 'react-native';

class App extends React.Component {

  render() {
    return (
      <View>
        <Text>Welcome to my awesome app!</Text>
      </View>
    );
  }

}

export default App;
```

Right now, we simply render out some text. Lets now anonymously authenticate the user before we show the app.
We'll use the [ref auth#signInAnonymously] method to do this:

```jsx
import React from 'react';
import { View, Text } from 'react-native';
import firebase from 'react-native-firebase';

class App extends React.Component {

  constructor() {
    super();
    this.state = {
      isAuthenticated: false,
    };
  }
  
  componentDidMount() {
    firebase.auth().signInAnonymously()
      .then(() => {
        this.setState({
          isAuthenticated: true,
        });
      });
  }

  render() {
    // If the user has not authenticated
    if (!this.state.isAuthenticated) {
      return null;
    }
  
    return (
      <View>
        <Text>Welcome to my awesome app!</Text>
      </View>
    );
  }

}

export default App;
```

Now the app wont render until the [ref auth#signInAnonymously] method has resolved. You can now access the anonymous users details using the [ref auth#currentUser] property.

If the user closes and re-opens the app, Firebase will automatically sign them back in to the anonymous account they've already been assigned if available. 

## Required Email/Password Auth

Another common scenario would be requiring your users to sign into an account before they can access your app. You'll probably also want them to be able to logout too.

Luckily, Firebase makes this super easy by providing a [ref auth#signInWithEmailAndPassword] method. If you also need a registration screen use [ref auth#createUserWithEmailAndPassword] instead. 

> Ensure you've enabled `Email/Password` sign-in on the [Firebase console](https://console.firebase.google.com) under Authentication!

The best place to implement this would be in a "root" level component which contains the entire app, lets call this component `App`:

```jsx
import React from 'react';
import { View, Text } from 'react-native';
import firebase from 'react-native-firebase';

class App extends React.Component {

  render() {
    return (
      <View>
        <Text>Welcome to my awesome app!</Text>
      </View>
    );
  }

}

export default App;
```

Much like anonymous auth, we'll need to use state to render the app based on the current Firebase authentication state.
The main difference is that we need to keep track of the users current authentication state (for logging in, creating an account or logging out). This can be done with the [ref auth#onAuthStateChanged] method:

We'll also keep track of the unsubscriber function for when the app unmounts.

```jsx
import React from 'react';
import { View, Text } from 'react-native';
import firebase from 'react-native-firebase';

import Login from './screens/Login';

class App extends React.Component {

  constructor() {
    super();
    this.unsubscriber = null;
    this.state = {
      user: null,
    };
  }

  /**
   * Listen for any auth state changes and update component state
   */
  componentDidMount() {
    this.unsubscriber = firebase.auth().onAuthStateChanged((user) => {
      this.setState({ user });
    });
  }
  
  componentWillUnmount() {
    if (this.unsubscriber) {
      this.unsubscriber();
    }
  }

  render() {
    if (!this.state.user) {
      return <Login />;
    }
  
    return (
      <View>
        <Text>Welcome to my awesome app {this.state.user.email}!</Text>
      </View>
    );
  }

}

export default App;
```

As the `onAuthStateChanged` listener returns a [ref auth.User] or `null`, we can directly pass this to our state.

When an authentication event happens, user state will be updated with our user (logged in or account created) or `null` (logged out). If the user state is null, the login screen is shown.
