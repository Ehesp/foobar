# Android Installation

First ensure you have followed the [initial setup guide](version /installation/initial-setup) and the [dynamic links setup guide](version /links/android).

### Find your SHA fingerprint
Ensure you have SHA fingerprint added in your Firebase console, under the `General settings` tab otherwise you will a receive a `Message failed to send` error.

E.g. for debug: run keytool command in your terminal

```bash
$ keytool -exportcert -list -v -alias androiddebugkey -keystore ~/.android/debug.keystore
```

## Install the RNFirebase Invites package

Add the `RNFirebaseInvitesPackage` to your `android/app/src/main/java/com/[app name]/MainApplication.java`:

```java
// ...
import io.invertase.firebase.RNFirebasePackage;
import io.invertase.firebase.invites.RNFirebaseInvitesPackage; // <-- Add this line

public class MainApplication extends Application implements ReactApplication {
    // ...

    @Override
    protected List<ReactPackage> getPackages() {
      return Arrays.<ReactPackage>asList(
          new MainReactPackage(),
          new RNFirebasePackage(),
          new RNFirebaseInvitesPackage() // <-- Add this line
      );
    }
  };
  // ...
}
```
