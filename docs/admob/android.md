# Android Installation

First ensure you have followed the [initial setup guide](version /installation/initial-setup).

## Add the dependency

Add the Firebase Admob dependancy to `android/app/build.gradle`:

```groovy
dependencies {
  // ...
  implementation "com.google.firebase:firebase-ads:{{ android.firebase.ads }}"
}
```

## Install the RNFirebase Admob package

Add the `RNFirebaseAdMobPackage` to your `android/app/src/main/java/com/[app name]/MainApplication.java`:

```java
// ...
import io.invertase.firebase.RNFirebasePackage;
import io.invertase.firebase.admob.RNFirebaseAdMobPackage; // <-- Add this line

public class MainApplication extends Application implements ReactApplication {
    // ...

    @Override
    protected List<ReactPackage> getPackages() {
      return Arrays.<ReactPackage>asList(
          new MainReactPackage(),
          new RNFirebasePackage(),
          new RNFirebaseAdMobPackage() // <-- Add this line
      );
    }
  };
  // ...
}
```

## Update Android Manifest

You must add your AdMob App Id to your AndroidManfest

Android 9.0 removed by default all traces of the old Apache HTTP library. However, some libraries like Admob still need it until they are updated. 
You need to alter to your manifest inside the `<application>` element to enable legacy HTTP Library.

Add the following to `android/app/src/main/AndroidManifest.xml`:

Within the application component, add your AdMob ID (from the AdMob UI):
```xml
<application ...>
  
  <!-- Add this line as part of new AdMob library process. Sample AdMob App ID: ca-app-pub-3940256099942544~3347511713 -->
  <meta-data
    android:name="com.google.android.gms.ads.APPLICATION_ID"
    android:value="YOUR_ADMOB_APP_ID"/>
  
  <uses-library android:name="org.apache.http.legacy" android:required="false"/>  <!-- Add this line to avoid crashes on Android 9 until AdMob SDK update -->
  
</application>
```

> Important: This AdmOb ID is required as of Google Mobile Ads SDK version 17.0.0. Failure to add this `<meta-data>` tag results in a crash with the message: "The Google Mobile Ads SDK was initialized incorrectly."
