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
      packages.add(new RNFirebaseAuthPackage()); <-- Add this line
      return packages;
    }
  };
  // ...
}
```
