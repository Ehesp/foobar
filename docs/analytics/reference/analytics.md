# Analytics

```
firebase.analytics
```

## Methods

The following methods are accessed via the Analytics instance `firebase.analytics()`.

### logEvent
[method]logEvent(event, params) returns void;[/method]

Log a custom event with optional params.
Note: up to 100 characters is the maximum character length supported for event parameters.

| Parameter |         |
| --------- | ------- |
| event   | **string**  |
| params   | **object**  |

### setAnalyticsCollectionEnabled
[method]setAnalyticsCollectionEnabled(enabled) returns void;[/method]

If true, allows the device to collect analytical data and send it to Firebase.

| Parameter |         |
| --------- | ------- |
| enabled   | **boolean**  |

### setCurrentScreen
[method]setCurrentScreen(screenName, screenClassOverride) returns void;[/method]

Sets the current screen name.

?> Whilst `screenClassOverride` is optional, it is recommended it is always sent as your current class name, for example on Android it will always show as 'MainActivity' if not specified.

| Parameter |         |
| --------- | ------- |
| screenName   | **string**  |
| screenClassOverride   | **string** (optional)  |

### setMinimumSessionDuration
[method]setMinimumSessionDuration(miliseconds) returns void;[/method]

Sets the minimum engagement time required before starting a session. The default value is 10000 (10 seconds).

| Parameter |         |
| --------- | ------- |
| miliseconds   | **number**  |

### setSessionTimeoutDuration
[method]setSessionTimeoutDuration(miliseconds) returns void;[/method]

Sets the duration of inactivity that terminates the current session. The default value is 1800000 (30 minutes).

| Parameter |         |
| --------- | ------- |
| miliseconds   | **number**  |

### setUserId
[method]setUserId(id) returns void;[/method]

Gives a user a unique identification.

| Parameter |         |
| --------- | ------- |
| id   | **string**  |

### setUserProperty
[method]setUserProperty(name, value) returns void;[/method]

Sets a key/value pair of data on the current user.

| Parameter |         |
| --------- | ------- |
| name   | **string**  |
| value   | **string**  |

### setUserProperties
[method]setUserProperties(fieldMapping) returns void;[/method]

Sets mutiple key/value pair of data on the current user.
Param object's keys are property value and values are values.


| Parameter |         |
| --------- | ------- |
| fieldMapping   | **object**  |
