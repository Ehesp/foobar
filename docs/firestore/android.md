# Android Installation

First ensure you have followed the [initial setup guide](version /installation/initial-setup).

## Add the dependency

Add the Firebase Firestore dependency to `android/app/build.gradle`:

```groovy
dependencies {
  // ...
  implementation "com.google.firebase:firebase-firestore:{{ android.firebase.firestore }}"
}
```

## Install the RNFirebase Firestore package

**Note**: This is for react-native 0.60+ - for earlier versions of react-native please refer to the [previous version of this documentation](https://github.com/invertase/react-native-firebase-docs/blob/ba1f39d6099ea384cb17ec9cc4a319e41e45154b/docs/firestore/android.md).

Add the `RNFirebaseFirestorePackage` to your `android/app/src/main/java/com/[app name]/MainApplication.java`:

```java
// ...
import com.facebook.react.ReactApplication;
import io.invertase.firebase.firestore.RNFirebaseFirestorePackage; // <-- Add this line

public class MainApplication extends Application implements ReactApplication {
    // ...

    @Override
    protected List<ReactPackage> getPackages() {
      @SuppressWarnings("UnnecessaryLocalVariable")
      List<ReactPackage> packages = new PackageList(this).getPackages();
      // Packages that cannot be autolinked yet can be added manually here, for example:
      // packages.add(new MyReactNativePackage());
      packages.add(new RNFirebaseFirestorePackage()); // <-- Add this line
      return packages;
    }
  };
  // ...
}
```

## Enable multidex

Adding Firestore to your Android app requires [`multiDexEnabled` to be set to `true`](https://developer.android.com/studio/build/multidex) in `android/app/build.gradle`:

```java
//..
android {
  //..
  
  defaultConfig {
    //..
    multiDexEnabled true  // needed for firestore:
  }
  //..
}
```
