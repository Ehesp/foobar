# Trace

?> **Upcoming Change Notification:** This implementations API is likely to change in `v6.0.0` to convert all Trace / HttpMetric methods (except start & stop) to be synchronous JS side methods. The API implemented currently is an initial draft to allow early access.
 
> Once a trace has been started and stopped, you cannot re-start it in the same app lifecycle.

## start
[method]trace.start() returns void;[/method]

Initializes the trace to start tracing performance to relay back to Firebase.

## stop
[method]trace.stop() returns void;[/method]

Stops performance tracing. The completed trace stats are now sent to Firebase.

> Results are not realtime. They can take a number of hours to appear in the Firebase console.

## getAttribute
[method]trace.getAttribute(attribute) returns Promise<string | null>;[/method]

Gets a trace attribute, or null if it does not exist.

| Parameter |         |
| --------- | ------- |
| attribute     | **string** <br /> Attribute name |

## getAttributes
[method]trace.getAttributes() returns Promise<Object>;[/method]

Returns an object of key (attribite) value pairs, or an empty object if no attributes exist.

## putAttribute
[method]trace.putAttribute(attribute, value) returns Promise<null>;[/method]

Gets a trace attribute, or null if it does not exist.

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

## getMetric
[method]trace.getMetric(metricName) returns Promise<number>;[/method]

Gets a trace metric value. Returns zero if metric has not been set.

| Parameter |         |
| --------- | ------- |
| metricName     | **string** <br /> Metric name |

## putMetric
[method]trace.putMetric(metricName, value) returns Promise<number>;[/method]

Gets a trace metric value. Returns zero if metric has not been set.

| Parameter |         |
| --------- | ------- |
| metricName     | **string** <br /> Metric name |
| value     | **number** <br /> Initial metric value |

## incrementMetric
[method]trace.incrementMetric(metricName, incrementBy) returns Promise<null>;[/method]

Increments a metric value by a given amount. If metric has not been set, a new one is created.

| Parameter |         |
| --------- | ------- |
| metricName     | **string** <br /> Metric name |
| incrementBy     | **number** <br /> Number to increment metric by |

