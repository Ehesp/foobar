# AndroidNotification

Android specific notification settings.

## Properties

### autoCancel
[method]autoCancel returns nullable boolean;[/method]

Whether the notification should be automatically canceled when the user clicks it in the panel.

### badgeIconType
[method]badgeIconType returns nullable [ref notifications.AndroidBadgeIconType];[/method]

Which icon to display as a badge for this notification.

### category
[method]category returns nullable [ref notifications.AndroidCategory];[/method]

The notification's category.

### channelId
[method]channelId returns string;[/method]

The channel the notification should be delivered on.

### clickAction
[method]clickAction returns nullable string;[/method]

The action that should be triggered by the Intent when the notification is clicked on.

### color
[method]color returns nullable string;[/method]

The accent color to use.

### colorized
[method]colorized returns nullable boolean;[/method]

Whether the notification should be colorized.

### contentInfo
[method]color returns nullable string;[/method]

The large text at the right-hand side of the notification.

### defaults
[method]defaults returns nullable Array of [ref notifications.AndroidDefaults];[/method]

The default notification options that will be used.

### group
[method]group returns nullable string;[/method]

The group the notification should belong to.

### groupAlertBehaviour
[method]groupAlertBehaviour returns nullable [ref notifications.AndroidGroupAlert];[/method]

The group alert behaviour for this notification.

### groupSummary
[method]groupSummary returns nullable boolean;[/method]

If this notification should be used as the group summary.

### largeIcon
[method]largeIcon returns nullable string;[/method]

The large icon to use for the notification.

### lights
[method]lights returns nullable [ref notifications.AndroidLights];[/method]

The lights to use for the notification.

### localOnly
[method]localOnly returns nullable boolean;[/method]

If this notification is only relevant to the current device.

### number
[method]number returns nullable number;[/method]

The large number at the right-hand side of the notification.

### ongoing
[method]ongoing returns nullable boolean;[/method]

If this notification is an ongoing notification.

### onlyAlertOnce
[method]onlyAlertOnce returns nullable boolean;[/method]

If the sound, vibrate and ticker should be played if the notification is not already showing.

### progress
[method]progress returns nullable [ref notifications.AndroidProgress];[/method]

The progress of the notification.

### remoteInputHistory
[method]remoteInputHistory returns nullable Array of string;[/method]

The remote input history.

### shortcutId
[method]shortcutId returns nullable string;[/method]

The id of the shortcut this notification supersedes.

### showWhen
[method]showWhen returns nullable boolean;[/method]

If the `when` timestamp should be shown.

### smallIcon
[method]smallIcon returns nullable Object;[/method]

The small icon to display.

### sortKey
[method]sortKey returns nullable string;[/method]

The sort key used for ordering this notification.

### ticker
[method]ticker returns nullable string;[/method]

The ticker text for the notification.

### timeoutAfter
[method]ticker returns nullable number;[/method]

The time after which the notification should be cancelled.

### usesChronometer
[method]usesChronometer returns nullable boolean;[/method]

If the `when` field should be shown as a stopwatch.

### visibility
[method]visibility returns nullable [ref notifications.AndroidVisibility];[/method]

The visibility of the notification.

### when
[method]when returns nullable number;[/method]

A timestamp related to this notification, in milliseconds, since the epoch.

## Methods

### addAction
[method]addAction(action) returns [ref notifications.Notification];[/method]

Add an action to this notification. Actions are typically displayed by the system as a button adjacent to the notification content. 
Action buttons won't appear on platforms prior to Android 4.1.

| Parameter |         |
| --------- | ------- |
| action  | **[ref notification.AndroidAction]** |

### addPerson
[method]addPerson(person) returns [ref notifications.Notification];[/method]

Add a person that is relevant to this notification.

Depending on user preferences, this annotation may allow the notification to pass through interruption filters, and to appear more prominently in the user interface.

The person should be specified by the String representation of a CONTENT_LOOKUP_URI.

| Parameter |         |
| --------- | ------- |
| person  | **string** |

### setAutoCancel
[method]setAutoCancel(autoCancel) returns [ref notifications.Notification];[/method]

Setting this flag will make it so the notification is automatically canceled when the user clicks it in the panel.

| Parameter |         |
| --------- | ------- |
| autoCancel  | **boolean** |

### setBadgeIconType
[method]setBadgeIconType(badgeIconType) returns [ref notifications.Notification];[/method]

Sets which icon to display as a badge for this notification.

| Parameter |         |
| --------- | ------- |
| badgeIconType  | **[ref notifications.AndroidBadgeIconType]** |

### setCategory
[method]setCategory(category) returns [ref notifications.Notification];[/method]

Set the notification category.

Must be one of the predefined notification categories in [ref notifications.AndroidCategory] that best describes this notification. May be used by the system for ranking and filtering.

| Parameter |         |
| --------- | ------- |
| category  | **[ref notifications.AndroidCategory]** |

### setChannelId
[method]setChannelId(channelId) returns [ref notifications.Notification];[/method]

Specifies the channel the notification should be delivered on.

| Parameter |         |
| --------- | ------- |
| channelId  | **string** |

### setClickAction
[method]setClickAction(clickAction) returns [ref notifications.Notification];[/method]

Specifies the action that should be triggered by the Intent when the notification is clicked on.

| Parameter |         |
| --------- | ------- |
| clickAction  | **string** |

### setColor
[method]setColor(color) returns [ref notifications.Notification];[/method]

Sets the accent color to use.

| Parameter |         |
| --------- | ------- |
| color  | **string** |

### setColorized
[method]setColorized(colorized) returns [ref notifications.Notification];[/method]

Set whether this notification should be colorized. When set, the color set with `setColor(int)` will be used as the background color of this notification.

This should only be used for high priority ongoing tasks like navigation, an ongoing call, or other similarly high-priority events for the user.

For most styles, the coloring will only be applied if the notification is for a foreground service notification.

| Parameter |         |
| --------- | ------- |
| colorized  | **boolean** |

### setContentInfo
[method]setContentInfo(contentInfo) returns [ref notifications.Notification];[/method]

Set the large text at the right-hand side of the notification.

| Parameter |         |
| --------- | ------- |
| contentInfo  | **string** |

### setDefaults
[method]setDefaults(defaults) returns [ref notifications.Notification];[/method]

Set the default notification options that will be used.

The value should be one or more of the following fields combined: `Default.Sound`, `Default.Vibrate`, `Default.Lights`.

For all default values, use `Default.All`.

| Parameter |         |
| --------- | ------- |
| defaults  | **Array<[ref Notifications.AndroidDefaults]>** |

### setGroup
[method]setGroup(group) returns [ref notifications.Notification];[/method]

Set this notification to be part of a group of notifications sharing the same key. Grouped notifications may display in a cluster or stack on devices which support such rendering.

To make this notification the summary for its group, also call `setGroupSummary(boolean)`. A sort order can be specified for group members by using `setSortKey(String)`.

| Parameter |         |
| --------- | ------- |
| group  | **string** |

### setGroupAlertBehaviour
[method]setGroupAlertBehaviour(groupAlertBehaviour) returns [ref notifications.Notification];[/method]

Sets the group alert behaviour for this notification. Use this method to mute this notification if alerts for this notification's group should be handled by a different notification. This is only applicable for notifications that belong to a group. This must be called on all notifications you want to mute. For example, if you want only the summary of your group to make noise, all children in the group should have the group alert behavior `GroupAlert.Summary`.

The default value is `GroupAlert.All`.

| Parameter |         |
| --------- | ------- |
| groupAlertBehaviour  | **[ref notifications.AndroidGroupAlert]** |

### setGroupSummary
[method]setGroupSummary(groupSummary) returns [ref notifications.Notification];[/method]

Set this notification to be the group summary for a group of notifications. Grouped notifications may display in a cluster or stack on devices which support such rendering. Requires a group key also be set using `setGroup`.

| Parameter |         |
| --------- | ------- |
| groupSummary  | **boolean** |

### setLargeIcon
[method]setLargeIcon(largeIcon) returns [ref notifications.Notification];[/method]

Set the large icon that is shown in the ticker and notification.

| Parameter |         |
| --------- | ------- |
| largeIcon  | **string** |

### setLights
[method]setLights(argb, onMs, offMs) returns [ref notifications.Notification];[/method]

Set the argb value that you would like the LED on the device to blink, as well as the rate. The rate is specified in terms of the number of milliseconds to be on and then the number of milliseconds to be off.

| Parameter |         |
| --------- | ------- |
| argb  | **number** |
| onMs  | **number** |
| offMs | **number** |

### setLocalOnly
[method]setLocalOnly(localOnly) returns [ref notifications.Notification];[/method]

Set whether or not this notification is only relevant to the current device.

Some notifications can be bridged to other devices for remote display. This hint can be set to recommend this notification not be bridged.

| Parameter |         |
| --------- | ------- |
| localOnly  | **boolean** |

### setNumber
[method]setNumber(number) returns [ref notifications.Notification];[/method]

Set the large number at the right-hand side of the notification. This is equivalent to `setContentInfo`, although it might show the number in a different font size for readability.

| Parameter |         |
| --------- | ------- |
| number  | **number** |

### setOngoing
[method]setOngoing(ongoing) returns [ref notifications.Notification];[/method]

Set whether this is an ongoing notification.

Ongoing notifications differ from regular notifications in the following ways:

- Ongoing notifications are sorted above the regular notifications in the notification panel.
- Ongoing notifications do not have an 'X' close button, and are not affected by the "Clear all" button.

| Parameter |         |
| --------- | ------- |
| ongoing  | **boolean** |

### setOnlyAlertOnce
[method]setOnlyAlertOnce(onlyAlertOnce) returns [ref notifications.Notification];[/method]

Set this flag if you would only like the sound, vibrate and ticker to be played if the notification is not already showing.

| Parameter |         |
| --------- | ------- |
| onlyAlertOnce  | **boolean** |

### setPriority
[method]setPriority(priority) returns [ref notifications.Notification];[/method]

Set the relative priority for this notification. Priority is an indication of how much of the user's valuable attention should be consumed by this notification. Low-priority notifications may be hidden from the user in certain situations, while the user might be interrupted for a higher-priority notification. The system sets a notification's priority based on various factors including the setPriority value. The effect may differ slightly on different platforms.

| Parameter |         |
| --------- | ------- |
| priority  | **[ref notifications.AndroidPriority]** |

### setProgress
[method]setProgress(max, progress, indeterminate) returns [ref notifications.Notification];[/method]

Set the progress this notification represents, which may be represented as a ProgressBar.

| Parameter |         |
| --------- | ------- |
| max  | **number** |
| progress  | **number** |
| indeterminate  | **boolean** |

### setRemoteInputHistory
[method]setRemoteInputHistory(remoteInputHistory) returns [ref notifications.Notification];[/method]

Set the remote input history. This should be set to the most recent inputs that have been sent through a RemoteInput of this Notification and cleared once the it is no longer relevant (e.g. for chat notifications once the other party has responded). The most recent input must be stored at the 0 index, the second most recent at the 1 index, etc. Note that the system will limit both how far back the inputs will be shown and how much of each individual input is shown.

Note: The reply text will only be shown on notifications that have least one action with a RemoteInput.

| Parameter |         |
| --------- | ------- |
| remoteInputHistory  | **Array<string>** |

### setShortcutId
[method]setShortcutId(shortcutId) returns [ref notifications.Notification];[/method]

If this notification is duplicative of a Launcher shortcut, sets the id of the shortcut, in case the Launcher wants to hide the shortcut.

Note:This field will be ignored by Launchers that don't support badging or shortcuts.

| Parameter |         |
| --------- | ------- |
| shortcutId  | **string** |

### setShowWhen
[method]setShowWhen(showWhen) returns [ref notifications.Notification];[/method]

Control whether the timestamp set with `setWhen` is shown in the content view.

| Parameter |         |
| --------- | ------- |
| showWhen  | **boolean** |

### setSmallIcon
[method]setSmallIcon(icon, level) returns [ref notifications.Notification];[/method]

Set the small icon to use in the notification layouts. Different classes of devices may return different sizes. See the UX guidelines for more information on how to design these icons.

| Parameter |         |
| --------- | ------- |
| icon  | **string** |
| level | **number** (optional) |

### setSortKey
[method]setSortKey(sortKey) returns [ref notifications.Notification];[/method]

Set a sort key that orders this notification among other notifications from the same package. This can be useful if an external sort was already applied and an app would like to preserve this. Notifications will be sorted lexicographically using this value, although providing different priorities in addition to providing sort key may cause this value to be ignored.

This sort key can also be used to order members of a notification group. See `setGroup`.

| Parameter |         |
| --------- | ------- |
| sortKey  | **string** |

### setTicker
[method]setTicker(ticker) returns [ref notifications.Notification];[/method]

Sets the "ticker" text which is sent to accessibility services. Prior to `LOLLIPOP`, sets the text that is displayed in the status bar when the notification first arrives.

| Parameter |         |
| --------- | ------- |
| ticker  | **string** |

### setTimeoutAfter
[method]setTimeoutAfter(timeoutAfter) returns [ref notifications.Notification];[/method]

Specifies the time at which this notification should be canceled, if it is not already canceled.

| Parameter |         |
| --------- | ------- |
| timeoutAfter  | **number** |

### setUsesChronometer
[method]setUsesChronometer(usesChronometer) returns [ref notifications.Notification];[/method]

Show the `when` field as a stopwatch. Instead of presenting `when` as a timestamp, the notification will show an automatically updating display of the minutes and seconds since `when`. Useful when showing an elapsed time (like an ongoing phone call).

| Parameter |         |
| --------- | ------- |
| usesChronometer  | **boolean** |

### setVibrate
[method]setVibrate(vibrate) returns [ref notifications.Notification];[/method]

Set the vibration pattern to use.

On some platforms, a notification that vibrates is more likely to be presented as a heads-up notification.

| Parameter |         |
| --------- | ------- |
| vibrate  | **Array<number>** |

### setVisibility
[method]setVisibility(visibility) returns [ref notifications.Notification];[/method]

Sets `visibility`, which affects how and when the SystemUI reveals the notification's presence and contents in untrusted situations (namely, on the secure lockscreen). The default level, `Visibility.Private`, behaves exactly as notifications have always done on Android: The notification's icon and tickerText (if available) are shown in all situations, but the contents are only available if the device is unlocked for the appropriate user. A more permissive policy can be expressed by `Visibility.Public`; such a notification can be read even in an "insecure" context (that is, above a secure lockscreen). To modify the public version of this notification—for example, to redact some portions—see setPublicVersion(Notification). Finally, a notification can be made `Visibility.Secret`, which will suppress its icon and ticker until the user has bypassed the lockscreen.

| Parameter |         |
| --------- | ------- |
| visibility  | **[ref notifications.AndroidVisibility]** |

### setWhen
[method]setWhen(when) returns [ref notifications.Notification];[/method]

Set the time that the event occurred, in milliseconds sine the epoch. Notifications in the panel are sorted by this time.

Choose a timestamp that will be most relevant to the user. For most finite events, this corresponds to the time the event happened (or will happen, in the case of events that have yet to occur but about which the user is being informed). Indefinite events should be timestamped according to when the activity began. Some examples:

- Notification of a new chat message should be stamped when the message was received.
- Notification of an ongoing file download (with a progress bar, for example) should be stamped when the download started.
- Notification of a completed file download should be stamped when the download finished.
- Notification of an upcoming meeting should be stamped with the time the meeting will begin (that is, in the future).
- Notification of an ongoing stopwatch (increasing timer) should be stamped with the watch's start time.
- Notification of an ongoing countdown timer should be stamped with the timer's end time.

| Parameter |         |
| --------- | ------- |
| when  | **number** |
