# Android Installation

## Add the dependency

Add the Firebase Storage dependency to `android/app/build.gradle`:

```groovy
dependencies {
  // ...
  implementation "com.google.firebase:firebase-storage:{{ android.firebase.storage }}"
}
```

## Install the RNFirebase Storage package

**Note**: This is for react-native 0.60+ - for earlier versions of react-native please refer to the [previous version of this documentation](https://github.com/invertase/react-native-firebase-docs/blob/c974d5253f85cec0a82081a086c5d9dff50c55ad/docs/storage/android.md).

Add the `RNFirebaseStoragePackage` to your `android/app/src/main/java/com/[app name]/MainApplication.java`:

```java
// ...
import com.facebook.react.ReactApplication;
import io.invertase.firebase.storage.RNFirebaseStoragePackage; // <-- Add this line

public class MainApplication extends Application implements ReactApplication {
    // ...

    @Override
    protected List<ReactPackage> getPackages() {
      @SuppressWarnings("UnnecessaryLocalVariable")
      List<ReactPackage> packages = new PackageList(this).getPackages();
      // Packages that cannot be autolinked yet can be added manually here, for example:
      // packages.add(new MyReactNativePackage());
      packages.add(new RNFirebaseStoragePackage()); // <-- Add this line
      return packages;
    }
  };
  // ...
}
```
