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
