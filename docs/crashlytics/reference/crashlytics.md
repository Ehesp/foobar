# Crashlytics

```js
firebase.crashlytics
```

?> **Upcoming Change:** Note that this API is likely to change in v5.1.0 to simplify setting values/multiple values as well as better JS Error reporting. The API implemented currently is an initial draft to allow early access.

## Methods

The following methods are accessed via the Crashlytics instance `firebase.crashlytics()`.

### crash

[method]crash() returns void;[/method]

Forces a native crash. Useful for testing your application is set up correctly.

### log

[method]log(message) returns void;[/method]

Logs a message that will be sent with any subsequent crash reports.

`recordError` or `recordCustomError` must be called after `log`.

| Parameter |         |
| --------- | ------- |
| message   | **string** |

***Example***

```js
firebase.crashlytics().log('Test Message!');
firebase.crashlytics().recordError(37,"Test Error");
```

### recordError

[method]recordError(code, message) returns void;[/method]

Logs a non fatal exception to Crashlytics.

> Reports are not realtime. They can take a number of hours to appear in the Firebase console.

| Parameter |     |
| --------- | --- |
| code      | **number** <br /> The error code. |
| message   | **string** <br /> The error message. |

### recordCustomError

[method]recordCustomError(name, message, stack) returns void;[/method]

Logs a custom non fatal exception to Crashlytics.

> Reports are not realtime. They can take a number of hours to appear in the Firebase console.

| Parameter |     |
| --------- | --- |
| name      | **string** <br /> The error title. |
| message   | **string** <br /> The error message. |
| stack   | **customError[]** *Optional* <br /> Array of the custom stack traces for the error. <br /> See [Custom Error Type](#custom-error-type).  |

***Example***

```js
firebase.crashlytics().recordCustomError(
            'Custom Error',
            'Oh No!',
            [
                {
                    className: 'AwesomeClass',
                    fileName: 'MyFile.tsx',
                    functionName: 'render',
                    lineNumber: 81,
                    additional: { Dog: 'Food', Laugh: 'No' }
                }
            ]
        );
```

#### Custom Error Type

[type]customError[/type]

The type for the custom stack trace.

| Parameter |     |
| --------- | --- |
| fileName      | **string** *Required*<br /> The name of the file. |
| className   | **string** *Optional*<br /> The name of the class. If `undefined` will be "Unknown Class" |
| functionName   | **string** *Optional*<br /> The name of the function. If `undefined` will be "Unknown Function"|
| lineNumber   | **number** *Optional*<br /> The line number of the error. If `undefined` will be -1|
| additional   | **Object** *Optional*<br /> Additional data you would like to include in the stack trace.<br/>See [recordCustomError](#recordCustomError) for an example.|

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

### setUserName

[method]setUserName(userName) returns void;[/method]

Set the user ID to show alongside any subsequent crash reports.

| Parameter |     |
| --------- | --- |
| userName    | **string** <br /> The user's name. |

### setUserEmail

[method]setUserEmail(userEmail) returns void;[/method]

Set the user ID to show alongside any subsequent crash reports.

| Parameter |     |
| --------- | --- |
| userEmail    | **string** <br /> The user's email address. |

### enableCrashlyticsCollection

[method]enableCrashlyticsCollection() returns void;[/method]

Enable Crashlytics reporting. Only avaliable when [disabled automatic initialization](../manual-initialization).