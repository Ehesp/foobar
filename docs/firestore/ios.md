# iOS Installation

First ensure you have followed the [initial setup guide](version /installation/initial-setup).

## Add the pod

Add the following to your `Podfile`:

```ruby
pod 'Firebase/Firestore', '~> {{ ios.firebase.firestore }}'
```

Run `pod update`.

## Troubleshooting

Your Xcode project may fail to build if you are including the Google Signin pod (`pod 'GoogleSignIn'`) in your project, this appears to be due to some extra search paths that need to be removed.

Invertase has a fork of the project at https://github.com/invertase/react-native-google-signin, which you can add to your project using:

```
npm install --save https://github.com/invertase/react-native-google-signin.git#v0.12.1
```

You can see the relevant discussion on github issues [here](https://github.com/invertase/react-native-firebase/issues/758#issuecomment-358575691).
