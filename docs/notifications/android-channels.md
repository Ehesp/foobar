# Android Notification Channels

As of Android 8.0 (API Level 26), notifications must specify a [Notification Channel](https://developer.android.com/guide/topics/ui/notifiers/notifications.html#ManageChannels) or they will not appear.  

To allow React Native Firebase to work seamlessly across all versions of Android, you will need to create a channel before you can display a notification.  This block of code can be re-run multiple times, so it is safe to do it each time your application starts.

## Creating a Notification Channel

```js
// Build a channel
const channel = new firebase.notifications.Android.Channel()
  .setChannelId('test-channel')
  .setName('Test Channel')
  .setImportance(firebase.notifications.Android.Importance.Max)
  .setDescription('My apps test channel');
  
// Create the channel
firebase.notifications().android.createChannel(channel);
```

For full reference documentation, please see [ref notifications.AndroidChannel] and [ref notifications.AndroidNotifications].

## Creating a Notification Channel Group

React Native Firebase also supports the concept of [Notification Channel Groups](https://developer.android.com/training/notify-user/channels.html#CreateChannelGroup).

```js
// Build a channel group
const channelGroup = new firebase.notifications.Android.ChannelGroup()
  .setGroupId('test-group')
  .setName('Test Channel Group');

// Create the channel group
firebase.notifications().android.createChannelGroup(channelGroup);
```

For full reference documentation, please see [ref notifications.AndroidChannelGroup] and [ref notifications.AndroidNotifications].