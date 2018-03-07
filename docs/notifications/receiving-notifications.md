# Receiving Notifications

## 1) Check permissions

Before you are able to send and receive Notifications, you need to ensure that the user has granted the correct permissions:

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

## 3) Listen for Notifications

Notifications encompass three different types:

- `notification` only messages from FCM
- `notification + data` messages from FCM
- `local` notifications

> For `data` only FCM messages, please see the [messaging section](version /messaging/receiving-messages).

A notification will trigger one of two listeners depending on the state of your application:

- `onNotificationDisplayed` - Triggered when a particular notification has been displayed
- `onNotificationReceived` - Triggered when a particular notification has been received

```js
// Optional: Flow type
import type { Notification } from 'react-native-firebase';

componentDidMount() {
    this.notificationDisplayedListener = firebase.notifications().onNotificationDisplayed(notification: Notification => {
        // Process your notification as required
    });
    this.notificationReceivedListener = firebase.notifications().onNotificationReceived(notification: Notification => {
        // Process your notification as required
    });
}

componentWillUnmount() {
    this.notificationDisplayedListener();
    this.notificationReceivedListener();
}
```

## 4) Listen for a Notification being opened

### App in Foreground and background
If your app is in the foreground, or background, you can listen for when a notification is clicked / tapped / opened as follows:

```js
// Optional: Flow type
import type { Notification, NotificationOpen } from 'react-native-firebase';

componentDidMount() {
    this.notificationOpenedListener = firebase.notifications().onNotificationOpened(notificationOpen: NotificationOpen => {
        // Get the action triggered by the notification being opened
        const action = notificationOpen.action;
        // Get information about the notification that was opened
        const notification: Notification = notificationOpen.notification;
    });
}

componentWillUnmount() {
    this.notificationOpenedListener();
}
```

### App Closed

If your app is closed, you can check if it was opened by a notification being clicked / tapped / opened as follows:

```js
// Optional: Flow type
import type { Notification, NotificationOpen } from 'react-native-firebase';

async componentDidMount() {
    const notificationOpen: NotificationOpen = await firebase.notifications().getInitialNotification();
    // Get the action triggered by the notification being opened
    const action = notificationOpen.action;
    // Get information about the notification that was opened
    const notification: Notification = notificationOpen.notification;
}
```

or:

```js
// Optional: Flow type
import type { Notification, NotificationOpen } from 'react-native-firebase';

componentDidMount() {
    firebase.notifications().getInitialNotification()
      .then(notificationOpen: NotificationOpen => {
        if (notificationOpen) {
          // App was opened by a notification
          // Get the action triggered by the notification being opened
          const action = notificationOpen.action;
          // Get information about the notification that was opened
          const notification: Notification = notificationOpen.notification;  
        }
      });
}
```