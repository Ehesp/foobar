# Android Installation

First ensure you have followed the [initial setup guide](version /installation/initial-setup).

## Add the dependency

Add the Firebase Cloud Messaging dependency to `android/app/build.gradle`:

```groovy
dependencies {
  // ...
  compile "com.google.firebase:firebase-messaging:{{ android.firebase.version }}"
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

(Optional) Within the application component, add metadata elements to set a default notification icon and color. Android uses these values whenever incoming messages do not explicitly set icon or color.

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

(Optional) From Android 8.0 (API level 26) and higher, notification channels are supported and recommended. FCM provides a default notification channel with basic settings. If you prefer to create and use your own default channel, set default_notification_channel_id to the ID of your notification channel object as shown; FCM will use this value whenever incoming messages do not explicitly set a notification channel.

```xml
<application ...>
  <meta-data
    android:name="com.google.firebase.messaging.default_notification_channel_id"
    android:value="@string/default_notification_channel_id"/>
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
