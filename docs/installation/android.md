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
    classpath 'com.google.gms:google-services:{{ android.google.services }}'
  }
}
```

To apply the plugin to your project, add the following to the **VERY BOTTOM** of your app `android/app/build.gradle` file:

```groovy
apply plugin: 'com.google.gms.google-services'
```

## 3. Include :react-native-firebase

Add  include `:react-native-firebase` to `android/settings.gradle` before your `:app` project include:

```groovy
include ':react-native-firebase'
project(':react-native-firebase').projectDir = new File(rootProject.projectDir, '../node_modules/react-native-firebase/android')

// Include of your project should be already here.
include ':app'
```

## 4. Add Firebase modules

The Firebase modules need to be installed as project dependencies. In the `android/app/build.gradle` file, add the following:

```groovy
dependencies {
  // This should be here already
  compile(project(':react-native-firebase')) {
    transitive = false
  }

  // Firebase dependencies
  implementation "com.google.android.gms:play-services-base:{{ android.firebase.version }}"
  implementation "com.google.firebase:firebase-core:{{ android.firebase.version }}"

  ...
```

### Update Google Play service maven repository

Google Play services from 11.2.0 onwards require their dependencies to be downloaded from Google's Maven respository so add the required reference to the repositories section of the project level `build.gradle` (`android/build.gradle`):

```groovy
allprojects {
    repositories {
        mavenLocal()
        jcenter()
        maven {
            // All of React Native (JS, Obj-C sources, Android binaries) is installed from npm
            url "$rootDir/../node_modules/react-native/android"
        }
        // -------------------------------------------------
        // Add this below the existing maven property above
        // -------------------------------------------------
        maven {
            url 'https://maven.google.com'
        }
    }
}
```

## 5. Install modules

The `RNFirebasePackage` only provides your application with access to [Core](version /core/reference/core) features. Check out the installation guides on the other modules for how to use other Firebase features.
