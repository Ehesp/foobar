# iOS Installation

First ensure you have followed the [initial setup guide](version /installation/initial-setup).

## Add the pod

Add the following to your `Podfile`:

```ruby
pod 'Firebase/AdMob', '~> {{ ios.firebase.ads }}'
```

Run `pod update`.

## Update your plist file

In your app's `Info.plist` file, add a GADApplicationIdentifier key with a string value of your AdMob app ID. You can find your App ID in the AdMob UI.

It should look like this, but with your ID, not the sample ID used below:

```xml
  <key>GADApplicationIdentifier</key>
  <string>ca-app-pub-3940256099942544~1458002511</string>
```
