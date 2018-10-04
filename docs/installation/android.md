# Android Installation

## 1) Link RNFirebase

Run `react-native link react-native-firebase`

## 2. Setup google-services.json

A google-services.json file contains all of the information required by the Firebase Android SDK to connect to your Firebase project. To automatically generate the json file, [follow the instructions](https://firebase.google.com/docs/android/setup#add_firebase_to_your_app) on the Firebase console to "Add Firebase to your app".

Once downloaded, place this file in the root of your project at `android/app/google-services.json`.

> The following instructions are also described on the Firebase console when going through the wizard.

In order for Android to parse this file, add the google-services gradle plugin as a dependency to your project in the *project* level `build.gradle` file:

```groovy
buildscript {
  // ...
  dependencies {
    // ...
    classpath 'com.google.gms:google-services:{{ android.gms.google-services }}'
  }
}
```

To apply the plugin to your project, add the following to the **VERY BOTTOM** of your app `android/app/build.gradle` file:

```groovy
apply plugin: 'com.google.gms.google-services'
```

## 3. Add Firebase modules

The Firebase modules need to be installed as project dependencies. In the `android/app/build.gradle` file, add the following:

```groovy
dependencies {
  // This should be here already
  implementation project(':react-native-firebase')

  // Firebase dependencies
  implementation "com.google.android.gms:play-services-base:{{ android.gms.play-services-base }}"
  implementation "com.google.firebase:firebase-core:{{ android.firebase.core }}"

  ...
```

### Update Gradle

Due to some breaking changes in v12+ of the Android Firebase libraries, you'll need to upgrade your Gradle version to at least v4.4 and make a few other tweaks as follows:

1) In `android/gradle/wrapper/gradle-wrapper.properties`, update the gradle URL to `gradle-4.4-all.zip`
2) In `android/build.gradle` check that you have `google()` specified in the buildScript repositories section:

```groovy
buildscript {
    repositories {
        google()  // <-- Check this line exists and is above jcenter
        jcenter()
        // ...
    }
    // ...
}
```

3) In `android/build.gradle` update Android build tools to version `{{ android.build.tools }}`:

```groovy
classpath 'com.android.tools.build:gradle:{{ android.build.tools }}'
```

4) In `android/app/build.gradle` update all your `compile` statements to be `implementation`, e.g.

```groovy
implementation project(':react-native-firebase')
```

5) When running your app from within Android Studio, you may encounter `Missing Byte Code` errors.  This is due to a known issue with version 3.1.x of the android tools plugin: https://issuetracker.google.com/issues/72811718.  You'll need to disable Instant Run to get past this error.

### Update Google Play service maven repository

Google Play services from 11.2.0 onwards require their dependencies to be downloaded from Google's Maven respository so add the required reference to the repositories section of the project level `build.gradle` (`android/build.gradle`):

```groovy
allprojects {
    repositories {
        mavenLocal()
        google() // <-- Add this line above jcenter
        jcenter()
        maven {
            // All of React Native (JS, Obj-C sources, Android binaries) is installed from npm
            url "$rootDir/../node_modules/react-native/android"
        }
    }
}
```

### Using with Proguard enabled

When using react-native-firebase with Proguard enabled (`minifyEnabled true in android/app/build.gradle`) you need to update your proguard-rules.pro file (`android/app/proguard-rules.pro`) to include the following lines:
```
-keep class io.invertase.firebase.** { *; }
-dontwarn io.invertase.firebase.**
```

## 4. Install modules

The `RNFirebasePackage` only provides your application with access to [Core](version /core/reference/core) features. Check out the installation guides on the other modules for how to use other Firebase features.
