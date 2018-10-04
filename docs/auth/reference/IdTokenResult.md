# IdTokenResult

Interface representing an ID token result obtained from [ref auth.User#getIdTokenResult].

It contains the ID token JWT string and other helper properties for getting different data
associated with the token as well as all the decoded payload claims.

?> Note that these claims are not to be trusted as they are parsed client side. Only server side verification can guarantee the integrity of the token claims.

## Properties

### authTime
[method]authTime returns string;[/method]

The authentication time as a ISO 8601 UTC Date string. This is the time the user authenticated (signed in) and not the time the token was refreshed.

### claims
[method]claims returns non-null Object;[/method]

The entire payload claims of the token including reserved claims and custom claims.

### expirationTime
[method]expirationTime returns string;[/method]

The token expiration time formatted as a ISO 8601 UTC Date string.

### issuedAtTime
[method]issuedAtTime returns string;[/method]

The token issued at time formatted as a ISO 8601 UTC Date string.

### signInProvider
[method]signInProvider returns nullable string;[/method]

The sign-in provider which the token was obtained with, e.g. anonymous, custom, phone, password, etc.
 
> Note, this does not map to provider IDs.

### token
[method]token returns string;[/method]

The Firebase JWT string.

----

**Source**: https://firebase.google.com/docs/reference/js/firebase.auth.IdTokenResult
