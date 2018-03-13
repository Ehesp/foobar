# AndroidRemoteInput

```
firebase.notifications.Android.RemoteInput
```

See the official [Android docs](https://developer.android.com/training/notify-user/build-notification.html#reply-action) for more information about Remote Input.

### Constructor
[method]new firebase.notifications.Android.RemoteInput(resultKey);[/method]

A RemoteInput object specifies input to be collected from a user to be passed along with an intent inside a PendingIntent that is sent. 

| Parameter |         |
| --------- | ------- |
| resultKey    | **string** |

## Properties

### allowedDataTypes
[method]allowedDataTypes returns Array of Object;[/method]

The data types this remote input supports.

### allowFreeFormInput
[method]allowFreeFormInput returns nullable boolean;[/method]

Get whether or not users can provide an arbitrary value for input.

### choices
[method]choices returns Array of string;[/method]

Get possible input choices.

### label
[method]choices returns nullable string;[/method]

Get the label to display to users when collecting this input.

### resultKey
[method]resultKey returns string;[/method]

Get the key that the result of this input will be set in the [ref notifications.NotificationOpened] `results` object.

## Methods

### setAllowDataType
[method]setAllowDataType(mimeType, allow) returns [ref notifications.AndroidRemoteInput];[/method]

| Parameter |         |
| --------- | ------- |
| mimeType  | **string** |
| allow  | **boolean** |

Specifies whether the user can provide arbitrary values.

### setAllowFreeFormInput
[method]setAllowFreeFormInput(allowFreeFormInput) returns [ref notifications.AndroidRemoteInput];[/method]

| Parameter |         |
| --------- | ------- |
| allowFreeFormInput  | **boolean** |

Specifies whether the user can provide arbitrary text values.

### setChoices
[method]setChoices(choices) returns [ref notifications.AndroidRemoteInput];[/method]

| Parameter |         |
| --------- | ------- |
| choices  | **Array<string>** |

Specifies choices available to the user to satisfy this input.

### setLabel
[method]setLabel(label) returns [ref notifications.AndroidRemoteInput];[/method]

| Parameter |         |
| --------- | ------- |
| label  | **string** |

Set a label to be displayed to the user when collecting this input.
