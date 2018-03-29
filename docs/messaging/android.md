# Android Installation

First ensure you have followed the [initial setup guide](version /installation/initial-setup).

## Add the dependency

Add the Firebase Cloud Messaging dependency to `android/app/build.gradle`:

```groovy
dependencies {
  // ...
  compile "com.google.firebase:firebase-messaging:{{ android.firebase.version }}"
  compile 'me.leolin:ShortcutBadger:1.1.18@aar' // optional for setBadgeNumber
}
```

## Install the RNFirebase Messaging package

Add the `RNFirebaseMessagingPackage` to your `android/app/src/main/java/com/[app name]/MainApplication.java`:

```java
// ...
import io.invertase.firebase.RNFirebasePackage;
import io.invertase.firebase.messaging.RNFirebaseMessagingPackage; // <-- Add this line

public class MainApplication extends Application implements ReactApplication {
    // ...

    @Override
    protected List<ReactPackage> getPackages() {
      return Arrays.<ReactPackage>asList(
          new MainReactPackage(),
          new RNFirebasePackage(),
          new RNFirebaseMessagingPackage() // <-- Add this line
      );
    }
  };
  // ...
}
```

## Update Android Manifest

Add the following to `android/app/src/main/AndroidManifest.xml`:

Within the application component, add the messaging service and instance ID service:
```xml
<application ...>
  <service android:name="io.invertase.firebase.messaging.RNFirebaseMessagingService">
    <intent-filter>
      <action android:name="com.google.firebase.MESSAGING_EVENT" />
    </intent-filter>
  </service>
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
