# Receiving Firebase Cloud Messages

## 1) Check permissions

Before you are able to send and receive Cloud Messages, you need to ensure that the user has granted the correct permissions:

```js
const enabled = await firebase.messaging().hasPermission();
if (enabled) {
    // user has permissions
} else {
    // user doesn't have permission
}
```

or:

```js
firebase.messaging().hasPermission()
  .then(enabled => {
    if (enabled) {
      // user has permissions
    } else {
      // user doesn't have permission
    } 
  });
```

## 2) Request permissions

If the user has not already granted permissions, then you can prompt them to do so, as follows:

```js
try {
    await firebase.messaging().requestPermission();
    // User has authorised
} catch (error) {
    // User has rejected permissions
}
```

or:

```js
firebase.messaging().requestPermission()
  .then(() => {
    // User has authorised  
  })
  .catch(error => {
    // User has rejected permissions  
  });
```

## 3) Listen for FCM messages

We class Messages as: 

- data-only messages from FCM

> For notification-only or notification + data messages, please see the [Notifications Module](version /notifications/receiving-notifications).

A message will trigger the `onMessage` listener when the application receives a message in the foreground.

```js
// Optional: Flow type
import type { RemoteMessage } from 'react-native-firebase';

componentDidMount() {
    this.messageListener = firebase.messaging().onMessage(message: RemoteMessage => {
        // Process your message as required
    });
}

componentWillUnmount() {
    this.messageListener();
}
```

## 4) (Optional)(Android-only) Listen for FCM messages in the background

Android allows you to act on data-only messages when your application is closed or running in the background.  This is particularly useful if you'd like to be able to show heads-up notifications to your user.

To allow this to work, we make use of React Native's built-in [Headless JS](https://facebook.github.io/react-native/docs/headless-js-android.html) functionality.

### 1) Add Service to Android Manifest

Firstly, check that you've followed the optional steps in the [Android Installation guide](version /installation/android).

### 2) Handle background messages

Create a new Javascript file (for this example we'll call it `bgMessaging.js`) which has the following structure:

```js
// @flow
import firebase from 'react-native-firebase';
// Optional flow type
import type { RemoteMessage } from 'react-native-firebase';

export default async (message: RemoteMessage) => {
    // handle your message
    
    return Promise.resolve();
}
```

> This handler method must return a promise and resolve within 60 seconds.

### 3) Register the background handler

In your main `index.js` you need to register your background handler as follows:

```js
import bgMessaging from './src/bgMessaging'; // <-- Import the file you created in (2)

// Current main application
AppRegistry.registerComponent('ReactNativeFirebaseDemo', () => bootstrap);
// New task registration
AppRegistry.registerHeadlessTask('RNFirebaseBackgroundMessage', () => bgMessaging); // <-- Add this line
```

> The headless task must be registered as `RNFirebaseBackgroundMessage`.