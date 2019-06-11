# Interstitial

```
firebase.admob.interstitial
```

An interstitial is a full screen advert which creates a new activity on top of React. As they need to be controlled, allowing the developer to choose when to display them they're not available as a component. Instead they're controlled via method calls. A single interstitial instance can only be shown once. If you want to display another, create a new one.

## Methods

### loadAd
[method]loadAd(request) returns void;[/method]

Starting loading an interstial from the Firebase servers with a given [ref admob.AdRequest#build] payload.

| Parameter |         |
| --------- | ------- |
| request   | **[ref admob.AdRequest#build]** <br /> An AdRequest.build object |

### on
[method]on(event, callback) returns void;[/method]

Listens for advert events. See [EventTypes](version /admob/reference#eventtypes) for more information.

| Parameter |         |
| --------- | ------- |
| event   | **[ref admob#EventTypes]** <br /> A single event type |
| callback   | **function** |

### isLoaded
[method]isLoaded() returns boolean;[/method]

Returns whether the current requested advert has loaded from the Firebase servers.

### show
[method]show() returns void;[/method]

Shows the loaded advert on the device.

## Example

```javascript
const advert = firebase.admob().interstitial('ca-app-pub-3940256099942544/1033173712');

const AdRequest = firebase.admob.AdRequest;
const request = new AdRequest();
request.addKeyword('foo').addKeyword('bar');

// Load the advert with our AdRequest
advert.loadAd(request.build());

advert.on('onAdLoaded', () => {
  console.log('Advert ready to show.');
});

// Simulate the interstitial being shown "sometime" later during the apps lifecycle
setTimeout(() => {
  if (advert.isLoaded()) {
    advert.show();
  } else {
    // Unable to show interstitial - not loaded yet.
  }
}, 1000);
```
