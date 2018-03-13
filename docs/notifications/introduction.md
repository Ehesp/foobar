# Introduction to Notifications

React Native Firebase's Notifications module has support for both remote (FCM) and local notifications.

## Remote Notifications

Firebase Cloud Messaging (FCM) allows notifications to be displayed by your application remotely.  To try and keep things simple and easier to understand, we have divided the React Native Firebase functionality clearly between data-only and notification messages.

Remote notifications:

- Used to display a visible notification on devices.
- Contain an optional data payload (map of key / value pairs) for consumption by the app if it is in the foreground, or if the notification is subsequently opened.  **If the notification is not opened, this data will never become available to the app.**
- Intercepted by the Mobile Device's OS.
- Delivered to the notification tray when the app is in the background or closed.

> The React Native Firebase Notifications Module deals with notification-only and notification + data FCM remote messages. <br /> <br/> For data-only FCM messages please see the [Messaging module](version /messaging/introduction).

Remote notifications behave as follows:

|         | App in foreground           | App in background            | App closed |
| ------- | --------------------------- | ---------------------------- | -----------|
| Android | `onNotification` triggered | `onNotificationOpened` triggered if the notification is tapped | `getInitialNotification` is populated if the notification is tapped and opens the app |
| iOS     | `onNotification` triggered | `onNotificationDisplayed` triggered if `content_available` set to `true` <br /><br />`onNotificationOpened` triggered if the notification is tapped | `getInitialNotification` is populated if the notification is tapped and opens the app |
| Notes   | No visible notification is shown to the user, it is up to you to display notifications manually | The notification is presented to the user by the Mobile Device's OS | The notification is presented to the user by the Mobile Device's OS |

## Local Notifications

Both Android and IOS support the ability to trigger notifications from your application locally.  These can either be displayed immediately, or scheduled to be displayed at a later date.

The notifications module handles all local notifications.

Scheduled notifications behave as follows:

|         | App in foreground           | App in background            | App closed |
| ------- | --------------------------- | ---------------------------- | -----------|
| Android | `onNotification` triggered | `onNotificationOpened` triggered if the notification is tapped | `getInitialNotification` is populated if the notification is tapped and opens the app |
| iOS     | `onNotification` triggered | `onNotificationOpened` triggered if the notification is tapped | `getInitialNotification` is populated if the notification is tapped and opens the app |
| Notes   | No visible notification is shown to the user, it is up to you to display notifications manually | The notification is presented to the user by the Mobile Device's OS | The notification is presented to the user by the Mobile Device's OS |

