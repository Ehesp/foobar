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

## Enable Legacy HTTP Library in AndroidManifest

Android 9.0 removed by default all traces of the old Apache HTTP library. However, it seems that some libraries need it. You need to add this to your manifest inside the <application> element to enable legacy HTTP Library.
  
`<uses-library
    android:name="org.apache.http.legacy"
    android:required="false"/>`
    
```

<application
      <uses-library android:name="org.apache.http.legacy" android:required="false"/>  // <-- Add this line 
</application>

```

