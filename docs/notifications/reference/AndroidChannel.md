# AndroidChannel

```
firebase.notifications.Android.Channel
```

### Constructor
[method]new firebase.notifications.Android.Channel(channelId, name, importance);[/method]

A representation of settings that apply to a collection of similarly themed notifications.

| Parameter |         |
| --------- | ------- |
| channelId | **string** |
| name      | **string** |
| importance | **[ref notifications.AndroidImportance]** |

## Properties

### bypassDnd
[method]android returns nullable boolean;[/method]

Whether or not notifications posted to this channel can bypass the Do Not Disturb INTERRUPTION_FILTER_PRIORITY mode.

### channelId
[method]channelId returns string;[/method]

The id of this channel.

### description
[method]description returns nullable string;[/method]

The user visible description of this channel.

### group
[method]group returns nullable string;[/method]

What group this channel belongs to.

### importance
[method]importance returns [ref notifications.AndroidImportance];[/method]

The user specified importance.

### lightColor
[method]lightColor returns nullable string;[/method]

The notification light color for notifications posted to this channel.

### lockScreenVisibility
[method]lockScreenVisibility returns nullable [ref notifications.AndroidVisibility];[/method]

Whether or not notifications posted to this channel are shown on the lockscreen in full or redacted form.

### name
[method]name returns string;[/method]

The user visible name of this channel.

### showBadge
[method]showBadge returns nullable boolean;[/method]

Whether notifications posted to this channel can appear as badges in a Launcher application.

### sound
[method]sound returns nullable string;[/method]

The notification sound for this channel.

### vibrationPattern
[method]vibrationPattern returns nullable Array of number;[/method]

The vibration pattern for notifications posted to this channel.

## Methods

### setBypassDnd
[method]setBypassDnd(bypassDnd) returns [ref notifications.AndroidChannel];[/method]

| Parameter |         |
| --------- | ------- |
| bypassDnd  | **boolean** |

Sets whether or not notifications posted to this channel can interrupt the user in INTERRUPTION_FILTER_PRIORITY mode.

### setDescription
[method]setDescription(description) returns [ref notifications.AndroidChannel];[/method]

| Parameter |         |
| --------- | ------- |
| description  | **string** |

Sets the user visible description of this channel.

### setGroup
[method]setGroup(groupId) returns [ref notifications.AndroidChannel];[/method]

| Parameter |         |
| --------- | ------- |
| groupId  | **string** |

Sets what group this channel belongs to.

### setLightColor
[method]setLightColor(lightColor) returns [ref notifications.AndroidChannel];[/method]

| Parameter |         |
| --------- | ------- |
| lightColor  | **string** |

Sets the notification light color for notifications posted to this channel, if lights are enabled on this channel and the device supports that feature.

### setLockScreenVisibility
[method]setLockScreenVisibility(lockScreenVisibility) returns [ref notifications.AndroidChannel];[/method]

| Parameter |         |
| --------- | ------- |
| lockScreenVisibility  | **[ref notifications.AndroidVisibility]** |

Sets whether notifications posted to this channel appear on the lockscreen or not, and if so, whether they appear in a redacted form.

### setShowBadge
[method]setShowBadge(showBadge) returns [ref notifications.AndroidChannel];[/method]

| Parameter |         |
| --------- | ------- |
| showBadge  | **boolean** |

Sets whether notifications posted to this channel can appear as application icon badges in a Launcher.

### setSound
[method]setSound(sound) returns [ref notifications.AndroidChannel];[/method]

| Parameter |         |
| --------- | ------- |
| sound  | **string** |

Sets the sound that should be played for notifications posted to this channel.

### setVibrationPattern
[method]setVibrationPattern(vibrationPattern) returns [ref notifications.AndroidChannel];[/method]

| Parameter |         |
| --------- | ------- |
| vibrationPattern  | **Array<number>** |

Sets the vibration pattern for notifications posted to this channel.