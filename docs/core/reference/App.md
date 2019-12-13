# App

## Methods

### extendApp
[method]extendApp(props) returns void;[/method]

Allows adding additional properties onto a firebase app instance.

?> This methods is undocumented on the web SDK.

| Parameter |         |
| --------- | ------- |
| props   | **Object**  |

### delete
[method]delete() returns Promise<void>;[/method]

Renders this app instance unusable and frees the resources of all associated services.

?> Due to native sdk requirments; the default app can not be deleted and will throw an error if a delete is attempted. 

### onReady
[method]onReady() returns Promise containing [App](#methods);[/method]

Resolves a promise once the App instance has been initilized.

## Properties

### name
[method]name returns string;[/method]

### options
[method]options returns Object;[/method]

