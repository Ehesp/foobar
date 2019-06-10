# Android Installation

First ensure you have followed the [initial setup guide](version /installation/initial-setup).

## Add the dependency

Add the Firebase Performance Monitoring dependency to `android/app/build.gradle`:

```groovy
dependencies {
  // ...
  implementation "com.google.firebase:firebase-perf:{{ android.firebase.perf }}"
}
```

Performance Monitoring also requires the Firebase Perf Plugins dependency. In your projects `android/build.gradle` file, add the plugin to your dependencies:

```groovy
dependencies {
  // ...
  classpath 'com.google.firebase:perf-plugin:{{ android.firebase.plugins }}'
}
```

!> Warning: the plugin dependency changed to `perf-plugin` from `firebase-plugins` with the move to version 1.2. You must update your `android/build.gradle` to use it.

At the top of your `android/app/build.gradle` file, below other plugins, apply the `firebase-perf` plugin:

```groovy
apply plugin: "com.android.application"
apply plugin: "com.google.firebase.firebase-perf"
```

## Install the RNFirebase Performance package

Add the `RNFirebasePerformancePackage` to your `android/app/src/main/java/com/[app name]/MainApplication.java`:

```java
// ...
import io.invertase.firebase.RNFirebasePackage;
import io.invertase.firebase.perf.RNFirebasePerformancePackage; // <-- Add this line

public class MainApplication extends Application implements ReactApplication {
    // ...

    @Override
    protected List<ReactPackage> getPackages() {
      return Arrays.<ReactPackage>asList(
          new MainReactPackage(),
          new RNFirebasePackage(),
          new RNFirebasePerformancePackage() // <-- Add this line
      );
    }
  };
  // ...
}
```
