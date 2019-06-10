# UserMetadata

Interface representing a user's metadata.

## Properties

### creationTime
[method]creationTime returns nullable string;[/method]

The date the user was created. This should be (and will be, in v6) a UTC string, for example 'Fri, 22 Sep 2017 01:49:58 GMT', but in v5 it is formatted as a string containing the time in milliseconds since 1 Jan 1970 UTC. For example, '1554052020521'.

### lastSignInTime
[method]lastSignInTime returns nullable string;[/method]

The date the user last signed in, This should be (and will be, in v6) a UTC string, for example 'Fri, 22 Sep 2017 01:49:58 GMT', but in v5 it is formatted as a string containing the time in milliseconds since 1 Jan 1970 UTC. For example, '1554052020521'.
