# FieldValue

```
firebase.firestore.Timestamp
```

A Timestamp represents a point in time independent of any time zone or calendar, represented as seconds and fractions of seconds at nanosecond resolution in UTC Epoch time.


## Static Methods

### static fromDate
[methods]fromDate(date: Date) returns [ref firestore.Timestamp];[/methods]

Creates a new timestamp from the given date.

### static fromMillis
[methods]fromMillis(ms: number) returns [ref firestore.Timestamp];[/methods]

Creates a new timestamp from the given number of milliseconds.

### static now
[methods]now() returns [ref firestore.FieldValue];[/methods]

Creates a new timestamp with the current date, with millisecond precision.

## Methods

### isEqual
[methods]isEqual(otherTimestamp: Timestamp) returns boolean;[/methods]

Returns true if this Timestamp is equal to the provided one.

### toDate
[methods]toDate() returns Date;[/methods]

Convert a Timestamp to a JavaScript Date object. This conversion causes a loss of precision since Date objects only support millisecond precision.

### toMillis
[methods]toMillis() returns number;[/methods]

Convert a timestamp to a numeric timestamp (in milliseconds since epoch). This operation causes a loss of precision.
