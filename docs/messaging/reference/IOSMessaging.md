# IOSMessaging

iOS specific messaging / APNS properties.

## Methods

### registerForRemoteNotifications
[method]registerForRemoteNotifications() returns Promise<void>;[/method]

Register for iOS remote notifications(APNS).

### getAPNSToken
[method]getAPNSToken() returns Promise<string | null>;[/method]

Get current APNS token linked with firebase. 
