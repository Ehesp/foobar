# IOSParameters

IOS specific link settings.

## Methods

### setAppStoreId
[method]setAppStoreId(appStoreId) returns [ref links.DynamicLink];[/method]

Sets the App Store ID, used to send users to the App Store when the app isn't installed.

| Parameter |         |
| --------- | ------- |
| appStoreId  | **string** <br /> The App Store ID. |

### setBundleId
[method]setBundleId(bundleId) returns [ref links.DynamicLink];[/method]

Sets the iOS bundle ID.

| Parameter |         |
| --------- | ------- |
| bundleId  | **string** <br /> The parameters ID of the iOS app to use to open the link. The app must be connected to your project from the Overview page of the Firebase console. |

### setCustomScheme
[method]setCustomScheme(customScheme) returns [ref links.DynamicLink];[/method]

Sets the app's custom URL scheme, if defined to be something other than your app's parameters ID.

| Parameter |         |
| --------- | ------- |
| customScheme  | **string** <br /> The app's custom URL scheme. |

### setFallbackUrl
[method]setFallbackUrl(fallbackUrl) returns [ref links.DynamicLink];[/method]

Sets the link to open when the app isn't installed. Specify this to do something other than install your app from the App Store when the app isn't installed, such as open the mobile web version of the content, or display a promotional page for your app.

| Parameter |         |
| --------- | ------- |
| fallbackUrl  | **string** <br /> The link to open on iOS if the app is not installed. |

### setIPadBundleId
[method]setIPadBundleId(iPadBundleId) returns [ref links.DynamicLink];[/method]

Sets the parameters ID of the iOS app to use on iPads to open the link. The app must be connected to your project from the Overview page of the Firebase console.

| Parameter |         |
| --------- | ------- |
| iPadBundleId  | **string** <br /> The iPad parameters ID of the app. |

### setIPadFallbackUrl
[method]setIPadFallbackUrl(iPadFallbackUrl) returns [ref links.DynamicLink];[/method]

Sets the link to open on iPads when the app isn't installed. Specify this to do something other than install your app from the App Store when the app isn't installed, such as open the web version of the content, or display a promotional page for your app. Overrides the fallback link set by `setFallbackUrl` on iPad.

| Parameter |         |
| --------- | ------- |
| iPadFallbackUrl  | **string** <br /> The link to open on iPad if the app is not installed. |

### setMinimumVersion
[method]setMinimumVersion(minimumVersion) returns [ref links.DynamicLink];[/method]

Sets the minimum version of your app that can open the link.

| Parameter |         |
| --------- | ------- |
| minimumVersion  | **string** <br /> The minimum version. |
