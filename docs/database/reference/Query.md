# Query

A Query sorts and filters the data at a Database location so only a subset of the child data is included. This can be used to order a collection of data by some attribute (for example, height of dinosaurs) as well as to restrict a large list of items (for example, chat messages) down to a number suitable for synchronizing to the client. Queries are created by chaining together one or more of the filter methods defined here.

Just as with a Reference, you can receive data from a Query by using the on() method. You will only receive events and DataSnapshots for the subset of the data that matches your query.

Read our documentation on [Sorting and filtering data](https://firebase.google.com/docs/database/web/lists-of-data#sorting_and_filtering_data) for more information.

## Properties

### ref
[method]ref returns non-null [ref database.Reference];[/method]

Returns a Reference to the Query's location.

## Methods

### endAt
[method]endAt(value, key) returns [ref database.Query];[/method]

Creates a Query with the specified ending point.

Using `startAt()`, `endAt()`, and `equalTo()` allows you to choose arbitrary starting and ending points for your queries.

The ending point is inclusive, so children with exactly the specified value will be included in the query. The optional key argument can be used to further limit the range of the query. If it is specified, then children that have exactly the specified value must also have a key name less than or equal to the specified key.

You can read more about endAt() in [Filtering data](https://firebase.google.com/docs/database/web/lists-of-data#filtering_data).

| Parameter |         |
| --------- | ------- |
| value  | **string** or **number** or **boolean** or **null** <br /> The value to end at. The argument type depends on which orderBy*() function was used in this query. Specify a value that matches the orderBy*() type. When used in combination with orderByKey(), the value must be a string. |
| key  | **string** (optional) <br /> The child key to end at, among the children with the previously specified priority. This argument is only allowed if ordering by child, value, or priority. |

### equalTo
[method]equalTo(value, key) returns [ref database.Query];[/method]

Creates a Query with the specified ending point.

Using `startAt()`, `endAt()`, and `equalTo()` allows you to choose arbitrary starting and ending points for your queries.

The ending point is inclusive, so children with exactly the specified value will be included in the query. The optional key argument can be used to further limit the range of the query. If it is specified, then children that have exactly the specified value must also have a key name less than or equal to the specified key.

You can read more about endAt() in [Filtering data](https://firebase.google.com/docs/database/web/lists-of-data#filtering_data).

| Parameter |         |
| --------- | ------- |
| value  | **string** or **number** or **boolean** or **null** <br /> The value to end at. The argument type depends on which orderBy*() function was used in this query. Specify a value that matches the orderBy*() type. When used in combination with orderByKey(), the value must be a string. |
| key  | **string** (optional) <br /> The child key to end at, among the children with the previously specified priority. This argument is only allowed if ordering by child, value, or priority. |

### isEqual
[method]isEqual(query) returns boolean;[/method]

Returns whether or not the current and provided queries represent the same location, have the same query parameters, and are from the same instance of firebase.app.App.

Two Reference objects are equivalent if they represent the same location and are from the same instance of firebase.app.App.

Two Query objects are equivalent if they represent the same location, have the same query parameters, and are from the same instance of firebase.app.App. Equivalent queries share the same sort order, limits, and starting and ending points.

| Parameter |         |
| --------- | ------- |
| query  | **[ref database.Query]** <br /> The query to compare against. |

### limitToFirst
[method]limitToFirst(query) returns [ref database.Query];[/method]

Generates a new Query limited to the first specific number of children.

The limitToFirst() method is used to set a maximum number of children to be synced for a given callback. If we set a limit of 100, we will initially only receive up to 100 child_added events. If we have fewer than 100 messages stored in our Database, a child_added event will fire for each message. However, if we have over 100 messages, we will only receive a child_added event for the first 100 ordered messages. As items change, we will receive child_removed events for each item that drops out of the active list so that the total number stays at 100.

You can read more about limitToFirst() in [Filtering data](https://firebase.google.com/docs/database/web/lists-of-data#filtering_data).

| Parameter |         |
| --------- | ------- |
| query  | **limit** <br /> The maximum number of nodes to include in this query. |

### limitToLast
[method]limitToLast(limit) returns [ref database.Query];[/method]

Generates a new Query object limited to the last specific number of children.

The `limitToLast()` method is used to set a maximum number of children to be synced for a given callback. If we set a limit of 100, we will initially only receive up to 100 child_added events. If we have fewer than 100 messages stored in our Database, a child_added event will fire for each message. However, if we have over 100 messages, we will only receive a child_added event for the last 100 ordered messages. As items change, we will receive child_removed events for each item that drops out of the active list so that the total number stays at 100.

| Parameter |         |
| --------- | ------- |
| limit   | **number** <br /> The maximum number of nodes to include in this query. |

### off
[method]off(eventType, callback, context) returns void;[/method]

Detaches a callback previously attached with `on()`.

Detach a callback previously attached with `on()`. Note that if on() was called multiple times with the same eventType and callback, the callback will be called multiple times for each event, and off() must be called multiple times to remove the callback. Calling off() on a parent listener will not automatically remove listeners registered on child nodes, off() must also be called on any child listeners to remove the callback.

If a callback is not specified, all callbacks for the specified eventType will be removed. Similarly, if no eventType or callback is specified, all callbacks for the Reference will be removed.

| Parameter |         |
| --------- | ------- |
| eventType   | **string** (optional) <br /> One of the following strings: "value", "child_added", "child_changed", "child_removed", or "child_moved." |
| callback   | **function** (optional) <br /> The callback function that was passed to on(). |
| context   | **Object** (optional) <br /> The context that was passed to on(). |

### on
[method]on(eventType, callback, cancelCallbackOrContext, context) returns function();[/method]

Listens for data changes at a particular location.

This is the primary way to read data from a Database. Your callback will be triggered for the initial data and again whenever the data changes. Use off() to stop receiving updates.

The provided callback function is returned unmodified. This is just for convenience if you want to pass an inline function to on() but store the callback function for later passing to off().

#### 'value' event

This event will trigger once with the initial data stored at this location, and then trigger again each time the data changes. The DataSnapshot passed to the callback will be for the location at which on() was called. It won't trigger until the entire contents has been synchronized. If the location has no data, it will be triggered with an empty DataSnapshot (val() will return null).

#### 'child_added' event

This event will be triggered once for each initial child at this location, and it will be triggered again every time a new child is added. The DataSnapshot passed into the callback will reflect the data for the relevant child. For ordering purposes, it is passed a second argument which is a string containing the key of the previous sibling child by sort order, or null if it is the first child.

#### 'child_removed' event

This event will be triggered once every time a child is removed. The DataSnapshot passed into the callback will be the old data for the child that was removed. A child will get removed when either:

- a client explicitly calls remove() on that child or one of its ancestors
- a client calls set(null) on that child or one of its ancestors
- that child has all of its children removed
- there is a query in effect which now filters out the child (because it's sort order changed or the max limit was hit)

#### 'child_changed' event

This event will be triggered when the data stored in a child (or any of its descendants) changes. Note that a single child_changed event may represent multiple changes to the child. The DataSnapshot passed to the callback will contain the new child contents. For ordering purposes, the callback is also passed a second argument which is a string containing the key of the previous sibling child by sort order, or null if it is the first child.

#### 'child_moved' event

This event will be triggered when a child's sort order changes such that its position relative to its siblings changes. The DataSnapshot passed to the callback will be for the data of the child that has moved. It is also passed a second argument which is a string containing the key of the previous sibling child by sort order, or null if it is the first child.

| Parameter |         |
| --------- | ------- |
| eventType   | **string** (optional) <br /> One of the following strings: "value", "child_added", "child_changed", "child_removed", or "child_moved." |
| callback   | **function** <br /> A callback that fires when the specified event occurs. The callback will be passed a DataSnapshot. For ordering purposes, "child_added", "child_changed", and "child_moved" will also be passed a string containing the key of the previous child, by sort order, or null if it is the first child. |
| cancelCallbackOrContext   | **Object** <br /> An optional callback that will be notified if your event subscription is ever canceled because your client does not have permission to read this data (or it had permission but has now lost it). This callback will be passed an Error object indicating why the failure occurred. |
| context   | **Object** (optional) <br /> If provided, this object will be used as this when calling your callback(s). |

### once
[method]once(eventType, successCallback, failureCallbackOrContext, context) returns Promise containing any type;[/method]

Listens for exactly one event of the specified event type, and then stops listening.

This is equivalent to calling [ref database.Query#on], and then calling [ref database.Query#off] inside the callback function. See on() for details on the event types.

| Parameter |         |
| --------- | ------- |
| eventType   | **string** (optional) <br /> One of the following strings: "value", "child_added", "child_changed", "child_removed", or "child_moved." |
| successCallback   | **function** <br /> A callback that fires when the specified event occurs. The callback will be passed a DataSnapshot. For ordering purposes, "child_added", "child_changed", and "child_moved" will also be passed a string containing the key of the previous child, by sort order, or null if it is the first child. |
| cancelCallbackOrContext   | **Object** <br /> An optional callback that will be notified if your event subscription is ever canceled because your client does not have permission to read this data (or it had permission but has now lost it). This callback will be passed an Error object indicating why the failure occurred. |
| context   | **Object** (optional) <br /> If provided, this object will be used as this when calling your callback(s). |

### orderByChild
[method]orderByChild(path) returns [ref database.Query];[/method]

Generates a new Query object ordered by the specified child key.

Queries can only order by one key at a time. Calling orderByChild() multiple times on the same query is an error.

Firebase queries allow you to order your data by any child key on the fly. However, if you know in advance what your indexes will be, you can define them via the .indexOn rule in your Security Rules for better performance. See the [.indexOn](https://firebase.google.com/docs/database/security/indexing-data) rule for more information.

| Parameter |         |
| --------- | ------- |
| path   | **string** (optional) |

### orderByKey
[method]orderByKey() returns [ref database.Query];[/method]

Generates a new Query object ordered by key.

Sorts the results of a query by their (ascending) key values.

You can read more about orderByKey() in [Sort data](https://firebase.google.com/docs/database/web/lists-of-data#sort_data).

### orderByPriority
[method]orderByPriority() returns [ref database.Query];[/method]

Generates a new Query object ordered by priority.

Applications need not use priority but can order collections by ordinary properties (see [Sort data](https://firebase.google.com/docs/database/web/lists-of-data#sort_data) for alternatives to priority).

### orderByValue
[method]orderByValue() returns [ref database.Query];[/method]

Generates a new Query object ordered by value.

If the children of a query are all scalar values (string, number, or boolean), you can order the results by their (ascending) values.

You can read more about orderByValue() in [Sort data](https://firebase.google.com/docs/database/web/lists-of-data#sort_data).

### startAt
[method]startAt(value, key) returns [ref database.Query];[/method]

Creates a Query with the specified starting point.

Using `startAt()`, `endAt()`, and `equalTo()` allows you to choose arbitrary starting and ending points for your queries.

The starting point is inclusive, so children with exactly the specified value will be included in the query. The optional key argument can be used to further limit the range of the query. If it is specified, then children that have exactly the specified value must also have a key name greater than or equal to the specified key.

You can read more about `startAt()` in [Filtering data](https://firebase.google.com/docs/database/web/lists-of-data#filtering_data).

| Parameter |         |
| --------- | ------- |
| value   | **string** <br /> The value to start at. The argument type depends on which orderBy*() function was used in this query. Specify a value that matches the orderBy*() type. When used in combination with orderByKey(). |
| key   | **string** <br /> The child key to start at. This argument is only allowed if ordering by child, value, or priority. |

### toJSON
[method]toJSON() returns Object;[/method]

Returns a JSON-serializable representation of this object.

### toString
[method]toString() returns Object;[/method]

Gets the absolute URL for this location.

The toString() method returns a URL that is ready to be put into a browser, curl command, or a firebase.database().refFromURL() call. Since all of those expect the URL to be url-encoded, toString() returns an encoded URL.

Append '.json' to the returned URL when typed into a browser to download JSON-formatted data. If the location is secured (that is, not publicly readable), you will get a permission-denied error.
