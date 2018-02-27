# Android Installation

## Add the dependency

Add the Firebase Cloud Messaging dependancy to `android/app/build.gradle`:

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

Add permissions:
```xml
<manifest ...>
  <uses-permission android:name="android.permission.INTERNET" />
  <uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED"/>
  <uses-permission android:name="android.permission.VIBRATE" />
```

Set app [launch mode](https://inthecheesefactory.com/blog/understand-android-activity-launchmode/en) inside activity props:
```xml
<activity
  ...
  android:launchMode="singleTop"
>
```

Add messaging service:
```xml
<application ...>
  <service
    android:name="io.invertase.firebase.messaging.MessagingService"
    android:enabled="true"
    android:exported="true">
      <intent-filter>
        <action android:name="com.google.firebase.MESSAGING_EVENT" />
      </intent-filter>
  </service>
  <service android:name="io.invertase.firebase.messaging.InstanceIdService" android:exported="false">
    <intent-filter>
      <action android:name="com.google.firebase.INSTANCE_ID_EVENT"/>
    </intent-filter>
  </service>
```

If you would like to schedule local notifications then you also need to add the following:
```xml
  <receiver android:name="io.invertase.firebase.messaging.RNFirebaseLocalMessagingPublisher"/>
  <receiver android:enabled="true" android:exported="true" android:name="io.invertase.firebase.messaging.RNFirebaseSystemBootEventReceiver">
    <intent-filter>
      <action android:name="android.intent.action.BOOT_COMPLETED"/>
      <action android:name="android.intent.action.QUICKBOOT_POWERON"/>
      <action android:name="com.htc.intent.action.QUICKBOOT_POWERON"/>
      <category android:name="android.intent.category.DEFAULT" />
    </intent-filter>
  </receiver>
```
