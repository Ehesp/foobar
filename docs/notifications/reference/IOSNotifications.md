# IOSNotifications

This deals with iOS-specific Notification functionality.


## Properties

### shouldAutoComplete
[method]shouldAutoComplete returns boolean;[/method]

Controls whether notifications are automatically completed. 

If `true` then the notification is immediately completed with the assumed value of `backgroundFetchResult.noData` and [ref notifications.IOSNofication]'s `complete` function is `undefined`. 

If `false` then you must handle notification completion manually via [ref notifications.IOSNotification]'s `complete` function.

> See the native [application:didReceiveRemoteNotification:fetchCompletionHandler:](https://developer.apple.com/documentation/uikit/uiapplicationdelegate/1623013-application?language=objc) method for more details on iOS notification completion.

### backgroundFetchResult
[method]backgroundFetchResult returns Object;[/method]

Returns an object with keys `noData`, `newData` and `failure`. The value for one of these keys should be used when calling [ref notifications.IOSNotification#complete].

[example Example]
```javascript
const newDataResult = firebase.notifications().ios.backgroundFetchResult.newData;
notification.ios.complete(newDataResult);
```
[/example]

> See the native [application:didReceiveRemoteNotification:fetchCompletionHandler:](https://developer.apple.com/documentation/uikit/uiapplicationdelegate/1623013-application?language=objc) method for more details on iOS notification completion.