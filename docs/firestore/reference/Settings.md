# Settings

Specifies custom configurations for your Cloud Firestore instance. You must set these before invoking any other methods.

## Properties

### host
[method]host returns nullable boolean;[/method]

The hostname to connect to.

### persistence
[method]persistence returns nullable boolean;[/method]

Whether to use persistence.

### ssl
[method]ssl returns nullable boolean;[/method]

Whether to use SSL when connecting.

## Unsupported Properties

### timestampsInSnapshots
[method]timestampsInSnapshots returns nullable boolean;[/method]

?> Defaults to true now and is deprecated (will be removed in v6.0.0)

Enables/Disables the use of [ref firestore.Timestamp]'s for timestamp fields in `DocumentSnapshot`s.

Formerly, Firestore returned timestamp fields as `Date` but `Date` only supports millisecond precision, which leads to truncation and causes unexpected behavior when using a timestamp from a snapshot as a part of a subsequent query.
   
Setting `timestampsInSnapshots` to true (now default) will cause Firestore to return `Timestamp` values instead of `Date` avoiding this kind of problem. To make this work you must also change any code that uses `Date` to use `Timestamp` instead.

See [ref firestore.Timestamp].
