# Cloud Messaging

Firebase Cloud Messaging ([FCM](https://firebase.google.com/docs/cloud-messaging/)) allows you to send push messages at no cost to both Android & iOS platforms. 

This `messaging` module deals with pure data-only messages only.  If you're interested in sending and receiving notifications, please take a look at the [ref notifications.Notifications] module.

!> On iOS, your app first needs to have [ref Messaging#requestPermission] in order to receive Cloud Messages.

## Properties

### ios

[method]ios returns [ref messaging.IOSMessaging];[/method]

Gets the iOS specific methods and properties of messaging.

## Methods

The following methods are accessed via the Cloud Messaging instance `firebase.messaging()`.

### getToken
[method]getToken() returns Promise containing String;[/method]

This generated registration token is used to identify the app instance and periodically sends data to the Firebase backend. To stop this, call firebase.messaging.Messaging#deleteToken.

Returns the FCM token;

### hasPermission
[method]hasPermission() returns Promise containing boolean;[/method]

Checks if the user has granted the appropriate permissions to be able to send and receive messages.

Returns true if permission is granted, false otherwise.

### onMessage
[method]onMessage(nextOrObserver) returns function();[/method]

When a push message is received, the onMessage() event is dispatched with the payload of the push message.

Returns an unsubscribe function.

Parameter |         |
| --------- | ------- |
| nextOrObserver   | **function([ref messaging.RemoteMessage])** or **Object** <br /> This function, or observer object with `next` defined, is called when a data-only message is received. |

### onTokenRefresh
[method]onTokenRefresh(nextOrObserver) returns function();[/method]

You should listen for token refreshes so your web app knows when FCM has invalidated your existing token.

Returns an unsubscribe function.

Parameter |         |
| --------- | ------- |
| nextOrObserver   | **function(string)** or **Object** <br /> This function, or observer object with `next` defined, is called when a token refresh has occurred with the new token. |

### requestPermission
[method]requestPermission() returns Promise containing void;[/method]

Notification permissions are required to send a user push messages. Calling this method displays the permission dialog to the user and resolves if the permission is granted.

After granting the permission, calling [ref messaging.IOSMessaging#registerForRemoteNotifications] will sync your app's apns token with firebase on demand.

Returns a promise that resolves if permission is granted, otherwise, it is rejected with an error.

### sendMessage
[method]sendMessage(message) returns Promise containing void;[/method]

Sends a remote message upstream to your app server.

When there is an active connection the message will be sent immediately, otherwise the message will be queued up to the time to live (TTL) set in the message.

Returns a promise that resolves if the messages is sent, otherwise it is rejected with an error.

| Parameter |         |
| --------- | ------- |
| message   | **[ref messaging.RemoteMessage]** <br /> The remote message to send.  |

### subscribeToTopic
[method]subscribeToTopic(topic) returns Promise containing void;[/method]

Subscribes the device to a topic.

| Parameter |         |
| --------- | ------- |
| topic   | **string** The name of the topic to subscribe to. |

### unsubscribeFromTopic
[method]unsubscribeFromTopic(topic) returns Promise containing void;[/method]

Unsubscribes the device from a topic.

| Parameter |         |
| --------- | ------- |
| topic   | **string** The name of the topic to unsubscribe from. |
