# Query

A Query refers to a Query which you can read or listen to. You can also construct refined Query objects by adding filters and ordering.

## Properties

### firestore
[method]firestore returns [ref firestore.Firestore];[/method]

The Firestore for the Cloud Firestore database (useful for performing transactions, etc.).

## Methods

### endAt
[method]endAt(snapshotOrVarArgs) returns [ref firestore.Query];[/method]

Creates a new query where the results end at the provided document (inclusive). The end position is relative to the order of the query. The document must contain all of the fields provided in the orderBy of this query.

| Parameter |         |
| --------- | ------- |
| snapshotOrVarArgs  | The snapshot of the document the query results should end at or the field values to start this query at, in order of the query's order by. |

### endBefore
[method]endBefore(snapshotOrVarArgs) returns [ref firestore.Query];[/method]

Creates a new query where the results end before the provided document (exclusive). The end position is relative to the order of the query. The document must contain all of the fields provided in the orderBy of this query.

| Parameter |         |
| --------- | ------- |
| snapshotOrVarArgs  | The snapshot of the document the query results should end before or the field values to start this query at, in order of the query's order by. |

### get
[method]get() returns Promise containing [ref firestore.QuerySnapshot];[/method]

Executes the query and returns the results as a QuerySnapshot.

### limit
[method]limit(limit) returns [ref firestore.Query];[/method]

Creates a new query where the results are limited to the specified number of documents.

| Parameter |         |
| --------- | ------- |
| limit  | **number** <br /> The maximum number of items to return. |

### onSnapshot
[method]onSnapshot(optionsOrObserverOrOnNext, observerOrOnNextOrOnError, onError, onCompletion) returns void;[/method]

Attaches a listener for QuerySnapshot events. You may either pass individual onNext and onError callbacks or pass a single observer object with next and error callbacks.

NOTE: Although an onCompletion callback can be provided, it will never be called because the snapshot stream is never-ending.

| Parameter |         |
| --------- | ------- |
| optionsOrObserverOrOnNext  | **[ref firestore.MetadataChanges]** or **Object** or **function([ref firestore.QuerySnapshot])** <br />This can be an observer object or an onNext function callback. It can also be a [ref firestore.MetadataChanges] object to opt into events even when only metadata changed. |
| observerOrOnNextOrOnError  | If you provided options, this will be an observer object or your onNext callback. Else, it is an optional onError callback. |
| onError  | (optional) <br /> If you didn't provide options and didn't use an observer object, this is the optional onError callback. |
| onCompletion  | Value must not be null. |

### orderBy
[method]orderBy(fieldPath, directionStr) returns [ref firestore.Query];[/method]

Creates a new query where the results are sorted by the specified field, in descendin or ascending order.

| Parameter |         |
| --------- | ------- |
| fieldPath  | **string** or **[ref firestore.FieldPath]** <br /> The field to sort by. |
| directionStr  | **string** (optional) <br /> Optional direction to sort by (asc or desc). If not specified, the default order is ascending. |

### startAfter
[method]startAfter(snapshotOrVarArgs) returns [ref firestore.Query];[/method]

Creates a new query where the results start after the provided document (exclusive). The starting position is relative to the order of the query. The document must contain all of the fields provided in the orderBy of this query.

| Parameter |         |
| --------- | ------- |
| snapshotOrVarArgs  | The snapshot of the document to start after or the field values to start this query at, in order of the query's order by. |

### startAt
[method]startAt(snapshotOrVarArgs) returns [ref firestore.Query];[/method]

Creates a new query where the results start at the provided document (inclusive). The starting position is relative to the order of the query. The document must contain all of the fields provided in the orderBy of the query.

| Parameter |         |
| --------- | ------- |
| snapshotOrVarArgs  | The snapshot of the document to start after or the field values to start this query at, in order of the query's order by. |

### where
[method]where(fieldPath, opStr, value) returns [ref firestore.Query];[/method]

Creates a new query that returns only documents that include the specified fields and where the values satisfy the constraints provided.

| Parameter |         |
| --------- | ------- |
| fieldPath  | **string** or **[ref firestore.FieldPath]** <br /> The path to compare. |
| opStr  | **string** <br /> The operation string (e.g "<", "<=", "==", ">", ">="). |
| value  | The value for comparison. |
