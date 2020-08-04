# Android Installation

First ensure you have followed the [initial setup guide](version /installation/initial-setup).

?> If you're migrating from Fabric ensure you **remove the `fabric.properties` file** from your android project - if you do not do this you will not receive crash reports on the Firebase console.

## Add the dependency

Add the Firebase Crashlytics dependency to `android/app/build.gradle`:

```groovy
dependencies {
  // ...
  implementation('com.crashlytics.sdk.android:crashlytics:{{ android.firebase.crashlytics }}@aar') {
    transitive = true
  }
}
```

Crashlytics also requires the Fabric Gradle dependency. In your projects `android/build.gradle` file, add the plugin to your dependencies and also check that you have version {{ android.gms.google-services }} of the google-services plugin:

```groovy
buildscript {
  // ...
  dependencies {
    // ...
    classpath 'com.google.gms:google-services:{{ android.gms.google-services }}'
    classpath 'io.fabric.tools:gradle:{{ android.fabric.tools }}'
  }
}
```

You need to add `maven { url 'https://maven.fabric.io/public' }` to your `android/build.gradle` as follows:

```groovy
buildscript {
    repositories {
        jcenter()
        maven {
            url 'https://maven.fabric.io/public'
        }
    }
    // ...
}
```

At the top of your `android/app/build.gradle` file, below other plugins, apply the `io.fabric` plugin:

```groovy
apply plugin: "com.android.application"
apply plugin: "io.fabric"
```

## Install the RNFirebase Crashlytics package

**Note**: This is for react-native 0.60+ - for earlier versions of react-native please refer to the [previous version of this documentation](https://github.com/invertase/react-native-firebase-docs/blob/bbb35f90a7b6280591caf7ffb072a2619724d829/docs/crashlytics/android.md).

Add the `RNFirebaseCrashlyticsPackage` to your `android/app/src/main/java/com/[app name]/MainApplication.java`:

```java
// ...
import com.facebook.react.ReactApplication;
import io.invertase.firebase.fabric.crashlytics.RNFirebaseCrashlyticsPackage; // <-- Add this line

public class MainApplication extends Application implements ReactApplication {
    // ...

    @Override
    protected List<ReactPackage> getPackages() {
      @SuppressWarnings("UnnecessaryLocalVariable")
      List<ReactPackage> packages = new PackageList(this).getPackages();
      // Packages that cannot be autolinked yet can be added manually here, for example:
      // packages.add(new MyReactNativePackage());
      packages.add(new RNFirebaseCrashlyticsPackage()); // <-- Add this line
      return packages;
    }
  };
  // ...
}
```

?> If you're migrating from Fabric ensure you **remove the `fabric.properties` file** from your android project - if you do not do this you will not receive crash reports on the Firebase console.

## Report Crash Events

Crashylitcs has two types of events. **Crash** and **Non-fatal**. In order to report Crash events it is necessary to reopen the application so that Firebase can send the report. But on Android the app doesn't report Crash type events with debug APK (this APK that is used by react-native run-android command, even if you're not in React Native debug mode), so on Android you need generate a release APK to see Crash report on Firebase Console. 
  1. Open the app. 
  2. Force a crash. 
  3. Reopen the app without crash.
  4. Wait about 5 minutes for the crash report to appear on the Firebase console.
