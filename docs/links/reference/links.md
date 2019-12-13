# Dynamic Links

[Firebase Dynamic Links](https://firebase.google.com/docs/dynamic-links/) allows you to create and receive links on both Android and iOS platforms.
Assuming the platform specific installation instructions have been followed, Firebase Dynamic Links is ready to go.

React Native Firebase mimics the [Firebase REST API](https://firebase.google.com/docs/dynamic-links/rest) for Dynamic Links creation with a few minor differences:

1. The input for the methods is a javascript object instead of a JSON object.
2. The response contains the URL string only.
3. There is no `dynamicLinkInfo` element. Instead, all of the elements under it were moved into the top-level.

## Methods

The following methods are accessed via the default app's Dynamic Links instance `firebase.links()`.

### createDynamicLink
[method]createDynamicLink(link) returns Promise<string>;[/method]

Creates a standard dynamic link.

| Parameter | Type |
| --------- | ------- |
| link   | **[ref links.DynamicLink]**  |

[collapse Example]
```javascript
const link = 
  new firebase.links.DynamicLink('https://example.com?param1=foo&param2=bar', 'abc123.page.link')
    .android.setPackageName('com.example.android')
    .ios.setBundleId('com.example.ios');

firebase.links()
    .createDynamicLink(link)
    .then((url) => {
      // ...
    });
```
[/collapse]

### createShortDynamicLink
[method]createShortDynamicLink(link, type) returns Promise<string>;[/method]

Creates a short dynamic link.

| Parameter | Type |
| --------- | ------- |
| link   | **[ref links.DynamicLink]**  |
| type   | **(Optional)`SHORT` or `UNGUESSABLE`**  |

[collapse Example]
```javascript
const link = 
  new firebase.links.DynamicLink('https://example.com?param1=foo&param2=bar', 'abc123.page.link')
    .android.setPackageName('com.example.android')
    .ios.setBundleId('com.example.ios');

firebase.links()
    .createShortDynamicLink(link, 'UNGUESSABLE')
    .then((url) => {
      // ...
    });
```
[/collapse]

### getInitialLink
[method]getInitialLink() returns Promise<string|null>;[/method]

Returns the URL that the app has been launched from. If the app was not launched from a URL the return value will be null.

> Use [ref auth.auth#isSignInWithEmailLink] to check if an inbound dynamic link is an email sign-in link.

[collapse Example]
```javascript
firebase.links()
    .getInitialLink()
    .then((url) => {
        if (url) {
            // app opened from a url
        } else {
           // app NOT opened from a url
        }
    });
```
[/collapse]

### onLink
[method]onLink(listener: Function<string>) returns Function;[/method]

Subscribe to URL open events while the app is still running.

The listener is called from URL open events whilst the app is still running, use [getInitialLink](#getInitialLink) for URLs which cause the app to open from a previously closed / not running state.

Returns an unsubscribe function, call the returned function to unsubscribe from all future events.

> Use [ref auth.auth#isSignInWithEmailLink] to check if an inbound dynamic link is an email sign-in link.

[collapse Example]
```javascript
// subscribe
const unsubscribe = firebase.links().onLink((url) => {
  // ...
});

// unsubscribe
unsubscribe();
```
[/collapse]
