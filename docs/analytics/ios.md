# iOS Installation

Ensure you have followed the [initial setup guide](version /installation/initial-setup).

## Device Identification

If you would like to enable Firebase Analytics to generate automatic audience metrics for iOS (as it does by default in Android), you must link additional iOS libraries, [as documented by the Google Firebase team](https://support.google.com/firebase/answer/6318039). Specifically you need libAdIdAccess.a and AdSupport.framework

The way to do this using Cocoapods is to add this to your Podfile (though please use [the most current Pod version](https://cocoapods.org/pods/GoogleIDFASupport) supported by react-native-firebase):
```ruby
  pod 'GoogleIDFASupport', '~> 3.14.0'
```
