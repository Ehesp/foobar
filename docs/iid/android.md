# Android Installation

First ensure you have followed the [initial setup guide](version /installation/initial-setup).

## Install the RNFirebase Instance ID package

**Note**: This is for react-native 0.60+ - for earlier versions of react-native please refer to the [previous version of this documentation](https://github.com/invertase/react-native-firebase-docs/blob/b519ea6e892d7068836c40fbd5ddf8fe1dbd7893/docs/iid/android.md).

Add the `RNFirebaseInstanceIdPackage` to your `android/app/src/main/java/com/[app name]/MainApplication.java`:

```java
// ...
import com.facebook.react.ReactApplication;
import io.invertase.firebase.instanceid.RNFirebaseInstanceIdPackage; // <-- Add this line

public class MainApplication extends Application implements ReactApplication {
    // ...

    @Override
    protected List<ReactPackage> getPackages() {
      @SuppressWarnings("UnnecessaryLocalVariable")
      List<ReactPackage> packages = new PackageList(this).getPackages();
      // Packages that cannot be autolinked yet can be added manually here, for example:
      // packages.add(new MyReactNativePackage());
      packages.add(new RNFirebaseInstanceIdPackage()); // <-- Add this line
      return packages;
    }
  };
  // ...
}
```
