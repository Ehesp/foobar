# NotificationOpen

Object giving information about the action that was taken when a specific notification was opened.

## Properties

### action
[method]action returns string;[/method]

The action that was used when the notification was opened.

### notification
[method]notification returns [ref notifications.Notification];[/method]

Information about the notification that was opened.

### results
[method]results returns nullable Object;[/method]

If the notification contains a [ref notifications.AndroidRemoteInput] then this object will be populated with the user's input.

> Android only
