# The Device Registration Token 

On initial startup of your app, the FCM SDK generates a registration token for the client app instance.  This token is needed to be able to send FCM messages and notifications to the user's device.

This section describes how to retrieve the token and how to monitor changes to the token. Because the token could be rotated after initial startup, you are strongly recommended to monitor for the latest updated registration token.

The registration token may change when:

- The app deletes Instance ID
- The app is restored on a new device
- The user uninstalls/reinstall the app
- The user clears app data.

## 1) Retrieve the current registration token

```js
const fcmToken = await firebase.messaging().getToken();
if (fcmToken) {
    // user has a device token
} else {
    // user doesn't have a device token yet
}
```

or:

```js
firebase.messaging().getToken()
  .then(fcmToken => {
    if (fcmToken) {
      // user has a device token
    } else {
      // user doesn't have a device token yet
    } 
  });
```

## 2) Monitor token generation

The `onTokenRefresh` callback fires with the latest registration token whenever a new token is generated.

```js
componentDidMount() {
    this.onTokenRefreshListener = firebase.messaging().onTokenRefreshed(fcmToken: string => {
        // Process your token as required
    });
}

componentWillUnmount() {
    this.onTokenRefreshListener();
}
```
