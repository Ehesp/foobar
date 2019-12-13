# iOS Installation

First ensure you have followed the [initial setup guide](version /installation/initial-setup).

## Add the pod

Add the following to your `Podfile`:

```ruby
pod 'Firebase/Auth', '~> {{ ios.firebase.auth }}'
```

Run `pod update`.

## Optional: authenticate with phone number

### Enable Phone Number sign-in for your Firebase project

To sign in users by SMS, you must first enable the Phone Number sign-in method for your Firebase project:

- In the Firebase console, open the `Authentication` section.
- On the `Sign-in` Method page, enable the `Phone Number` sign-in method.

More details: [Firebase-phone-auth](https://firebase.google.com/docs/auth/ios/phone-auth)

### Enable app verification

Phone authentication leaves you 2 choices:
- Silent APNs notifications
- reCAPTCHA verification

Please read carefully and follow Firebase related documentation to complete this step [Firebase-phone-auth](https://firebase.google.com/docs/auth/ios/phone-auth) otherwise app verification will throw an error.

?> If you plan to make use of email sign-in links then you'll also need to follow the [Dynamic Links for iOS installation guide](version /links/ios).
