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

**Note**: This is for react-native 0.60+ - for earlier versions of react-native please refer to the [previous version of this documentation](https://github.com/invertase/react-native-firebase-docs/blob/0a1f0abcf2fbf16524e61375aa16545a94132739/docs/perf-mon/android.md).

Add the `RNFirebasePerformancePackage` to your `android/app/src/main/java/com/[app name]/MainApplication.java`:

```java
// ...
import com.facebook.react.ReactApplication;
import io.invertase.firebase.perf.RNFirebasePerformancePackage; // <-- Add this line

public class MainApplication extends Application implements ReactApplication {
    // ...

    @Override
    protected List<ReactPackage> getPackages() {
      @SuppressWarnings("UnnecessaryLocalVariable")
      List<ReactPackage> packages = new PackageList(this).getPackages();
      // Packages that cannot be autolinked yet can be added manually here, for example:
      // packages.add(new MyReactNativePackage());
      packages.add(new RNFirebasePerformancePackage()); // <-- Add this line
      return packages;
    }
  };
  // ...
}
```
