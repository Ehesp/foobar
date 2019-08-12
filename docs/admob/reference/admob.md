# Admob

```
firebase.admob
```

## Methods 

The following methods are accessed via the Admob instance `firebase.admob()`.

### initialize
[method]initialize(id) returns void;[/method]

Before using any AdMob feature, ensure you call the initialize method. This only needs to be done once per the apps lifecycle. Initialize takes your AdMob App ID, where you can find on your AdMob dashboard.

For testing purposes, you can use the Admob test app ID "ca-app-pub-3940256099942544~3347511713"

| Parameter |         |
| --------- | ------- |
| id   | **string**  |

### openDebugMenu
[method]openDebugMenu() returns void;[/method]

Opens a debug menu, allowing you to test your ads. This menu cannot be closed unless you reload your app.

### interstitial
[method]interstitial(unitId) returns [ref admob.Interstitial];[/method]

Returns a new [ref admob.Interstitial] to be loaded with a given unitId.

| Parameter |         |
| --------- | ------- |
| unitId   | **string** <br /> Ad unitId |

### rewarded
[method]rewarded(unitId) returns [ref admob.RewardedVideo];[/method]

Returns a new [ref admob.RewardedVideo] to be loaded with a given unitId.

| Parameter |         |
| --------- | ------- |
| unitId   | **string** <br /> Ad unitId |

## Statics

### Banner
[method]Banner returns [ref admob.Banner];[/method]

Returns a [ref admob.Banner] component.

### NativeExpress
[method]NativeExpress returns [ref admob.NativeExpress];[/method]

Returns a [ref admob.NativeExpress] component.

### AdRequest
[method]AdRequest returns [ref admob.AdRequest];[/method]

Returns a [ref admob.AdRequest] class.

### VideoOptions
[method]VideoOptions returns [ref admob.VideoOptions];[/method]

Returns a [ref admob.VideoOptions] class.

## Types

### EventTypes
[method]VideoOptions returns [EventTypes](https://github.com/invertase/react-native-firebase/blob/master/src/modules/admob/EventTypes.js#L2);[/method]

Returns an `Object` containing Admob event types.

### RewardedVideoEventTypes
[method]RewardedVideoEventTypes returns [RewardedVideoEventTypes](https://github.com/invertase/react-native-firebase/blob/master/src/modules/admob/EventTypes.js#L10);[/method]

Returns an `Object` containing [RewardedVideo](#rewarded) event types.

### NativeExpressEventTypes
[method]NativeExpressEventTypes returns [NativeExpressEventTypes](https://github.com/invertase/react-native-firebase/blob/master/src/modules/admob/EventTypes.js#L18);[/method]

Returns an `Object` containing [NativeExpress](#NativeExpress) event types.
