# iOS Installation

First ensure you have followed the [initial setup guide](version /installation/initial-setup).

## Add the pods

Add the following to your `Podfile`:

```ruby
pod 'Fabric', '~> {{ ios.fabric.tools }}'
pod 'Crashlytics', '~> {{ ios.firebase.crashlytics }}'
```

Run `pod update`.

## Add the Crashlytics run script

1. Open your project in Xcode and select its project file in the Navigator
2. Open the **Build Phases** tab.
3. Click **+ Add a new build phase**, and select **New Run Script Phase**.
4. Add the following line to the **Type a script..** text box:

```groovy
"${PODS_ROOT}/Fabric/run"
```
