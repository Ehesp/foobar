# Notification

```
firebase.notifications.Notification
```

### Notification
[method]new Notification();[/method]

A Notification can be displayed instantly or scheduled to be displayed at some point in the future.

To display a Notification, first populate it by using the `setX` methods described below, then pass it to `firebase.notifications().displayNotification(notification)` or `firebase.notifications().scheduleNotification(notification, schedule)`;

## Properties

### android
[method]android returns [ref notifications.AndroidNotification];[/method]

Gets the Android specific properties of the notification.

### body
[method]body returns string;[/method]

Gets the body of the notification.

### data
[method]data returns Object;[/method]

Gets the custom data associated with the notification.

### ios
[method]ios returns [ref notifications.IOSNotification];[/method]

Gets the iOS specific properties of the notification.

### notificationId
[method]collapseKey returns string;[/method]

Gets the ID of the notification.

### sound
[method]sound returns nullable string;[/method]

Gets the optional sound of the notification.

### subtitle
[method]subtitle returns nullable string;[/method]

Gets the optional subtitle of the notification.

### title
[method]title returns string;[/method]

Gets the title of the notification.

## Methods

### setBody
[method]setBody(body) returns [ref notifications.Notification];[/method]

Sets the body for the notification.

| Parameter |         |
| --------- | ------- |
| body  | **string** <br /> The body. |

### setData
[method]setData(data) returns [ref notifications.Notification];[/method]

Sets the custom data for the notification.

| Parameter |         |
| --------- | ------- |
| data  | **Object** <br /> The custom data. |

### setNotificationId
[method]setNotificationId(notificationId) returns [ref notifications.Notification];[/method]

Sets the ID for the notification.

| Parameter |         |
| --------- | ------- |
| notificationId  | **string** <br /> The notification's ID. |

### setSound
[method]setSound(sound) returns [ref notifications.Notification];[/method]

Sets the sound for the notification.

| Parameter |         |
| --------- | ------- |
| sound  | **string** <br /> The sound. |

### setSubtitle
[method]setSubtitle(subtitle) returns [ref notifications.Notification];[/method]

Sets the subtitle for the notification.

| Parameter |         |
| --------- | ------- |
| subtitle  | **string** <br /> The subtitle. |
