# Android Installation

First ensure you have followed the [initial setup guide](version /installation/initial-setup).

## Add the dependency

Add the Firebase Firestore dependency to `android/app/build.gradle`:

```groovy
dependencies {
  // ...
  compile "com.google.firebase:firebase-firestore:{{ android.firebase.version }}"
}
```

## Enable multi DEX
Make sure you have `multiDexEnabled true` in `android/app/build.gradle`:
```groovy
android {
    // ...
    defaultConfig {
        // ...
        multiDexEnabled true
    }
}
```

## Install the RNFirebase Firestore package

Add the `RNFirebaseFirestorePackage` to your `android/app/src/main/java/com/[app name]/MainApplication.java`:

```java
// ...
import io.invertase.firebase.RNFirebasePackage;
import io.invertase.firebase.firestore.RNFirebaseFirestorePackage; // <-- Add this line

public class MainApplication extends Application implements ReactApplication {
    // ...

    @Override
    protected List<ReactPackage> getPackages() {
      return Arrays.<ReactPackage>asList(
          new MainReactPackage(),
          new RNFirebasePackage(),
          new RNFirebaseFirestorePackage() // <-- Add this line
      );
    }
  };
  // ...
}
```
