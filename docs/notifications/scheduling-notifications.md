# Scheduling Notifications

Both Android and iOS allow notifications to be scheduled to display at some point in the future.

## 1) Building a notification

To build a notification, follow the [Displaying Notifications Guide](version /notifications/displaying-notifications).

## 2) Scheduling the notification

### (Android) Set up a notification channel

Before you can schedule a notification on Android, you must ensure you have created a Notification Channel, as explained [here](version /notifications/android-channels).

### Schedule the notification

```js
// Build notification
const notification = new firebase.notifications.Notification()...;

// Schedule the notification for 1 minute in the future
const date = new Date();
date.setMinutes(date.getMinutes() + 1);

firebase.notifications().scheduleNotification(notification, {
    fireDate: date.getTime(),
})
```

For full reference documentation, please see [ref notifications.Notifications#scheduleNotification].