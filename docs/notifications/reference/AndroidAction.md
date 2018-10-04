# AndroidAction

```
firebase.notifications.Android.Action
```

See the official [Android docs](https://developer.android.com/training/notify-user/build-notification.html#Actions) for more information about Actions.

### Constructor
[method]new firebase.notifications.Android.Action(action, icon, title);[/method]

Structure to encapsulate a named action that can be shown as part of this notification. It must include an icon, a label, and a PendingIntent to be fired when the action is selected by the user. Action buttons won't appear on platforms prior to Android 4.1.

| Parameter |         |
| --------- | ------- |
| action    | **string** |
| icon      | **string** |
| title     | **string** |

## Properties

### action
[method]action returns string;[/method]

The name of the action.

### allowGeneratedReplies
[method]allowGeneratedReplies returns nullable boolean;[/method]

Return whether the platform should automatically generate possible replies for this action.

### icon
[method]icon returns string;[/method]

The icon to use for this action.

### remoteInputs
[method]remoteInputs returns Array of [ref notifications.AndroidRemoteInput];[/method]

Get the list of inputs to be collected from the user when this action is sent.

### semanticAction
[method]icon returns nullable [ref notifications.AndroidSemanticAction];[/method]

Returns the semantic action associated with this action.

### showUserInterface
[method]showUserInterface returns nullable boolean;[/method]

Return whether or not triggering this action will open a user interface.

### title
[method]title returns string;[/method]

The title for this action.

## Methods

### addRemoteInput
[method]addRemoteInput(remoteInput) returns [ref notifications.AndroidAction];[/method]

| Parameter |         |
| --------- | ------- |
| remoteInput  | **[ref notifications.AndroidRemoteInput]** |

Add an input to be collected from the user when this action is sent.

### setAllowGenerateReplies
[method]setAllowGenerateReplies(allowGeneratedReplies) returns [ref notifications.AndroidAction];[/method]

| Parameter |         |
| --------- | ------- |
| allowGeneratedReplies  | **boolean** |

Set whether the platform should automatically generate possible replies to add to getChoices().

### setSemanticAction
[method]setSemanticAction(semanticAction) returns [ref notifications.AndroidAction];[/method]

| Parameter |         |
| --------- | ------- |
| semanticAction  | **[ref notifications.AndroidSemanticAction]** |

Sets the SemanticAction for this action.

### setShowUserInterface
[method]setShowUserInterface(showUserInterface) returns [ref notifications.AndroidAction];[/method]

| Parameter |         |
| --------- | ------- |
| showUserInterface  | **boolean** |

Set whether or not this action will open the user interface. Defaults to true.
