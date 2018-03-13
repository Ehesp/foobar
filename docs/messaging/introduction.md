# Introduction to Firebase Cloud Messaging

Firebase Cloud Messaging (FCM) offers a broad range of messaging options and capabilities. The information in this page is intended to help you understand the different types of FCM messages and what you can do with them in React Native Firebase.

To try and keep things simple and easier to understand, we have divided the React Native Firebase functionality clearly between data-only and notification messages.

> The React Native Firebase Messaging Module deals exclusively with data-only messages. <br /> <br/> For notification-only and notification + data FCM messages please see the [Notifications module](version /notifications/introduction).

## Message types

With FCM, you can send two types of messages to clients:

- Notification messages, sometimes thought of as "display messages." These are handled by the FCM SDK automatically.
- Data messages, which are handled by the client app.

Notification messages contain a predefined set of user-visible keys. Data messages, by contrast, contain only your user-defined custom key-value pairs. Notification messages can contain an optional data payload. Maximum payload for both message types is 4KB, except when sending messages from the Firebase console, which enforces a 1024 character limit.

|                      | Use scenario | How to send |
| -------------------- | ------------ | ----------- |
| Data message         | Client app is responsible for processing data messages. Data messages have only custom key-value pairs. | In a trusted environment such as Cloud Functions or your app server, use the Admin SDK or the FCM Server Protocols: Set the data key only. |
| Notification message | FCM automatically displays the message to end-user devices on behalf of the client app. | 1. In a trusted environment such as Cloud Functions or your app server, use the Admin SDK or the FCM Server Protocols: Set the notification key. May have optional data payload. Always collapsible. <br /><br /> 2. Use the Notifications composer: Enter the Message Text, Title, etc., and send. Add optional data payload by providing Custom data. |

Use notification messages when you want FCM to handle displaying a notification on your client app's behalf. Use data messages when you want to process the messages on your client app.

FCM can send a notification message including an optional data payload. In such cases, FCM handles displaying the notification payload, and the client app handles the data payload.

### Data-only messages

- Handled by the RNFirebase Messaging module.
- Contain a data payload (map of key / value pairs) for consumption by the app. 
- Do not display any visible notification.
- Never intercepted by the Mobile Device's OS.
- Behave as follows:

|         | App in foreground           | App in background            | App closed |
| ------- | --------------------------- | ---------------------------- | -----------|
| Android | `onMessage` triggered | [Background Handler](version /messaging/receiving-messages) | [Background Handler](version /messaging/receiving-messages) |
| iOS     | `onMessage` triggered | `onMessage` triggered if `content_available` set to `true` | Received when app is next opened |


### Notification-only and Notification + Data messages

- Handled by the RNFirebase [Notifications module](version /notifications/introduction).
- Used to display a visible notification on devices.
- Contain an optional data payload (map of key / value pairs) for consumption by the app if it is in the foreground, or if the notification is subsequently opened.  **If the notification is not opened, this data will never become available to the app.**
- Intercepted by the Mobile Device's OS.
- Delivered to the notification tray when the app is in the background or closed.
- Behaviour is defined in the [Notifications module](version /notifications/introduction).
