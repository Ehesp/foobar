# AndroidGroupAlert

```
firebase.notifications.Android.GroupAlert
```

## Constants

### All

Constant for `setGroupAlertBehaviour`, meaning that all notifications in a group with sound or vibration ought to make sound or vibrate (respectively), so this notification will not be muted when it is in a group.

```
firebase.notifications.Android.GroupAlert.All
```

### Children

Constant for `setGroupAlertBehaviour`, meaning that the summary notification in a group should be silenced (no sound or vibration) even if they would otherwise make sound or vibrate. Use this constant to mute this notification if this notification is a group summary.

For example, you might want to use this constant if only the children notifications in your group have content and the summary is only used to visually group notifications rather than to alert the user that new information is available.

```
firebase.notifications.Android.GroupAlert.Children
```

### Summary

Constant for `setGroupAlertBehaviour`, meaning that all children notification in a group should be silenced (no sound or vibration) even if they would otherwise make sound or vibrate. Use this constant to mute this notification if this notification is a group child. This must be applied to all children notifications you want to mute.

For example, you might want to use this constant if you post a number of children notifications at once (say, after a periodic sync), and only need to notify the user audibly once.
    
```
firebase.notifications.Android.GroupAlert.Summary
```