# Android Installation

## Add the dependency

Add the Firebase Dynamic Links / Invites dependency to your `android/app/build.gradle` file:

```groovy
dependencies {
  // ...
  implementation "com.google.firebase:firebase-invites:{{ android.firebase.invites }}"
}
```

## Install the RNFirebase Links package

Add the `RNFirebaseLinksPackage` to your `android/app/src/main/java/com/[app name]/MainApplication.java`:

```java
// ...
import io.invertase.firebase.RNFirebasePackage;
import io.invertase.firebase.links.RNFirebaseLinksPackage; // <-- Add this line

public class MainApplication extends Application implements ReactApplication {
    // ...

    @Override
    protected List<ReactPackage> getPackages() {
      return Arrays.<ReactPackage>asList(
          new MainReactPackage(),
          new RNFirebasePackage(),
          new RNFirebaseLinksPackage() // <-- Add this line
      );
    }
  };
  // ...
}
```


## Configure Android Project

1. In your [Firebase console](https://console.firebase.google.com/), open the Dynamic Links section.
    1. Accept the terms of service if you are prompted to do so.
    2. Take note of your project's Dynamic Links domain, which is displayed at the top of the Dynamic Links page. You need your project's Dynamic Links domain to programmatically create Dynamic Links. A Dynamic Links domain looks like app_code.app.goo.gl.

        ![console](https://firebase.google.com/docs/dynamic-links/images/dynamic-links-domain.png)

2. In your `android/app/src/main/AndroidManifest.xml` file, add a new intent filter to the activity that handles deep links for your app (for react-native this is usually the MainActivity), and specify the host and the scheme:

    ```xml
    <intent-filter>
        <action android:name="android.intent.action.VIEW"/>
        <category android:name="android.intent.category.DEFAULT"/>
        <category android:name="android.intent.category.BROWSABLE"/>
        <data android:host="example.page.link" android:scheme="http"/>
        <data android:host="example.page.link" android:scheme="https"/>
    </intent-filter>
    ```
    
3. If you wish to receive the intent in an existing instance of MainActivity, you may set the launchMode of MainActivity to singleTask in AndroidManifest.xml. See [<activity>](https://developer.android.com/guide/topics/manifest/activity-element.html) documentation for more information.

    ```xml
    <activity
      android:name=".MainActivity"
      android:launchMode="singleTask">
    ```

> For more information on Analytics for links or Handling Dynamic Links using App Links see the official [Firebase Android SDK docs](https://firebase.google.com/docs/dynamic-links/android/receive#record-analytics)
