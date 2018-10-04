# Android Installation

First ensure you have followed the [initial setup guide](version /installation/initial-setup).

Analytics does not require any other dependencies to work.

## Install the RNFirebase Analytics package

Add the `RNFirebaseAnalyticsPackage` to your `android/app/src/main/java/com/[app name]/MainApplication.java`:

```java
// ...
import io.invertase.firebase.RNFirebasePackage;
import io.invertase.firebase.analytics.RNFirebaseAnalyticsPackage; // <-- Add this line

public class MainApplication extends Application implements ReactApplication {
    // ...

    @Override
    protected List<ReactPackage> getPackages() {
      return Arrays.<ReactPackage>asList(
          new MainReactPackage(),
          new RNFirebasePackage(),
          new RNFirebaseAnalyticsPackage() // <-- Add this line
      );
    }
  };
  // ...
}
```
