# AndroidNotifications

This deals with Android-specific Notification functionality.

## Methods

The following methods are accessed via the AndroidNotifications instance `firebase.notifications().android`

createChannel(channel: AndroidChannel): Promise<void> {
    createChannelGroup(channelGroup: AndroidChannelGroup): Promise<void> {
        createChannelGroups(channelGroups: AndroidChannelGroup[]): Promise<void> {
            createChannels(channels: AndroidChannel[]): Promise<void> {


### createChannel
[method]createChannel(channel) returns Promise;[/method]

Creates a new channel.

Returns a promise that resolves if the channel is created, otherwise it is rejected with an error.

| Parameter |         |
| --------- | ------- |
| channel   | **[ref notifications.AndroidChannel]** <br /> The channel to create.  |

### createChannelGroup
[method]createChannelGroup(channelGroup) returns Promise;[/method]

Creates a new channel group.

Returns a promise that resolves if the channel group is created, otherwise it is rejected with an error.

| Parameter |         |
| --------- | ------- |
| channelGroup   | **[ref notifications.AndroidChannelGroup]** <br /> The channel group to create.  |

### createChannelGroups
[method]createChannelGroups(channelGroups) returns Promise;[/method]

Creates multiple new channel grousps

Returns a promise that resolves if the channel groups are created, otherwise it is rejected with an error.

| Parameter |         |
| --------- | ------- |
| channelGroups   | **Array<[ref notifications.AndroidChannelGroup]>** <br /> The channel groups to create.  |

### createChannels
[method]createChannels(channels) returns Promise;[/method]

Creates multiple new channels.

Returns a promise that resolves if the channels are created, otherwise it is rejected with an error.

| Parameter |         |
| --------- | ------- |
| channels   | **Array<[ref notifications.AndroidChannel]>** <br /> The channels to create.  |
