# Android Installation

First ensure you have followed the [initial setup guide](version /installation/initial-setup).

Analytics does not require any other dependencies to work.

## Install the RNFirebase Analytics package

**Note**: This is for react-native 0.60+ - for earlier versions of react-native please refer to the [previous version of this documentation](https://github.com/invertase/react-native-firebase-docs/blob/7996824f9613a500c3929d3aabd21321337db15c/docs/analytics/android.md).

Add the `RNFirebaseAnalyticsPackage` to your `android/app/src/main/java/com/[app name]/MainApplication.java`:

```java
// ...
import com.facebook.react.ReactApplication;
import io.invertase.firebase.analytics.RNFirebaseAnalyticsPackage; // <-- Add this line

public class MainApplication extends Application implements ReactApplication {
    // ...

    @Override
    protected List<ReactPackage> getPackages() {
      @SuppressWarnings("UnnecessaryLocalVariable")
      List<ReactPackage> packages = new PackageList(this).getPackages();
      // Packages that cannot be autolinked yet can be added manually here, for example:
      // packages.add(new MyReactNativePackage());
      packages.add(new RNFirebaseAnalyticsPackage()); // <-- Add this line
      return packages;
    }
  };
  // ...
}
```
