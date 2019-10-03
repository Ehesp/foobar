# iOS Installation

First ensure you have followed the [initial setup guide](version /installation/initial-setup) and the [messaging setup guide](version /messaging/ios).

?> Remote notifications do not work on the iOS simulator, you must test them using a real device. This is a restriction enforced by Apple.

## Update `AppDelegate.m`

Add the following import to the top of your `ios/[App Name]/AppDelegate.m`:

```objectivec
#import "RNFirebaseNotifications.h"
```

Add the following to the `didFinishLaunchingWithOptions:(NSDictionary *)launchOptions` method, right after `[FIRApp Configure]`:

```objectivec
[FIRApp Configure] // after this line
[RNFirebaseNotifications configure];
```

?> It is recommended to add the line within the method **BETWEEN** the statement **[FIRApp Configure]** and the creation of **RCTRootView**. Otherwise the initialization can occur after already being required in your JavaScript code - leading to `app not initialised` exceptions.

Add the following method:

```objectivec
- (void)application:(UIApplication *)application didReceiveLocalNotification:(UILocalNotification *)notification {
  [[RNFirebaseNotifications instance] didReceiveLocalNotification:notification];
}
```

## Remote Notifications (Optional)

If you would like to support Remote Notifications via FCM, also add the following import to the top of your `ios/[App Name]/AppDelegate.m`:

```objectivec
#import "RNFirebaseMessaging.h"
```

Then add the following methods to your `ios/[App Name]/AppDelegate.m`:

```objectivec
- (void)application:(UIApplication *)application didReceiveRemoteNotification:(nonnull NSDictionary *)userInfo
                                                       fetchCompletionHandler:(nonnull void (^)(UIBackgroundFetchResult))completionHandler{
  [[RNFirebaseNotifications instance] didReceiveRemoteNotification:userInfo fetchCompletionHandler:completionHandler];
}

- (void)application:(UIApplication *)application didRegisterUserNotificationSettings:(UIUserNotificationSettings *)notificationSettings {
  [[RNFirebaseMessaging instance] didRegisterUserNotificationSettings:notificationSettings];
}
```

## Debugging

If you're having problems with messages not being received, check out the following blog post for help:

https://firebase.googleblog.com/2017/01/debugging-firebase-cloud-messaging-on.html
