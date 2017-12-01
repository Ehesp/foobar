# Release Notes

## Installation

```
npm i react-native-firebase@next
```

and follow the migration guide below (there isn't much to change).

## Known Issues

 - Currently no way (in JS) to set database persistence, you can however set this natively:
    - [android] add `FirebaseDatabase.getInstance().setPersistenceEnabled(true);` to your `MainApplication` `onCreate` method.
    - [ios] add `[FIRDatabase database].persistenceEnabled = YES;` after the `[FIRApp configure];` line  inside your `AppDelegate` `didFinishLaunchingWithOptions` method.
 - Currently no way to enable RNFirebase debug logging.
 - [android] no play store/play services version checks and associated methods.

## Flagging an Issue/Feature request

Please follow the standard issue template but start your issue title with `[v3]` so we can pick these up easier. For brownie points add an additional module tag right after it i.e. `[v3][database]`

## Contributing to v3

### Docs
We'd love some help on the docs, there's a lot of sections lacking docs and several features are 
currently undocumented (see todo annotations in change log below). The docs are located in the `/docs` folder - you can use the online GH markdown editor if needed to update the docs. To add a sidebar section to the docs you can add it on the `_sidebar.md` file in the root of the docs folder and create an associated markdown file to go with it.

### Issue Fixes / Feature additions

For other changes, clone the master branch and follow the contributing [guidelines](https://invertase.io/react-native-firebase/#/contributing/guidelines). For instructions on running the testing suite/playground see the testing [guide](https://invertase.io/react-native-firebase/#/contributing/testing).

---

## Change log

### CHANGE LOG STILL WIP.

This release is mainly aimed at adding firebase 'core' functionality and further adjustments to bring the modules in line with the web sdk api. Additionally there's been a lot of internal code improvements aimed at performance and improving QoL for module development.

Whilst every effort has been taken to document all breaking changes there may still be a chance that some undocumented breaking changes have snuck in as this was probably one of the largest releases to date code wise. 🙈 

## Migration guide (WIP)

### Android
- You can update all your Firebase dependencies to 11.2.0 in `android/app/build.gradle`
- You must add `maven { url 'https://maven.google.com' }` to your `android/build.gradle` as follows:
```groovy
// Top-level build file where you can add configuration options common to all sub-projects/modules.

buildscript {
    repositories {
        jcenter()
    }
    dependencies {
        classpath 'com.android.tools.build:gradle:2.2.3'
        classpath 'com.google.gms:google-services:3.1.0'
        classpath 'com.google.firebase:firebase-plugins:1.1.1'

        // NOTE: Do not place your application dependencies here; they belong
        // in the individual module build.gradle files
    }
}

allprojects {
    repositories {
        mavenLocal()
        jcenter()
        maven {
            // All of React Native (JS, Obj-C sources, Android binaries) is installed from npm
            url "$rootDir/../node_modules/react-native/android"
        }
        // ADD THIS SECTION HERE
        maven {
            url 'https://maven.google.com'
        }
    }
}
```

## Core
This release introduces full [firebase core](https://firebase.google.com/docs/reference/js/firebase) support. This means multiple firebase apps are now supported both in JS and native android/ios code (initialize additional apps on either end to have the app available in both automatically).

- ![#f03c15](https://placehold.it/15/f03c15/000000?text=+) **[breaking]** `new RNFirebase()` is no longer supported. See below for information about app initialisation.
- ![#f03c15](https://placehold.it/15/fdfd96/000000?text=+) **[deprecation]** `initializeApp()` for apps that are already initialized natively (i.e. the default app initialized via google-services plist/json) will now log a deprecation warning. 
    - As these apps are already initialized natively there's no need to call `initializeApp` in your JS code. For now, calling it will just return the app that's already internally initialized - in a future version this will throw an `already initialized` exception.
    - Accessing apps can now be done the same way as the web sdk, simply call `firebase.app()` to get the default app, or with the name of specific app as the first arg, e.g. `const meow = firebase.app('catsApp');` to get a specific app.
- `FirebaseApp.extendApp(props: Object)` support added.
- RNFirebase no longer requires a singleton exported instance of your app to work (though you can still do this if you'd like). You can now just import RNFirebase in any module and straight away access all the initialized apps. e.g. : 
```javascript 
import firebase from 'react-native-firebase';

// get started immediately with the default app for example
firebase.database().ref('kittens').once('value', (snapshot) => {
     console.log('kittenslol', snapshot.val());
});

// or get some other app
const dogsApp = firebase.apps('doge');

// then it's either:

// 1)
dogsApp.database().ref('puppies').once('value', (snapshot) => {
     console.log('muchwow', snapshot.val());
});

// 2) or this one
firebase.database(dogsApp).ref('puppies').once('value', (snapshot) => {
     console.log('muchwow', snapshot.val());
});
```

- **TODO** initialising apps via js
    - **TODO** explain why js app initialisation is not supported for the default app (firebase sdk limited module support etc)
    - **TODO** explain `app.onReady(): Promise` and why it's needed for JS initialized apps.
- **TODO** what firebase modules support multiple apps
- **TODO** delete app caveats - e.g cannot delete default apps, cannot delete apps on android, cannot get app config clientId on ios - see issue comments on firebase repo: https://github.com/firebase/firebase-ios-sdk/issues/140#issuecomment-315953708
- **TODO** `firebase.SDK_VERSION`
- **TODO** `firebase.DEFAULT_APP_NAME`


## Auth 
- `auth()` now supports passing an instance of [App](https://firebase.google.com/docs/reference/js/firebase.app.App) as the first argument
- **TODO** phone authentication 👀  #119 
- ![#f03c15](https://placehold.it/15/f03c15/000000?text=+) **[breaking]** Third party providers now user `providerId` rather than `provider` as per the Web SDK.  If you are manually creating your credentials, you will need to update the field name.

## Database 
- `database()` now supports passing an instance of [App](https://firebase.google.com/docs/reference/js/firebase.app.App) as the first argument
- `once` now supports `context` as per the web sdk
- `remove` now supports onComplete callbacks (and promises) as per the web sdk
- `update` now supports onComplete callbacks (and promises) as per the web sdk
- `setWithPriority` now supports onComplete callbacks (and promises) as per the web sdk
- `setPriority` now supports onComplete callbacks (and promises) as per the web sdk
- `set` now supports onComplete callbacks (and promises) as per the web sdk
- `keepSynced` now correctly takes into account query modifiers natively, was ignoring these before
- improved native `transaction` implementations to have better error handling and timeout checks (mainly for whilst running in dev)
    - **[websdk-diff]** the web sdk transaction errors return [one worded errors](https://github.com/firebase/firebase-js-sdk/blob/master/src/database/core/Repo_transaction.ts#L758) that don't make much sense and have no error codes or description like all the other database errors do. RNFirebase internally maps these into the database error codes we're accustomed to, for example the one worder above comes back as `The transaction was overridden by a subsequent set. (database/overridden-by-set)` instead. 
- [ios] implemented missing `onDisconnectUpdate` method. See #272. 
- ![#f03c15](https://placehold.it/15/f03c15/000000?text=+) **[breaking]** error messages and codes internally re-written to match the web sdk
- ![#f03c15](https://placehold.it/15/f03c15/000000?text=+) **[breaking]** `ref.isEqual` now checks the query modifiers as well as the ref path (was just path before). With the release of multi apps/core support this check now also includes whether the refs are for the same app.
- ![#f03c15](https://placehold.it/15/f03c15/000000?text=+) **[breaking]** on/off behaviour changes. Previous `off` behaviour was incorrect. A `SyncTree/Repo` implementation was added to provide the correct behaviour you'd expect in the web sdk. Whilst this is a breaking change it shouldn't be much of an issue if you've previously setup your on/off handling correctly. See #160 for specifics of this change. 
- [internal] re-wrote native android & ios methods to now use RN promise implementation - was callbacks before with a callback to promise wrapper in JS
- [js] `ThenableReference` support implemented, for now this is just for `.push()`.  See #147.


## Storage 
- `storage()` now supports passing an instance of [App](https://firebase.google.com/docs/reference/js/firebase.app.App) as the first argument
- [ios] `putFile` now sets the remote file `content/type` automatically for images and videos (Android TODO)
- ![#f03c15](https://placehold.it/15/f03c15/000000?text=+) **[breaking]** UploadTaskSnapshot -> `downloadUrl` renamed to `downloadURL` to match web sdk


## Misc

- We're now using `Apache License 2.0` to license this library. 
- [internal] re-wrote event emitter / subscriptions logic to be more performant and to support multiple database/app instances. This is for events such as storage task events, database transaction/realtime events and authentication state changes.
- QoL change: added more descriptive errors on incorrect setup of native modules, e.g: 
![image](https://user-images.githubusercontent.com/5347038/29463240-f08bc7c0-8429-11e7-9671-f92b4da97277.png)
- QoL change: added Groovy script to RNFirebase build.gradle to automatically detect duplicate dex build failures:
![image](https://user-images.githubusercontent.com/5347038/29476094-572dcc5a-845a-11e7-95da-276b9c6b1170.png)
