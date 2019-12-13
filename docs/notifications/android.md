# Android Installation

First ensure you have followed the [initial setup guide](version /installation/initial-setup) and the [messaging setup guide](version /messaging/android).

?> Before getting started with Android notifications it is highly recommended that you read through the official [Android Notifications Overview](https://developer.android.com/guide/topics/ui/notifiers/notifications) page and also use it as a reference during development; e.g. if your Heads-up notification is not showing then see the `Heads-up notification` section which explains the conditions and versions that will trigger a notification to display in Heads-up form.

## Install the RNFirebase Notifications package

**Note**: This is for react-native 0.60+ - for earlier versions of react-native please refer to the [previous version of this documentation](https://github.com/invertase/react-native-firebase-docs/blob/c73145088de14ede089fdd3bd3eaf156cc01203c/docs/notifications/android.md).

Add the `RNFirebaseNotificationsPackage` to your `android/app/src/main/java/com/[app name]/MainApplication.java`:

```java
// ...
import com.facebook.react.ReactApplication;
import io.invertase.firebase.notifications.RNFirebaseNotificationsPackage; // <-- Add this line

public class MainApplication extends Application implements ReactApplication {
    // ...

    @Override
    protected List<ReactPackage> getPackages() {
      @SuppressWarnings("UnnecessaryLocalVariable")
      List<ReactPackage> packages = new PackageList(this).getPackages();
      // Packages that cannot be autolinked yet can be added manually here, for example:
      // packages.add(new MyReactNativePackage());
      packages.add(new RNFirebaseNotificationsPackage()); // <-- Add this line
      return packages;
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

### Default icon and color (Optional) 

Within the application component, add metadata elements to set a default notification icon and color. Android uses these values whenever incoming messages do not explicitly set icon or color.

```xml
<application ...>
  <!-- Set custom default icon. This is used when no icon is set for incoming notification messages.
       See README(https://goo.gl/l4GJaQ) for more. -->
  <meta-data
    android:name="com.google.firebase.messaging.default_notification_icon"
    android:resource="@drawable/ic_stat_ic_notification" />
  <!-- Set color used with incoming notification messages. This is used when no color is set for the incoming
       notification message. See README(https://goo.gl/6BKBk7) for more. -->
  <meta-data
    android:name="com.google.firebase.messaging.default_notification_color"
    android:resource="@color/colorAccent" />
</application>
```

### Notification channels (Optional)

From Android 8.0 (API level 26) and higher, notification channels are supported and recommended. FCM provides a default notification channel with basic settings. If you prefer to create and use your own default channel, set default_notification_channel_id to the ID of your notification channel object as shown; FCM will use this value whenever incoming messages do not explicitly set a notification channel.

```xml
<application ...>
  <meta-data
    android:name="com.google.firebase.messaging.default_notification_channel_id"
    android:value="@string/default_notification_channel_id"/>
</application>
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
