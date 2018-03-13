# Sending Upstream Messages

If your app server implements the XMPP Connection Server protocol, it can receive upstream messages from a user's device to the cloud. To initiate an upstream message, the client app sends a request containing the following:

- The address of the receiving app server in the format SENDER_ID@gcm.googleapis.com.
- A message ID that should be unique for each sender ID.
- The message data comprising the key-value pairs of the message's payload.

When it receives this data, FCM builds an XMPP stanza to send to the app server, adding some additional information about the sending device and app.

## Send an upstream message

Your app can send an upstream message using `sendMessage`:

```js
// Create a RemoteMessage
const message = new firebase.messaging.RemoteMessage()
  .setMessageId('unique id')
  .setTo('senderId@gcm.googleapis.com')
  .setData({
    key1: 'value1',
    key2: 'value2',
  });
// Send the message
firebase.messaging().sendMessage(message);
```