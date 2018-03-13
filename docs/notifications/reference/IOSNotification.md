# IOSNotification

iOS specific notification settings.

> Some of these settings apply only to iOS 8/9, or iOS 10+.  These are flagged as appropriate.

## Properties

### alertAction
[method]alertAction returns nullable string;[/method]

Gets the alert action of the notification.

> iOS 8 and 9 only.

### attachments
[method]attachments returns Array of [ref notifications.IOSAttachment];[/method]

Gets the attachments for the notification.

> iOS 10+.

### badge
[method]badge returns nullable string;[/method]

Gets the optional badge for the notification.

### category
[method]category returns nullable string;[/method]

Gets the optional category for the notification.

### hasAction
[method]alertAction returns nullable boolean;[/method]

Gets whether the notification has an action or not.

> iOS 8 and 9 only.

### launchImage
[method]launchImage returns nullable string;[/method]

Gets the launch image to use with the notification.

### threadIdentifier
[method]threadIdentifier returns nullable string;[/method]

Gets the optional thread ID for the notification.

> iOS 10+.

## Methods

### addAttachment
[method]addAttachment(identifier, url, options) returns [ref notifications.Notification];[/method]

Adds an attachment to the notification.

> iOS 10+.

| Parameter |         |
| --------- | ------- |
| identifier  | **string** <br /> The ID for the attachment. |
| url  | **string** <br /> The URL for the attachment. |
| options  | **[ref Notifications.IOSAttachmentOptions]** (optional) <br /> The options for the attachment. |

### setAlertAction
[method]setAlertAction(alertAction) returns [ref notifications.Notification];[/method]

Sets the alert action for the notification.

> iOS 8 and 9 only.

| Parameter |         |
| --------- | ------- |
| alertAction  | **string** <br /> The alert action. |

### setBadge
[method]setBadge(badge) returns [ref notifications.Notification];[/method]

Sets the badge for the notification.

| Parameter |         |
| --------- | ------- |
| badge  | **number** <br /> The badge. |

### setCategory
[method]setCategory(category) returns [ref notifications.Notification];[/method]

Sets the category for the notification.

| Parameter |         |
| --------- | ------- |
| alertAction  | **string** <br /> The alert action. |

### setHasAction
[method]setHasAction(hasAction) returns [ref notifications.Notification];[/method]

Sets whether the notification has an action.

> iOS 8 and 9 only.

| Parameter |         |
| --------- | ------- |
| hasAction  | **boolean** |

### setLaunchImage
[method]setLaunchImage(launchImage) returns [ref notifications.Notification];[/method]

Sets the launch image for the notification.

| Parameter |         |
| --------- | ------- |
| launchImage  | **string** <br /> The launch image. |

### setThreadIdentifier
[method]setThreadIdentifier(threadIdentifier) returns [ref notifications.Notification];[/method]

Sets the thread ID for the notification.

> iOS 10+.

| Parameter |         |
| --------- | ------- |
| threadIdentifier  | **string** <br /> The thread ID. |