# Android Installation

## Add the dependency

Add the Firebase Realtime Database dependency to `android/app/build.gradle`:

```groovy
dependencies {
  // ...
  implementation "com.google.firebase:firebase-database:{{ android.firebase.database }}"
}
```

## Install the RNFirebase Database package

**Note**: This is for react-native 0.60+ - for earlier versions of react-native please refer to the [previous version of this documentation](https://github.com/invertase/react-native-firebase-docs/blob/cfe8802662b0de36f5f0ad083a0c7472319629ba/docs/database/android.md).

Add the `RNFirebaseDatabasePackage` to your `android/app/src/main/java/com/[app name]/MainApplication.java`:

```java
// ...
import com.facebook.react.ReactApplication;
import io.invertase.firebase.database.RNFirebaseDatabasePackage; // <-- Add this line

public class MainApplication extends Application implements ReactApplication {
    // ...

    @Override
    protected List<ReactPackage> getPackages() {
      @SuppressWarnings("UnnecessaryLocalVariable")
      List<ReactPackage> packages = new PackageList(this).getPackages();
      // Packages that cannot be autolinked yet can be added manually here, for example:
      // packages.add(new MyReactNativePackage());
      packages.add(new RNFirebaseDatabasePackage()); // <-- Add this line
      return packages;
    }
  };
  // ...
}
```
