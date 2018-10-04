# HttpMetric

?> **Upcoming Change:** Note that this API is likely to change in v5.1.0 to convert all Trace / HttpMetric methods (except start & stop) to be synchronous JS side methods. The API implemented currently is an initial draft to allow early access.

> Once a trace has been started and stopped, you cannot re-start it in the same app lifecycle.

## start
[method]httpMetric.start() returns Promise<null>;[/method]

Initializes the http metric to start.

## stop
[method]httpMetric.stop() returns Promise<null>;[/method]

Stops performance tracing. The completed trace stats are now sent to Firebase.

> Results are not realtime. They can take a number of hours to appear in the Firebase console.

## getAttribute
[method]httpMetric.getAttribute(attribute) returns Promise<string | null>;[/method]

Returns an attribute value, or null if it does not exist.

| Parameter |         |
| --------- | ------- |
| attribute     | **string**  |

## getAttributes
[method]httpMetric.getAttributes() returns Promise<Object>;[/method]

Returns an object of key (attribite) value pairs, or an empty object if no attributes exist.

## putAttribute
[method]httpMetric.putAttribute(attribute, value) returns Promise<true | false>;[/method]

Creates or updates an attribute by name.

Returns true if attributes was added, false otherwise.

| Parameter |         |
| --------- | ------- |
| attribute     | **string**  |
| value     | **string**  |

## removeAttribute
[method]httpMetric.removeAttribute(attribute) returns Promise<null>;[/method]

Returns an attribute value, or null if it does not exist.

| Parameter |         |
| --------- | ------- |
| attribute     | **string**  |

## setHttpResponseCode
[method]httpMetric.setHttpResponseCode(code) returns Promise<null>;[/method]

| Parameter |         |
| --------- | ------- |
| code     | **number** <br /> HTTP response code, e.g. 200, 404, 500 |

## setRequestPayloadSize
[method]httpMetric.setRequestPayloadSize(bytes) returns Promise<null>;[/method]

| Parameter |         |
| --------- | ------- |
| bytes     | **number** <br /> Request payload size in bytes |

## setResponseContentType
[method]httpMetric.setResponseContentType(type) returns Promise<null>;[/method]

| Parameter |         |
| --------- | ------- |
| type     | **string** <br /> HTTP response content-type, e.g. application/json  |

## setResponsePayloadSize
[method]httpMetric.setResponsePayloadSize(bytes) returns Promise<null>;[/method]

| Parameter |         |
| --------- | ------- |
| bytes     | **number** <br /> Response payload size in bytes |
