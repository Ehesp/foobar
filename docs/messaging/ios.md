# iOS Installation

First ensure you have followed the [initial setup guide](version /installation/initial-setup).

?> FCM does not work on the iOS simulator, you must test them using a real device. This is a restriction enforced by Apple.

## Add the pod

Add the following to your `Podfile`:

```ruby
pod 'Firebase/Messaging', '~> {{ ios.firebase.messaging }}'
```

Run `pod update`.

## Setup Certificates

Please follow the instructions on the [Firebase docs](https://firebase.google.com/docs/cloud-messaging/ios/certs) on how to setup your APN certificates with FCM.

## Enable Capabilities

In Xcode, enable the following capabilities:

1) Push Notifications
2) Background modes > Remote notifications

## Debugging

If you're having problems with messages not being received, check out the following blog post for help:

https://firebase.googleblog.com/2017/01/debugging-firebase-cloud-messaging-on.html
