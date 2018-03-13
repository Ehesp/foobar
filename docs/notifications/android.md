# Android Installation

First ensure you have followed the [initial setup guide](version /installation/initial-setup) and the [messaging setup guide](version /messaging/android).

## Install the RNFirebase Notifications package

Add the `RNFirebaseNotificationsPackage` to your `android/app/src/main/java/com/[app name]/MainApplication.java`:

```java
// ...
import io.invertase.firebase.RNFirebasePackage;
import io.invertase.firebase.messaging.RNFirebaseNotificationsPackage; // <-- Add this line

public class MainApplication extends Application implements ReactApplication {
    // ...

    @Override
    protected List<ReactPackage> getPackages() {
      return Arrays.<ReactPackage>asList(
          new MainReactPackage(),
          new RNFirebasePackage(),
          new RNFirebaseNotificationsPackage() // <-- Add this line
      );
    }
  };
  // ...
}
```

## Update Android Manifest

Add the following to `android/app/src/main/AndroidManifest.xml`:

Add permissions:
```xml
<manifest ...>
  <uses-permission android:name="android.permission.INTERNET" />
  <uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />
  <uses-permission android:name="android.permission.VIBRATE" />
```

Set app [launch mode](https://inthecheesefactory.com/blog/understand-android-activity-launchmode/en) inside activity props:
```xml
<activity
  ...
  android:launchMode="singleTop"
>
```

## Scheduled Notifications (Optional)

If you would like to schedule local notifications then you also need to add the following to the application component of `android/app/src/main/AndroidManifest.xml`:

```xml
<application ...>
  <receiver android:name="io.invertase.firebase.notifications.RNFirebaseNotificationReceiver"/>
  <receiver android:enabled="true" android:exported="true"  android:name="io.invertase.firebase.notifications.RNFirebaseNotificationsRebootReceiver">
    <intent-filter>
      <action android:name="android.intent.action.BOOT_COMPLETED"/>
      <action android:name="android.intent.action.QUICKBOOT_POWERON"/>
      <action android:name="com.htc.intent.action.QUICKBOOT_POWERON"/>
      <category android:name="android.intent.category.DEFAULT" />
    </intent-filter>
  </receiver>
</application>
```
