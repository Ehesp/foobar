# Rewarded Video

```
firebase.admob.rewarded
```

A rewarded video allows you to display a video to a user, whereby they're able to watch it to gain "rewards", or skip it
and receive nothing. For example, when a user completes a level on your gaming app, show them a video which will give them in-game
credit.

A single rewarded video instance can only be shown once. If you want to display another, create a new one.

> It's recommended you begin loading the video as soon as possible.

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
| event   | **[ref admob#EventTypes]** or **[ref admob#RewardedVideoEventTypes]** <br /> A single event type |
| callback   | **function** |

### isLoaded
[method]isLoaded() returns boolean;[/method]

Returns whether the current requested advert has loaded from the Firebase servers.

### show
[method]show() returns void;[/method]

Shows the loaded advert on the device.

## Example

```js
const advert = firebase.admob().rewarded('ca-app-pub-3940256099942544/1033173712');

const AdRequest = firebase.admob.AdRequest;
const request = new AdRequest();
request.addKeyword('foo').addKeyword('bar');

// Load the advert with our AdRequest
advert.loadAd(request.build());

advert.on('onAdLoaded', () => {
  console.log('Advert ready to show.');
});

advert.on('onRewarded', (event) => {
  console.log('The user watched the entire video and will now be rewarded!', event);
});

...

onLevelComplete()
  .then(() => {
    if (advert.isLoaded()) {
      advert.show();
    } else {
      // skip...
    }
  });
```
