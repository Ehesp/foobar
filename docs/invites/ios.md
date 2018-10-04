# iOS Installation

First ensure you have followed the [initial setup guide](version /installation/initial-setup) and the [dynamic links setup guide](version /links/ios).

> On iOS, users must be signed in with their Google Accounts before they can send invitations.

## Add the pod

Add the following to your `Podfile`:

```ruby
pod 'Firebase/Invites', '~> {{ ios.firebase.invites }}'
```

Run `pod update`.

## Update `AppDelegate.m`

Replace the `RNFirebaseLinks` import with `RNFirebaseInvites` at the top of your `ios/[App Name]/AppDelegate.m`:

```objectivec
#import "RNFirebaseInvites.h"
```

Replace the `RNFirebaseLinks` methods with `RNFirebaseInvites` as follows:

```objectivec
- (BOOL)application:(UIApplication *)application
            openURL:(NSURL *)url
            options:(NSDictionary<NSString *, id> *)options {
    return [[RNFirebaseInvites instance] application:application openURL:url options:options];
}

- (BOOL)application:(UIApplication *)application
continueUserActivity:(NSUserActivity *)userActivity
 restorationHandler:(void (^)(NSArray *))restorationHandler {
    return [[RNFirebaseInvites instance] application:application continueUserActivity:userActivity restorationHandler:restorationHandler];
}
```

## Setup Google Sign-In

> Take a look at our [social auth guide](version /auth/social-auth) for how to use Google Sign In with `react-native-firebase`.

To add custom URL schemes to your Xcode project see [this quick tutorial](https://codorial.com/g/invertase/tutorials/ios-xcode-custom-url-scheme/) - the `URL Schemes` is usually your reversed client ID. To find this value, open your `GoogleService-Info.plist` configuration file, and look for the `REVERSED_CLIENT_ID` key. Copy the value of that key, and paste it into the URL Schemes box on the configuration page.
