# Android Installation

First ensure you have followed the [initial setup guide](version /installation/initial-setup).

## Install the RNFirebase Instance ID package

Add the `RNFirebaseInstanceIdPackage` to your `android/app/src/main/java/com/[app name]/MainApplication.java`:

```java
// ...
import io.invertase.firebase.RNFirebasePackage;
import io.invertase.firebase.analytics.RNFirebaseInstanceIdPackage; // <-- Add this line

public class MainApplication extends Application implements ReactApplication {
    // ...

    @Override
    protected List<ReactPackage> getPackages() {
      return Arrays.<ReactPackage>asList(
          new MainReactPackage(),
          new RNFirebasePackage(),
          new RNFirebaseInstanceIdPackage() // <-- Add this line
      );
    }
  };
  // ...
}
```
