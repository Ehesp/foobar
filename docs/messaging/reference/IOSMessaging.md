# IOSMessaging

iOS specific messaging / APNS properties.

## Methods

### registerForRemoteNotifications
[method]registerForRemoteNotifications() returns Promise containing void;[/method]

Register for iOS remote notifications(APNS).

### getAPNSToken
[method]getAPNSToken() returns Promise containing nullable string;[/method]

Get current APNS token linked with firebase. 

Returns a promise that resolves with the token string if APNS is registered. Otherwise it resolves with null.
