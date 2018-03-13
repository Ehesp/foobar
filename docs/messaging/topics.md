# Topic Messaging

Based on the publish/subscribe model, FCM topic messaging allows you to send a message to multiple devices that have opted in to a particular topic. You compose topic messages as needed, and FCM handles routing and delivering the message reliably to the right devices.

For example, users of a local weather forecasting app could opt in to a "severe weather alerts" topic and receive notifications of storms threatening specified areas. Users of a sports app could subscribe to automatic updates in live game scores for their favourite teams.

Some things to keep in mind about topics:

- Topic messaging supports unlimited topics and subscriptions for each app.
- Topic messaging is best suited for content such as news, weather, or other publicly available information.
- Topic messages are optimized for throughput rather than latency. For fast, secure delivery to single devices or small groups of devices, target messages to registration tokens, not topics.
- If you need to send messages to multiple devices per user, consider device group messaging for those use cases.

## 1) Subscribe the client app to a topic

Client apps can subscribe to any existing topic, or they can create a new topic. When a client app subscribes to a new topic name (one that does not already exist for your Firebase project), a new topic of that name is created in FCM and any client can subsequently subscribe to it.

To subscribe to a topic:

```js
firebase.messaging().subscribeToTopic(topicName);
```

To unsubscribe from a topic:

```js
firebase.messaging().unsubscribeFromTopic(topicName);
```

## 2) Receive and handle topic messages

FCM delivers topic messages in the same way as other downstream messages.

To receive messages, make use of the `onMessage` method described in [Receiving Messages](version /messaging/receiving-messages).
