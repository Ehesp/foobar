# Android Actions

Actions allow users to interact with a notification, for example, by pressing a button or entering text.

## Adding a custom button

```js

// Set up your listener
firebase.notifications().onNotificationOpened((notificationOpen) => {
    // notificationOpen.action will equal 'test_action'
});

// Build your notification
const notification = new firebase.notifications.Notification()
  .setTitle('Android Notification Actions')
  .setBody('Action Body')
  .setNotificationId('notification-action')
  .setSound('default')
  .android.setChannelId('notification-action')
  .android.setPriority(firebase.notifications.Android.Priority.Max);
// Build an action
const action = new firebase.notifications.Android.Action('test_action', 'ic_launcher', 'My Test Action');
// Add the action to the notification
notification.android.addAction(action);

// Display the notification
firebase.notifications().displayNotification(notification);
```

For full reference documentation, please see [ref notifications.AndroidAction].

## Adding a text input

```js

// Set up your listener
firebase.notifications().onNotificationOpened((notificationOpen) => {
    // notificationOpen.results.inputText will contain the text entered by the user
});

// Build your notification
const notification = new firebase.notifications.Notification()
  .setTitle('Android Notification Actions')
  .setBody('Action Body')
  .setNotificationId('notification-action')
  .setSound('default')
  .android.setChannelId('notification-action')
  .android.setPriority(firebase.notifications.Android.Priority.Max);
// Build an action
const action = new firebase.notifications.Android.Action('test_action', 'ic_launcher', 'My Test Action');

// Build a remote input
const remoteInput = new RNfirebase.notifications.Android.RemoteInput('inputText')
  .setLabel('Message');

// Add the remote input to the action
action.addRemoteInput(remoteInput);
  
// Add the action to the notification
notification.android.addAction(action);

// Display the notification
firebase.notifications().displayNotification(notification);
```

## Performing the action in the background

By default, the action will cause your application to open and come to the foreground.  If you'd like to override this behaviour, for example, to support a `snooze` action then you need to follow these steps.

> If the app is already in the foreground then the action will still need to be handled in the normal `onNotificationOpened` listener

### 1) Update `AndroidManifest.xml`

If you would like to schedule local notifications then you also need to add the following to the application component of `android/app/src/main/AndroidManifest.xml`:

```xml
<application ...>
  <receiver android:name="io.invertase.firebase.notifications.RNFirebaseBackgroundNotificationActionReceiver" android:exported="true">
    <intent-filter>
      <action android:name="io.invertase.firebase.notifications.BackgroundAction"/>
    </intent-filter>
  </receiver>
  <service android:name="io.invertase.firebase.notifications.RNFirebaseBackgroundNotificationActionsService"/>
</application>
```

### 2) Handle background actions

Create a new Javascript file (for this example we'll call it `bgActions.js`) which has the following structure:

```js
// @flow
import firebase from 'react-native-firebase';
// Optional flow type
import type { NotificationOpen } from 'react-native-firebase';

export default async (notificationOpen: NotificationOpen) => {
    if (notificationOpen.action === 'snooze') {
        // handle the action
    }
    
    return Promise.resolve();
}
```

> This handler method must return a promise and resolve within 60 seconds.

### 3) Register the background handler

In your main `index.js` you need to register your background handler as follows:

```js
import bgActions from './src/bgActions'; // <-- Import the file you created in (2)

// Current main application
AppRegistry.registerComponent('ReactNativeFirebaseDemo', () => bootstrap);
// New task registration
AppRegistry.registerHeadlessTask('RNFirebaseBackgroundNotificationAction', () => bgActions); // <-- Add this line
```

### 4) Create your action with `showUserInterface` false

```js

// Set up your listener
firebase.notifications().onNotificationOpened((notificationOpen) => {
    // notificationOpen.action will equal 'snooze'
});

// Build your notification
const notification = new firebase.notifications.Notification()
  .setTitle('Android Notification Actions')
  .setBody('Action Body')
  .setNotificationId('notification-action')
  .setSound('default')
  .android.setChannelId('notification-action')
  .android.setPriority(firebase.notifications.Android.Priority.Max);
// Build an action
const action = new firebase.notifications.Android.Action('snooze', 'ic_launcher', 'My Test Action');
// This is the important line
action.setShowUserInterface(false);
// Add the action to the notification
notification.android.addAction(action);

// Display the notification
firebase.notifications().displayNotification(notification);
```