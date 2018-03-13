# Notifications

This `notifications` module deals with Notification and Notification + Data messages.  If you're interested in sending and receiving just data messages, please take a look at the [ref messaging.Messaging] module.

!> On iOS, your app first needs to [ref Messaging#requestPermission] in order to receive Notifications.

## Properties

### android
[method]android returns [ref notifications.AndroidNotifications];[/method]

Access Android specific notification methods.

## Methods

The following methods are accessed via the Notifications instance `firebase.notifications()`.

### cancelAllNotifications
[method]cancelAllNotifications() returns void;[/method]

Cancels all pending notifications.

### cancelNotification
[method]cancelNotification(notificationId) returns void;[/method]

Cancels a pending notification with the specified ID.

| Parameter |         |
| --------- | ------- |
| notificationId   | **string** <br /> The ID of the notification to be cancelled. |

### displayNotification
[method]displayNotification(notification) returns Promise;[/method]

Displays the specified notification straight away.

!> It is not possible to display a notification whilst the app is in the foreground on iOS 8 and 9.

Returns a promise that resolves if the notification is displayed, otherwise it is rejected with an error.

| Parameter |         |
| --------- | ------- |
| notification   | **[ref notifications.Notification]** <br /> The notification to display.  |

### getBadge
[method]getBadge() returns Promise containing number;[/method]

Returns the current badge number on the app icon.

!> On Android, we make use of the ShortcutBadger library to display badges.

### getInitialNotification
[method]getInitialNotification() returns Promise containing nullable [ref notifications.NotificationOpen];[/method]

Due to the delay in the React Native bridge, the `onNotification` listeners will not be available at startup, so this method can be used to check to see if the application was opened by a notification.

For notifications when the app is running, see [ref notifications#onNotification], [ref notifications#onNotificationDisplayed] and [ref notifications#onNotificationOpened].

Returns the notification that caused the application to open if available, and the action that was invoked when it was clicked on.

### getScheduledNotifications
[method]getScheduledNotifications() returns Promise containing Array of [ref notifications.Notification];[/method]

Returns an array of all scheduled notifications.

### onNotification
[method]onNotification(nextOrObserver) returns function();[/method]

When a notification is received, but not displayed, the listener is invoked with the notification.

Returns an unsubscribe function.

Parameter |         |
| --------- | ------- |
| nextOrObserver   | **function([ref notifications.Notification])** or **Object** <br /> This function, or observer object with `next` defined, is called when a notification is received but not displayed. |

### onNotificationDisplayed
[method]onNotificationDisplayed(nextOrObserver) returns function();[/method]

When a notification is displayed, the listener is invoked with the notification.

Returns an unsubscribe function.

Parameter |         |
| --------- | ------- |
| nextOrObserver   | **function([ref notifications.Notification])** or **Object** <br /> This function, or observer object with `next` defined, is called when a notification is displayed. |

### onNotificationOpened
[method]onNotificationOpened(nextOrObserver) returns function();[/method]

When a notification is opened, the listener is invoked with the notification and the action that was invoked when it was clicked on.

Returns an unsubscribe function.

Parameter |         |
| --------- | ------- |
| nextOrObserver   | **function([ref notifications.NotificationOpen])** or **Object** <br /> This function, or observer object with `next` defined, is called when a notification is opened. |

### removeAllDeliveredNotifications
[method]removeAllDeliveredNotifications() returns void;[/method]

Removes all delivered notifications.

### removeDeliveredNotification
[method]removeDeliveredNotification(notificationId) returns void;[/method]

Removes a delivered notification with the specified ID.

| Parameter |         |
| --------- | ------- |
| notificationId   | **string** <br /> The ID of the notification to be removed. |

### scheduleNotification
[method]scheduleNotification(notification, schedule) returns Promise;[/method]

Displays the specified notification according to the supplied schedule.

!> It is not possible to display a notification whilst the app is in the foreground on iOS 8 and 9.

Returns a promise that resolves if the notification is scheduled, otherwise it is rejected with an error.

| Parameter |         |
| --------- | ------- |
| notification   | **[ref notifications.Notification]** <br /> The notification to display.  |
| schedule   | **[ref notifications.Schedule]** <br /> The schedule to control when the notification is displayed.  |

### setBadge
[method]setBadge(badge) returns void;[/method]

Sets the current badge number on the app icon.

!> On Android, we make use of the ShortcutBadger library to display badges.

| Parameter |         |
| --------- | ------- |
| badge   | **number** <br /> The badge number to display. |
