# Android Installation

First ensure you have followed the [initial setup guide](version /installation/initial-setup).

## Add the dependency

Then Just Add the Firebase InAppMessaging dependancy to `android/app/build.gradle`:

```groovy
dependencies {
  // ...
  implementation 'com.google.firebase:firebase-inappmessaging-display:{{ android.firebase.in-app-messaging }}'
}
```

