# iOS Installation

First ensure you have followed the [initial setup guide](version /installation/initial-setup).

## Pods (recommended)

### Add the pods

Add the following to your `Podfile`:

```ruby
pod 'Fabric', '~> {{ ios.fabric.tools }}'
pod 'Crashlytics', '~> {{ ios.firebase.crashlytics }}'
```

Run `pod update`.

### Add the Crashlytics run script

1. Open your project in Xcode and select its project file in the Navigator
2. Open the **Build Phases** tab.
3. Click **+ Add a new build phase**, and select **New Run Script Phase**.
4. Add the following line to the **Type a script..** text box:

```groovy
"${PODS_ROOT}/Fabric/run"
```

## Manual

### Add to project
1. Go and download the [crashlytics iOS library](https://fabric.io/kits/ios/crashlytics/manual-install).
2. Add the `Crashytics.framework` and `Fabric.framework` to your iOS project.
3. Add both frameworks to "Link Binary With Libraries" in your Build Phases.
4. Add `$(PROJECT_DIR)/Firebase/Fabric` and `$(PROJECT_DIR)/Firebase/Crashlytics` to your "Header Search Paths" in Build Settings (Assuming Fabric and Crashlytics libraries are in a folder called `Firebase/Crashlytics`).

### Add the Crashlytics run script

1. Open your project in Xcode and select its project file in the Navigator
2. Open the **Build Phases** tab.
3. Click **+ Add a new build phase**, and select **New Run Script Phase**.
4. Add the following line to the **Type a script..** text box (Assuming the Fabric library is in `${SRCROOT}/Firebase/Fabric`):

```groovy
"${SRCROOT}/Firebase/Fabric/Fabric.framework/run"
```

5. **Xcode 10 only:** Add your app's built Info.plist location to the Build Phase's Input Files field:

```groovy
$(BUILT_PRODUCTS_DIR)/$(INFOPLIST_PATH)
```


----

**Source:** [Firebase Crashlytics - Getting Started - iOS](https://firebase.google.com/docs/crashlytics/get-started#ios)
