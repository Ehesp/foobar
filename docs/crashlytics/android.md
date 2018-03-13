# Android Installation

First ensure you have followed the [initial setup guide](version /installation/initial-setup).

## Add the dependency

Add the Firebase Crashlytics dependency to `android/app/build.gradle`:

```groovy
dependencies {
  // ...
  compile('com.crashlytics.sdk.android:crashlytics:{{ android.fabric.version }}@aar') {
    transitive = true
  }
}
```

Crashlytics also requires the Fabric Gradle dependency. In your projects `android/build.gradle` file, add the plugin to your dependencies and also check that you have version {{ android.google.services }} of the google-services plugin:

```groovy
dependencies {
  // ...
  classpath 'com.google.gms:google-services:{{ android.google.services }}'
  classpath 'io.fabric.tools:gradle:{{ android.fabric.tools }}'
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

Add the `RNFirebaseCrashlyticsPackage` to your `android/app/src/main/java/com/[app name]/MainApplication.java`:

```java
// ...
import io.invertase.firebase.RNFirebasePackage;
import io.invertase.firebase.fabric.crashlytics.RNFirebaseCrashlyticsPackage; // <-- Add this line

public class MainApplication extends Application implements ReactApplication {
    // ...

    @Override
    protected List<ReactPackage> getPackages() {
      return Arrays.<ReactPackage>asList(
          new MainReactPackage(),
          new RNFirebasePackage(),
          new RNFirebaseCrashlyticsPackage() // <-- Add this line
      );
    }
  };
  // ...
}
```
