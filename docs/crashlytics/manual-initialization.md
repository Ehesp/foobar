# Manual Initialization

By default, Firebase Crashlytics automatically collects crash reports for all your app's users. To give users more control over the data they send, you can enable opt-in reporting instead.

To do that, you have to disable automatic collection and initialize Crashlytics only for opt-in users.

## 1) Disable automatic initialization

### iOS:

Turn off automatic collection with a new key to your `Info.plist` file:

* Key: `firebase_crashlytics_collection_enabled`
* Value: `false`

### Android:

Turn off automatic collection with a meta-data tag in your `AndroidManifest.xml` file:

```xml
<meta-data
    android:name="firebase_crashlytics_collection_enabled"
    android:value="false" />
```

## 2) Enable collection at runtime

Initializing Crashlytics in your js code:

```js
firebase.crashlytics().enableCrashlyticsCollection();
```
