# Android Installation

## Add the dependency

Add the Firebase Authentication dependency to `android/app/build.gradle`:

```groovy
dependencies {
  // ...
  implementation "com.google.firebase:firebase-auth:{{ android.firebase.auth }}"
}
```

?> If you plan to make use of Email sign-in links then you'll also need to follow the [Dynamic Links for Android installation guide](version /links/android).

## Install the RNFirebase Authentication package

**Note**: This is for react-native 0.60+ - for earlier versions of react-native please refer to the [previous version of this documentation](https://github.com/invertase/react-native-firebase-docs/blob/8c36d9df1a35e993f5d4126c33448256b9c5b682/docs/auth/android.md).

Add the `RNFirebaseAuthPackage` to your `android/app/src/main/java/com/[app name]/MainApplication.java`:

```java
// ...
import com.facebook.react.ReactApplication;
import io.invertase.firebase.auth.RNFirebaseAuthPackage; // <-- Add this line

public class MainApplication extends Application implements ReactApplication {
    // ...

    @Override
    protected List<ReactPackage> getPackages() {
      @SuppressWarnings("UnnecessaryLocalVariable")
      List<ReactPackage> packages = new PackageList(this).getPackages();
      // Packages that cannot be autolinked yet can be added manually here, for example:
      // packages.add(new MyReactNativePackage());
      packages.add(new RNFirebaseAuthPackage()); // <-- Add this line
      return packages;
    }
  };
  // ...
}
```
