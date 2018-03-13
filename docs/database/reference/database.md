# Database

```
firebase.database
```

## Methods

The following methods are accessed via the Database instance `firebase.database()`.

### goOffline
[method]goOffline() returns void;[/method]

Disconnects from the server (all Database operations will be completed offline).

The client automatically maintains a persistent connection to the Database server, which will remain active indefinitely and reconnect when disconnected. However, the goOffline() and goOnline() methods may be used to control the client connection in cases where a persistent connection is undesirable.

While offline, the client will no longer receive data updates from the Database. However, all Database operations performed locally will continue to immediately fire events, allowing your application to continue behaving normally. Additionally, each operation performed locally will automatically be queued and retried upon reconnection to the Database server.

To reconnect to the Database and begin receiving remote events, see [ref database.Database#goOnline].

[collapse Example]
```js
firebase.database().goOffline();
```
[/collapse]

### goOnline
[method]goOnline() returns void;[/method]

Reconnects to the server and synchronizes the offline Database state with the server state.

This method should be used after disabling the active connection with goOffline(). Once reconnected, the client will transmit the proper data and fire the appropriate events so that your client "catches up" automatically.


[collapse Example]
```js
firebase.database().goOnline();
```
[/collapse]

### ref
[method]ref(path) returns [ref database.Reference];[/method]

Returns a Reference representing the location in the Database corresponding to the provided path. If no path is provided, the Reference will point to the root of the Database.

[collapse Example]
```js
const ref = firebase.database().ref('path');
ref.update({ foo: 'bar' });
```
[/collapse]

| Parameter |         |
| --------- | ------- |
| path  | **string** (optional) <br /> Optional path representing the location the returned Reference will point. If not provided, the returned Reference will point to the root of the Database. |

### getServerTime
[method]getServerTime() returns number;[/method]

Gets the Firebase server current timestamp.

[collapse Example]
```js
const serverTime = firebase.database().getServerTime();
```
[/collapse]

## Unsupported Methods

### refFromURL
