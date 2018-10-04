# iOS Installation

First ensure you have followed the [initial setup guide](version /installation/initial-setup).

## Add the pod

Add the following to your `Podfile`:

```ruby
pod 'Firebase/Auth', '~> {{ ios.firebase.auth }}'
```

Run `pod update`.

?> If you plan to make use of email sign-in links then you'll also need to follow the [Dynamic Links for iOS installation guide](version /links/ios).