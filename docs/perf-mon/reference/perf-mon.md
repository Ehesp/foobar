# Performance Monitoring

```
firebase.perf
```

?> **Upcoming Change:** Note that this API is likely to change in v5.1.0 to convert all Trace / HttpMetric methods (except start & stop) to be synchronous JS side methods. The API implemented currently is an initial draft to allow early access.

Firebase Performance Monitoring captures a number of traces automatically, such as all outbound HTTP requests, app boot time and more.

## Methods 

The following methods are accessed via the Performance Monitoring instance `firebase.perf()`.

### setPerformanceCollectionEnabled
[method]setPerformanceCollectionEnabled(enabled) returns void;[/method]

Enables or disables performance monitoring. 

| Parameter |         |
| --------- | ------- |
| enabled   | **boolean** <br />Whether monitoring is enabled or disabled |

### newTrace
[method]newTrace(id) returns [ref perf-mon.Trace];[/method]

Returns a new instance of Trace. The id is the unique name of something you'd like to run performance monitoring against.

| Parameter |         |
| --------- | ------- |
| id   | **string** <br /> The unique name of the trace to monitor |

### newHttpMetric
[method]newHttpMetric(url, method) returns [ref perf-mon.HttpMetric];[/method]

Returns a new instance of HttpMetric.

| Parameter |         |
| --------- | ------- |
| url   | **string** <br /> The full URL of the new request |
| method   | **string** <br /> The HTTP method of the request. One of: GET, PUT, POST, DELETE, HEAD, PATCH, OPTIONS, TRACE, CONNECT |

## Classes

### Trace

[ref perf-mon.Trace]

### HttpMetric

[ref perf-mon.HttpMetric]
