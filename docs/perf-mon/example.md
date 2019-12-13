# Performance Monitoring Example

Installing performance monitoring automatically allows Firebase to capture
a number of events and traces with no futher action, such as monitoring app events
(boot time, time in foreground/background etc) and network requests.

If however you'd like to dive deeper into monitoring certain events in your app,
two classes are available, Trace and HttpMetric. Both give access to a number of methods
to better provide Firebase with additional custom attributes and metrics.

## Custom Trace

A custom trace can be used in any situation throughout your apps lifecycle. Take the following hypothetical case:

A user opens a specific view inside your app. Every time the user presses a button
data is fetched from a remote source. We'd like to trace the following metrics and attributes:

- The user ID (note, do not trace any personally identifiable information such as an email address)
- The data endpoint
- How many times the action was carried out
- Whether the response was cached on the server (from the response payload)

To trace this, in our view/component we can create a new trace:

```jsx
...

class TraceView extends React.Component {

    constructor() {
        super();
        this.endpoint = 'https://example.com/data.json';
        this.trace = null;
    }

    async componentDidMount() {
        // Define & start trace
        this.trace = firebase.perf().newTrace('cache_trace');
        await this.trace.start();

        // Set initial attributes
        await this.trace.putAttribute('user_id', firebase.auth().currentUser.uid);
        await this.trace.putAttribute('endpoint', this.endpoint);
        await this.trace.putMetric('requests', 0);
    }

    async componentWillUnmount() {
        await this.trace.stop();
    }

    _onPress = async () => {
        const response = await fetch(this.endpoint);
        const json = await response.json();

        // Increment the requests metric by 1
        await this.trace.incrementMetric('requests', 1);

        // Increment a metric based on whether the payload was cached
        if (json.cached) await this.trace.incrementMetric('requests_cached', 1);
        else await this.trace.incrementMetric('requests_not_cached', 1);
    }

    render() {
        return (
            <Button
                title="Press to get data"
                onPress={this._onPress}
            />
        );
    }

}

```

## Network Metric

An HTTP Metric trace provides Firebase with more specific data of a network request, such as
request/response payload size, HTTP reponse code and content type of the request.

The following example shows how to create a new HTTP Metric by using the standard
React Native [fetch](https://facebook.github.io/react-native/docs/network.html) API:

```jsx
...

class ExampleView extends React.Component {

    constructor() {
        super();
        this.endpoint = 'https://example.com/data.json';
        this.metric = null;
    }

    async componentDidMount() {
        // Define & start trace
        this.metric = firebase.perf().newHttpMetric(this.endpoint, 'GET');
        await this.metric.start();

        // Set initial attributes
        await this.metric.putAttribute('user_id', firebase.auth().currentUser.uid);
        await this.metric.putAttribute('endpoint', this.endpoint);

        const response = await fetch(this.endpoint);
        await this.metric.setHttpResponseCode(response.status);
        await this.metric.setResponseContentType(response.headers.get('Content-Type'));
        await this.metric.setResponsePayloadSize(response.headers.get('Content-Length'));

        const json = await response.json();

        await this.metric.putAttribute('cached', json.cached ? 'true' : 'false');

        await this.metric.stop();
    }

    ...

```
