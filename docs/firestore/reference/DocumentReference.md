# DocumentReference

A DocumentReference refers to a document location in a Firestore database and can be used to write, read, or listen to the location. The document at the referenced location may or may not exist. A DocumentReference can also be used to create a CollectionReference to a subcollection.

## Properties

### firestore
[method]firestore returns [ref firestore.Firestore];[/method]

The Firestore the document is in. This is useful for performing transactions, for example.

### id
[method]id returns string;[/method]

The document's identifier within its collection.

### parent
[method]parent returns nullable [ref firestore.DocumentReference];[/method]

The Collection this DocumentReference belongs to.

## Methods

### collection
[method]collection(collectionPath) returns [ref firestore.CollectionReference];[/method]

Gets a CollectionReference instance that refers to the collection at the specified path.

| Parameter |         |
| --------- | ------- |
| collectionPath  | **string** <br /> A slash-separated path to a collection. |

### delete
[method]delete() returns Promise containing void;[/method]

Deletes the document referred to by this DocumentReference.

Returns a promise that resolves once the document has been successfully deleted from the backend (Note that it won't resolve while you're offline).

### get
[method]get() returns Promise containing [ref firestore.DocumentSnapshot];[/method]

Reads the document referred to by this DocumentReference.

Note: get() attempts to provide up-to-date data when possible by waiting for data from the server, but it may return cached data or fail if you are offline and the server cannot be reached.

### onSnapshot
[method]onSnapshot(optionsOrObserverOrOnNext, observerOrOnNextOrOnError, onError) returns function();[/method]

Attaches a listener for DocumentSnapshot events. You may either pass individual onNext and onError callbacks or pass a single observer object with next and error callbacks.

Returns an unsubscribe function.

| Parameter |         |
| --------- | ------- |
| optionsOrObserverOrOnNext  | **[ref firestore.MetadataChanges]** or **Object** or **function([ref firestore.DocumentSnapshot])** <br /> This can be an observer object or an onNext function callback. It can also be a [ref firestore.MetadataChanges] object to opt into events even when only metadata changed. |
| observerOrOnNextOrOnError  | **Object** or **function([ref firestore.DocumentSnapshot])** or  **function(Error)** <br /> If you provided options, this will be an observer object or your onNext callback. Else, it is an optional onError callback. |
| onError  | **function([ref firestore.SnapshotError])** (optional) <br /> If you didn't provide options and didn't use an observer object, this is the optional onError callback. |

### set
[method]set(data, options) returns Promise containing void;[/method]

Writes to the document referred to by this DocumentReference. If the document does not exist yet, it will be created. If you pass options, the provided data can be merged into the existing document.

Returns a promise that resolves once the data has been successfully written to the backend. (Note that it won't resolve while you're offline).

| Parameter |         |
| --------- | ------- |
| data  | **Object** <br /> An object of the fields and values for the document. <br /> Value must not be null. |
| options  | **[ref firestore.SetOptions]** (optional) <br /> An object to configure the set behavior. Pass {merge: true} to only replace the values specified in the data argument. Fields omitted will remain untouched. <br /> Value must not be null. |

### update
[method]update(...args) returns Promise containing void;[/method]

Updates fields in the document referred to by this DocumentReference. The update will fail if applied to a document that does not exist.

Nested fields can be updated by providing dot-separated field path strings or by providing FieldPath objects.

Returns a promise that resolves once the data has been successfully written to the backend (Note that it won't resolve while you're offline).

| Parameter |         |
| --------- | ------- |
| args  | **any type** <br /> Either an object containing all of the fields and values to update, or a series of arguments alternating between fields (as string or [ref firestore.FieldPath] objects) and values.. <br /> Value may be repeated. |
