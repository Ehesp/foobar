# Android Installation

First ensure you have followed the [initial setup guide](version /installation/initial-setup).

## Add the dependency

Add the Firebase Cloud Messaging dependency and optional ShortcutBadger dependency to `android/app/build.gradle`:

```groovy
dependencies {
  // ...
  implementation "com.google.firebase:firebase-messaging:{{ android.firebase.messaging }}"
  implementation 'me.leolin:ShortcutBadger:1.1.21@aar' // <-- Add this line if you wish to use badge on Android
}
```

## Install the RNFirebase Messaging package

**Note**: This is for react-native 0.60+ - for earlier versions of react-native please refer to the [previous version of this documentation](https://github.com/invertase/react-native-firebase-docs/blob/2d4382ed1d2aaa939f01851fd909e88f8dc0a632/docs/messaging/android.md).

Add the `RNFirebaseMessagingPackage` to your `android/app/src/main/java/com/[app name]/MainApplication.java`:

```java
// ...
import com.facebook.react.ReactApplication;
import io.invertase.firebase.messaging.RNFirebaseMessagingPackage; // <-- Add this line

public class MainApplication extends Application implements ReactApplication {
    // ...

    @Override
    protected List<ReactPackage> getPackages() {
      @SuppressWarnings("UnnecessaryLocalVariable")
      List<ReactPackage> packages = new PackageList(this).getPackages();
      // Packages that cannot be autolinked yet can be added manually here, for example:
      // packages.add(new MyReactNativePackage());
      packages.add(new RNFirebaseMessagingPackage()); // <-- Add this line
      return packages;
    }
  };
  // ...
}
```

## Update Android Manifest

Add the following to `android/app/src/main/AndroidManifest.xml`:

Within the application component, add the messaging service:
```xml
<application ...>

  <service android:name="io.invertase.firebase.messaging.RNFirebaseMessagingService">
    <intent-filter>
      <action android:name="com.google.firebase.MESSAGING_EVENT" />
    </intent-filter>
  </service>

</application>
```

**For RNFB versions less than 5.2.0 only**; add the instance ID service:
```xml
<application ...>

  <service android:name="io.invertase.firebase.messaging.RNFirebaseInstanceIdService">
    <intent-filter>
      <action android:name="com.google.firebase.INSTANCE_ID_EVENT"/>
    </intent-filter>
  </service>

</application>
```

## (Optional) Background Messages

If you want to be able to react to data-only messages when your app is in the background, e.g. to display a heads up notification, then you need to add the following to `android/app/src/main/AndroidManifest.xml`:

```xml
<application ...>
  <service android:name="io.invertase.firebase.messaging.RNFirebaseBackgroundMessagingService" />
</application>
``` 

You'll also need to check out the optional steps as part of our [Receiving Messages guide](version /messaging/receiving-messages).
