# Displaying Notifications

When your app is in the foreground, you can choose to present a notification to the user.

> iOS 8 and 9 do not support displaying a notification whilst the app is in the foreground

## 1) Building a notification

React Native Firebase provides a [ref notifications.Notification] class which works as a builder to allow you to construct a notification.  This [ref notifications.Notification] class contains all the generic notification functionality that is shared between Android and iOS.

```js
const notification = new firebase.notifications.Notification()
  .setNotificationId('notificationId')
  .setTitle('My notification title')
  .setBody('My notification body')
  .setData({
    key1: 'value1',
    key2: 'value2',
  });
```

For the full set of shared parameters that can be set, please see the [ref notifications.Notification] reference docs.

### Android specific functionality

As Android provides some bespoke notification functionality, we have segregated this into an [ref notifications.AndroidNotification] class.  This is accessible on the notification you created above, as follows:

```js
notification
  .android.setChannelId('channelId')
  .android.setSmallIcon('ic_launcher');
```

For the full set of Android-specific parameters that can be set, please see the [ref notifications.AndroidNotification] reference docs.

### iOS specific functionality

As iOS provides some bespoke notification functionality, we have segregated this into an [ref notifications.IOSNotification] class.  This is accessible on the notification you created above, as follows:

```js
notification
  .ios.setBadge(2);
```

For the full set of iOS-specific parameters that can be set, please see the [ref notifications.IOSNotification] reference docs.

## 2) Display the notification

### (Android) Set up a notification channel

Before you can display a notification on Android, you must ensure you have created a Notification Channel, as explained [here](version /notifications/android-channels).

### Display the notification

```js
// Build notification as above
const notification = ...;
// Display the notification
firebase.notifications().displayNotification(notification)
```