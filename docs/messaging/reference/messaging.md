# Cloud Messaging

Firebase Cloud Messaging ([FCM](https://firebase.google.com/docs/cloud-messaging/)) allows you to send push messages at no cost to both Android & iOS platforms.

As the Firebase Web SDK has limited messaging functionality, the following methods within `react-native-firebase` have been created to handle FCM in the React Native environment.

Badge notification is well known on the iOS platform, but also supported by different Android devices / launchers. This library uses the [ShortcutBadger](https://github.com/leolin310148/ShortcutBadger) library to set the badge number also on Android. A list of supported launcher can be found there.

To customise the notification icon, make the following changes:

1) Add the following to the AndroidManifest.xml
`<meta-data` <br />
   `android:name="com.google.firebase.messaging.default_notification_icon"`<br />
   `android:resource="@drawable/ic_stat_ic_notification" />`<br />
`<meta-data` <br />
    `android:name="com.google.firebase.messaging.default_notification_color"
    android:resource="@color/colorAccent" />` <br />
<br />Then add your notification icon (named `ic_stat_ic_notification.png`) to the drawable folders and add the color accent to the colors.xml (eg. `<color name="colorAccent">#44fff2</color>`).
     

!> On iOS, your app first needs to [ref messaging#requestPermission] in order to receive Cloud Messages.

## Methods

The following methods are accessed via the Cloud Messaging instance firebase.messaging().

### subscribeToTopic
[method]subscribeToTopic(topic) returns void;[/method]

Subscribes the device to a topic.

| Parameter |         |
| --------- | ------- |
| topic   | **string**  |

### unsubscribeFromTopic
[method]unsubscribeFromTopic(topic) returns void;[/method]

Unsubscribes the device to a topic.

| Parameter |         |
| --------- | ------- |
| topic   | **string**  |

### getInitialNotification
[method]getInitialNotification() returns Promise containing Object;[/method]

When the application has been opened from a notification, `getInitialNotification` is called and the notification payload is returned. Use [ref messaging#onMessage] for notifications when the app is running.

### getToken
[method]getToken() returns Promise containing string;[/method]

Returns the devices FCM token. This token can be used in the Firebase console to send messages to directly.

### deleteInstanceId
[method]deleteInstanceId() returns Promise containing void;[/method]

Reset Instance ID and revokes all tokens.

### onTokenRefresh
[method]onTokenRefresh(listener) returns function();[/method]

On the event a devices FCM token is refreshed by Google, the new token is returned in a callback listener.

Returns an unsubscribe function.

| Parameter |         |
| --------- | ------- |
| listener   | **function(string)** <br /> A listener function called when a new token is generated. |

### onMessage
[method]onMessage() returns function();[/method]

On a new message, the payload object is passed to the listener callback. This method is only triggered when the app is running. Use [ref messaging#getInitialNotification] for notifications which cause the app to open.

Returns an unsubsciber function.

### [ios] requestPermissions
[method]requestPermissions() returns void;[/method]

Requests app notification permissions in an Alert dialog.

On iOS 9 or below, there's no way to tell whether the user accepted or rejected the permissions popup - in this case the resolved object will have a property called `status` with a value of `"unknown"`

In all other cases the resolved object will have a `granted` property which is a boolean value of `true` or `false`.

### setBadgeNumber
[method]setBadgeNumber(value) returns void;[/method]

Sets the badge number on the app icon.

| Parameter |         |
| --------- | ------- |
| value   | **number**  |

### getBadgeNumber
[method]getBadgeNumber() returns Promise containing number;[/method]

Returns the current badge number on the app icon.
