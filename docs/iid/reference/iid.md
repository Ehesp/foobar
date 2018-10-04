# Instance ID

```
firebase.iid
```

## Methods

The following methods are accessed via the Instance ID instance: `firebase.iid()`.

### get
[method]get() returns Promise containing string;[/method]

Get the current Instance ID.

### delete
[method]delete() returns Promise containing void;[/method]

Delete the current Instance ID.

### getToken
[method]getToken(authorizedEntity?: string, scope?: string) returns Promise containing string;[/method]

Get a token that authorizes an Entity to perform an action on behalf of the application identified by Instance ID.

Returns a promise that resolves with the token if successful, otherwise rejects with an error.

| Parameter |         |
| --------- | ------- |
| authorizedEntity | Entity authorized by the token. </br> **Defaults to:** `firebase.iid().app.options.messagingSenderId;` |
| scope | Action authorized for authorizedEntity. </br> **Defaults to:** `*` |

### deleteToken
[method]deleteToken(authorizedEntity?: string, scope?: string) returns Promise containing void;[/method]

Revokes access to a scope (action) for an entity previously authorized by getToken().

Returns a promise that resolves with null if successful, otherwise rejects with an error.

| Parameter |         |
| --------- | ------- |
| authorizedEntity | Entity authorized by the token. </br> **Defaults to:** `firebase.iid().app.options.messagingSenderId;` |
| scope | Action authorized for authorizedEntity. </br> **Defaults to:** `*` |
