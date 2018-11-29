# Crashlytics

```
firebase.crashlytics
```

?> **Upcoming Change:** Note that this API is likely to change in v5.1.0 to simplify setting values/multiple values as well as better JS Error reporting. The API implemented currently is an initial draft to allow early access.

## Methods 

The following methods are accessed via the Crashlytics instance `firebase.crashlytics()`.

### crash
[method]crash() returns void;[/method]

Forces a crash. Useful for testing your application is set up correctly.

### log
[method]log(message) returns void;[/method]

Logs a message that will be sent with any subsequent crash reports.

| Parameter |         |
| --------- | ------- |
| message   | **string** |

### recordError
[method]recordError(code, message) returns void;[/method]

Logs a non fatal exception to Crashlytics.

> Reports are not realtime. They can take a number of hours to appear in the Firebase console.

| Parameter |     |
| --------- | --- |
| code      | **number** <br /> The error code. |
| message   | **string** <br /> The error message. |

### setBoolValue
[method]setBoolValue(key, value) returns void;[/method]

Set a boolean value to show alongside any subsequent crash reports.

| Parameter |     |
| --------- | --- |
| key       | **string** <br /> The name of the key. |
| value     | **boolean** <br /> The value of the key. |

### setFloatValue
[method]setFloatValue(key, value) returns void;[/method]

Set a float value to show alongside any subsequent crash reports.

| Parameter |     |
| --------- | --- |
| key       | **string** <br /> The name of the key. |
| value     | **number** <br /> The value of the key. |

### setIntValue
[method]setIntValue(key, value) returns void;[/method]

Set an integer value to show alongside any subsequent crash reports.

| Parameter |     |
| --------- | --- |
| key       | **string** <br /> The name of the key. |
| value     | **number** <br /> The value of the key. |

### setStringValue
[method]setStringValue(key, value) returns void;[/method]

Set a string value to show alongside any subsequent crash reports.

| Parameter |     |
| --------- | --- |
| key       | **string** <br /> The name of the key. |
| value     | **number** <br /> The value of the key. |

### setUserIdentifier
[method]setUserIdentifier(userId) returns void;[/method]

Set the user ID to show alongside any subsequent crash reports.

| Parameter |     |
| --------- | --- |
| userId    | **string** <br /> The user's ID. |

### enableCrashlyticsCollection
[method]enableCrashlyticsCollection() returns void;[/method]

Enable Crashlytics reporting. Only avaliable when [disabled automatic initialization](../manual-initialization).