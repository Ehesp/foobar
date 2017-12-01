# iOS Installation

!> Please note that there is a known issue when using Cocoapods with the `use_frameworks!` enabled.  This is explained [here](https://github.com/invertase/react-native-firebase/issues/252#issuecomment-316340974).  Unfortunately we don't currently have a workaround, but are engaging with Firebase directly to try and resolve the problem.

## 1) Link RNFirebase

Run `react-native link react-native-firebase`

## 2. Setup GoogleService-Info.plist

A `GoogleService-Info.plist` file contains all of the information required by the Firebase iOS SDK to connect to your Firebase project. To automatically generate the plist file, [follow the instructions](https://firebase.google.com/docs/ios/setup#add_firebase_to_your_app) on the Firebase console to "Add Firebase to your app".

Once downloaded, place the file in the root of your iOS app at `ios/[YOUR APP NAME]/GoogleService-Info.plist`.

Make sure that the `GoogleService-Info.plist` file has been added to your project within XCode.

## 3. Initialize Firebase

> The following instructions are also described on the Firebase console when going through the wizard.

To initilize the native SDK in your app, add the following to your `ios/[YOUR APP NAME]/AppDelegate.m` file:

A) At the top of the file:

```objectivec
#import <Firebase.h>
```

B) At the beginning of the `didFinishLaunchingWithOptions:(NSDictionary *)launchOptions` method add the following line:

```objectivec
[FIRApp configure];
```

**WARNING: It is recommended to add the line within the method BEFORE creating the RCTRootView. Otherwise the initialization can happen too late after already being needed in your JavaScript code**

## 4. Setup Firebase Pods

Firebase recommends using Cocoapods to install the Firebase SDK.

We don't recommend it, but if for some reason you are unable to use Cocoapods, then you need to manually add the Firebase frameworks to an `ios/Firebase` folder for them to be recognised.

### 4.0) If you don't already have Cocoapods set up
Follow the instructions to install Cocoapods and create your Podfile [here](https://firebase.google.com/docs/ios/setup#add_the_sdk).

**NOTE: The Podfile needs to be initialized in the `ios` directory of your project. Make sure to update cocoapods libs first by running `pod update`**

#### Troubleshooting
1) When running `pod install` you may encounter an error saying that a `tvOSTests` target is declared twice. This appears to be a bug with `pod init` and the way that react native is set up.

**Resolution:**
- Open your Podfile
- Remove the duplicate `tvOSTests` target nested within the main project target
- Re-run `pod install`.

2) When running `pod install` you may encounter a number of warnings relating to `target overrides 'OTHER_LDFLAGS'`.

**Resolution:**
- Open Xcode
- Select your project
- For each target:
-- Select the target
-- Click Build settings
-- Search for `other linker flags`
-- Add `$(inherited)` as the top line if it doesn't already exist
- Re-run `pod install`

3) When running `pod install` you may encounter a warning that a default iOS platform has been assigned.  If you wish to specify a different minimum version:

**Resolution**
- Open your Podfile
- Uncomment the `# platform :ios, '9.0'` line by removing the `#` character
- Change the version as required

### 4.1) Check the Podfile platform version
We recommend using a minimum platform version of at least 9.0 for your application to ensure that the correct version of the Firebase libraries are used.  To do this, you need to uncomment or make sure the following line is present at the top of your `Podfile`:

`platform :ios, '9.0'`

### 4.2) Add the required pods
Simply add the following to your `Podfile` either at the top level, or within the main project target:

```ruby
# Required by RNFirebase
pod 'Firebase/Core'
```

Run `pod install`.

**NOTE: You need to use the `ios/[YOUR APP NAME].xcworkspace` instead of the `ios/[YOUR APP NAME].xcproj` file from now on.**

## 5. Install modules

`RNFirebase` only provides your application with access to [Core](version /core/reference) features. Check out the installation guides on the other modules for how to use other Firebase features.
