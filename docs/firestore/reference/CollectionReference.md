# CollectionReference

## Properties

### firestore
[method]firestore returns [ref firestore.Firestore];[/method]

The Firestore for the Cloud Firestore database (useful for performing transactions, etc.).

### id
[method]id returns string;[/method]

The collection's identifier.

### parent
[method]parent returns nullable [ref firestore.DocumentReference];[/method]

A reference to the containing DocumentReference if this is a subcollection. If this isn't a subcollection, the reference is null.

## Methods

### add
[method]add(data) returns Promise containing [ref firestore.DocumentReference];[/method]

Adds a new document to this collection with the specified data, assigning it a document ID automatically.

Returns a Promise that resolves with a [ref firestore.DocumentReference] pointing to the newly created document after it has been written to the backend.

| Parameter |         |
| --------- | ------- |
| data  | **Object** <br /> Value must not be null. |

### doc
[method]doc(documentPath) returns [ref firestore.DocumentReference];[/method]

Gets a DocumentReference for the document within the collection at the specified path. If no path is specified, an automatically-generated unique ID will be used for the returned DocumentReference.

| Parameter |         |
| --------- | ------- |
| documentPath  | **string** (optional) <br /> A slash-separated path to a document. |

### endAt
[method]endAt(snapshotOrVarArgs) returns [ref firestore.Query];[/method]

Creates a new query where the results end at the provided document (inclusive). The end position is relative to the order of the query. The document must contain all of the fields provided in the orderBy of this query.

| Parameter |         |
| --------- | ------- |
| snapshotOrVarArgs  | The snapshot of the document the query results should end at or the field values to start this query at, in order of the query's order by. |

### endBefore
[method]endBefore(snapshotOrVarArgs) returns [ref firestore.Query];[/method]

Creates a new query where the results end at the provided document (inclusive). The end position is relative to the order of the query. The document must contain all of the fields provided in the orderBy of this query.

| Parameter |         |
| --------- | ------- |
| snapshotOrVarArgs  | The snapshot of the document the query results should end before or the field values to start this query at, in order of the query's order by. |

### get
[method]get() returns Promise containing [ref firestore.QuerySnapshot];[/method]

Executes the query and returns the results as a [ref firestore.QuerySnapshot].

### limit
[method]limit(limit) returns [ref firestore.Query];[/method]

Creates a new query where the results are limited to the specified number of documents.

| Parameter |         |
| --------- | ------- |
| limit  | **number** <br /> The maximum number of items to return. |

### onSnapshot
[method]onSnapshot(optionsOrObserverOrOnNext, observerOrOnNextOrOnError, onError, onCompletion) returns function();[/method]

Attaches a listener for QuerySnapshot events. You may either pass individual `onNext` and `onError` callbacks or pass a single observer object with `next` and `error` callbacks.

NOTE: Although an onCompletion callback can be provided, it will never be called because the snapshot stream is never-ending.

Returns an unsubscribe function.

| Parameter |         |
| --------- | ------- |
| optionsOrObserverOrOnNext  | This can be an observer object or an onNext function callback. This can be an observer object or an onNext function callback. It can also be a [ref firestore.MetadataChanges] object to opt into events even when only metadata changed. |
| observerOrOnNextOrOnError  | If you provided options, this will be an observer object or your onNext callback. Else, it is an optional onError callback. |
| onError  | (optional) <br /> If you didn't provide options and didn't use an observer object, this is the optional onError callback. Errors are instances of [ref firestore.SnapshotError] |
| onCompletion  | Value must not be null. |

### orderBy
[method]orderBy(fieldPath, directionStr) returns [ref firestore.Query];[/method]

Creates a new query where the results are sorted by the specified field, in descending or ascending order.

| Parameter |         |
| --------- | ------- |
| fieldPath  | **string** or **[ref firestore.FieldPath]** <br /> The field to sort by. |
| directionStr  | **string** (optional) <br /> Optional direction to sort by (asc or desc). If not specified, the default order is ascending. |

### startAfter
[method]startAfter(snapshotOrVarArgs) returns [ref firestore.Query];[/method]

Creates a new query where the results start after the provided document (exclusive). The starting position is relative to the order of the query. The document must contain all of the fields provided in the orderBy of this query.

| Parameter |         |
| --------- | ------- |
| snapshotOrVarArgs  | The snapshot of the document to start after or the field values to start this query at, in order of the query's order by. |

### startAt
[method]startAt(snapshotOrVarArgs) returns [ref firestore.Query];[/method]

Creates a new query where the results start at the provided document (inclusive). The starting position is relative to the order of the query. The document must contain all of the fields provided in the orderBy of the query.

| Parameter |         |
| --------- | ------- |
| snapshotOrVarArgs  | The snapshot of the document to start after or the field values to start this query at, in order of the query's order by. |

### where
[method]where(fieldPath, opStr, value) returns [ref firestore.Query];[/method]

Creates a new query that returns only documents that include the specified fields and where the values satisfy the constraints provided.

| Parameter |         |
| --------- | ------- |
| fieldPath  | **string** or **[ref firestore.FieldPath]** <br /> The path to compare. |
| opStr  | **string** <br /> The operation string (e.g "<", "<=", "==", ">", ">="). |
| value  | The value for comparison. |
