# Android Installation

!> Invites has been removed from the Firebase SDKs, and removed here as of v5.5.0. This documentation is only here for users of older versions of the library. Use Dynamic Links instead.

First ensure you have followed the [initial setup guide](version /installation/initial-setup) and the [dynamic links setup guide](version /links/android).

### Find your SHA fingerprint
Ensure you have SHA fingerprint added in your Firebase console, under the `General settings` tab otherwise you will a receive a `Message failed to send` error.

E.g. for debug: run keytool command in your terminal

```bash
$ keytool -exportcert -list -v -alias androiddebugkey -keystore ~/.android/debug.keystore
```

## Install the RNFirebase Invites package

**Note**: This is for react-native 0.60+ - for earlier versions of react-native please refer to the [previous version of this documentation](https://github.com/invertase/react-native-firebase-docs/blob/a02587befebb0513da8d662cc7ea5f435947e2e8/docs/invites/android.md).

Add the `RNFirebaseInvitesPackage` to your `android/app/src/main/java/com/[app name]/MainApplication.java`:

```java
// ...
import com.facebook.react.ReactApplication;
import io.invertase.firebase.invites.RNFirebaseInvitesPackage; // <-- Add this line

public class MainApplication extends Application implements ReactApplication {
    // ...

    @Override
    protected List<ReactPackage> getPackages() {
      @SuppressWarnings("UnnecessaryLocalVariable")
      List<ReactPackage> packages = new PackageList(this).getPackages();
      // Packages that cannot be autolinked yet can be added manually here, for example:
      // packages.add(new MyReactNativePackage());
      packages.add(new RNFirebaseInvitesPackage()); // <-- Add this line
      return packages;
    }
  };
  // ...
}
```
