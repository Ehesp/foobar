# Functions

```
firebase.functions
```

## Reference Material

 - [Official Firebase Functions Documentation](https://firebase.google.com/docs/functions/callable)
 - [RNFirebase - Functions Test Suite](https://github.com/invertase/react-native-firebase/blob/master/bridge/e2e/functions/functions.e2e.js)
 - [RNFirebase - Test Cloud Function](https://github.com/invertase/react-native-firebase/tree/master/bridge/functions)

## Properties

### app
[method]app return [ref core.App];[/method]

The app associated with this Firestore service instance.

## Methods

The following methods are accessed via the Functions instance `firebase.functions()`.

### constructor
[method]functions(appOrRegion?: [ref core.App] | string, region?: string) returns this;[/method]

| Parameter |         |
| --------- | ------- |
| appOrRegion | **[ref core.App] | string** <br /> An App instance, ID or Firebase region name |
| region | **string** <br /> A Firebase region, defaults to us-central1 |

### httpsCallable
[method]httpsCallable(name: string) returns (data?: any): [HttpsCallablePromise](#Types) => {};[/method]

Gets an `HttpsCallable` instance that refers to the function with the given name.

| Parameter |         |
| --------- | ------- |
| name      | **string** <br /> The name of the https callable function. |


[collapse RNFirebase Client SDK Example]
```js
const httpsCallable = firebase.functions().httpsCallable('myFooBarFn');

httpsCallable({ some: 'args' })
    .then(({ data }) => {
        console.log(data.someResponse); // hello world
    })
    .catch(httpsError => {
        console.log(httpsError.code); // invalid-argument
        console.log(httpsError.message); // Your error message goes here
        console.log(httpsError.details.foo); // bar
    })
```
[/collapse]

[collapse Firebase Cloud Function Example]
```js
const functions = require('firebase-functions');

exports.myFooBarFn = functions.https.onCall(data => {
    console.log(data.some);

    if (!data.some) {
        throw new functions.https.HttpsError(
          'invalid-argument', // code
          'Your error message goes here', // message
          { foo: 'bar' }, // details - optional and can be anything JSON serializable
        );
    }

    return { someResponse: 'hello world' };
});
```
[/collapse]

### useFunctionsEmulator
[method]useFunctionsEmulator(origin: string) returns Promise<null>;[/method]

Changes this instance to point to a Cloud Functions emulator running locally.

| Parameter |         |
| --------- | ------- |
| origin      | **string** <br /> The origin string of the local emulator started via [firebase tools](https://firebase.google.com/docs/functions/local-emulator) |


## Types

### HttpsCallableResult

```ts
type HttpsCallableResult = {
  data: Object,
};
```

### HttpsCallablePromise

[method] type HttpsCallablePromise = Promise<HttpsCallableResult>| Promise<[ref functions.HttpsError]>; [/method]
