# User

A user account.

## Methods

### delete
[method]delete() returns Promise containing void;[/method]

Deletes and signs out the user.

Important: this is a security sensitive operation that requires the user to have recently signed in. If this requirement isn't met, ask the user to authenticate again and then call [ref auth.User#reauthenticateWithCredential].

#### Error Codes

| Code | Message |
| --------- | ------- |
| auth/requires-recent-login  | Thrown if the user's last sign-in time does not meet the security threshold. Use [ref auth.User#reauthenticateWithCredential] to resolve. This does not apply if the user is anonymous. |

### getIdToken
[method]getIdToken(forceRefresh) returns Promise containing string;[/method]

Returns a JWT token used to identify the user to a Firebase service.

Returns the current token if it has not expired, otherwise this will refresh the token and return a new one.

| Parameter |         |
| --------- | ------- |
| forceRefresh   | **boolean** (optional) <br /> Force refresh regardless of token expiration. |

### getIdTokenResult
[method]getIdTokenResult(forceRefresh) returns Promise containing [ref auth.IdTokenResult];[/method]

Returns a [ref auth.IdTokenResult] object which contains the ID token JWT string and other properties for getting
data associated with the token and all the decoded payload claims.                        

?> While client side parsing of ID tokens is convenient for UI changes depending on payload content, it is not sufficient or secure. Server side ID token verification is always required when enforcing access to restricted resources.

Returns the current [ref auth.IdTokenResult] object if it has not expired, otherwise this will refresh the token and return a new one.

| Parameter |         |
| --------- | ------- |
| forceRefresh   | **boolean** (optional) <br /> Force refresh regardless of token expiration. |

#### Guides

 - [Firebase - Control Access with Custom Claims and Security Rules](https://firebase.google.com/docs/auth/admin/custom-claims)
 - [YouTube - Firecasts - Controlling Data Access Using Firebase Auth Custom Claims](https://youtu.be/3hj_r_N0qMs)


### linkAndRetrieveDataWithCredential
[method]linkAndRetrieveDataWithCredential(credential) returns Promise containing [ref auth.UserCredential];[/method]

Links the user account with the given credentials, and returns any available additional user information, such as user name.

?> This method is deprecated.

| Parameter |         |
| --------- | ------- |
| credential   | **[ref auth.AuthCredential]** <br /> The auth credential. <br /> Value must not be null. |

#### Error Codes

| Code | Message |
| --------- | ------- |
| auth/provider-already-linked  | Thrown if the provider has already been linked to the user. This error is thrown even if this is not the same provider's account that is currently linked to the user. |
| auth/invalid-credential  | Thrown if the provider's credential is not valid. This can happen if it has already expired when calling link, or if it used invalid token(s). See the Firebase documentation for your provider, and make sure you pass in the correct parameters to the credential method. |
| auth/credential-already-in-use  | Thrown if the account corresponding to the credential already exists among your users, or is already linked to a Firebase User. For example, this error could be thrown if you are upgrading an anonymous user to a Google user by linking a Google credential to it and the Google credential used is already associated with an existing Firebase Google user. The fields error.email, error.phoneNumber, and error.credential ([ref auth.AuthCredential]) may be provided, depending on the type of credential. You can recover from this error by signing in with error.credential directly via [ref auth#signInWithCredential]. |
| auth/email-already-in-use  | Thrown if the email corresponding to the credential already exists among your users. When thrown while linking a credential to an existing user, an error.email and error.credential [ref auth.AuthCredential] fields are also provided. You have to link the credential to the existing user with that email if you wish to continue signing in with that credential. To do so, call [ref auth.Auth#fetchProvidersForEmail], sign in to error.email via one of the providers returned and then [ref auth.User#linkWithCredential] the original credential to that newly signed in user |
| auth/operation-not-allowed  | Thrown if you have not enabled the provider in the Firebase Console. Go to the Firebase Console for your project, in the Auth section and the **Sign in Method** tab and configure the provider. |
| auth/invalid-email  | Thrown if the email used in a [ref auth.EmailAuthProvider#credential] is invalid. |
| auth/wrong-password  | Thrown if the password used in a [ref auth.EmailAuthProvider#credential] is not correct or when the user associated with the email does not have a password. |
| auth/invalid-verification-code  | Thrown if the credential is a [ref auth.PhoneAuthProvider#credential] and the verification code of the credential is not valid. |
| auth/invalid-verification-id  | Thrown if the credential is a [ref auth.PhoneAuthProvider#credential] and the verification ID of the credential is not valid. |

### linkWithCredential
[method]linkWithCredential(credential) returns Promise containing [ref auth.UserCredential];[/method]

Links the user account with the given credentials, and returns any available additional user information, such as user name.

| Parameter |         |
| --------- | ------- |
| credential   | **[ref auth.AuthCredential]** <br /> The auth credential. <br /> Value must not be null. |

#### Error Codes

| Code | Message |
| --------- | ------- |
| auth/provider-already-linked  | Thrown if the provider has already been linked to the user. This error is thrown even if this is not the same provider's account that is currently linked to the user. |
| auth/invalid-credential  | Thrown if the provider's credential is not valid. This can happen if it has already expired when calling link, or if it used invalid token(s). See the Firebase documentation for your provider, and make sure you pass in the correct parameters to the credential method. |
| auth/credential-already-in-use  | Thrown if the account corresponding to the credential already exists among your users, or is already linked to a Firebase User. For example, this error could be thrown if you are upgrading an anonymous user to a Google user by linking a Google credential to it and the Google credential used is already associated with an existing Firebase Google user. The fields error.email, error.phoneNumber, and error.credential ([ref auth.AuthCredential]) may be provided, depending on the type of credential. You can recover from this error by signing in with error.credential directly via [ref auth#signInWithCredential]. |
| auth/email-already-in-use  | Thrown if the email corresponding to the credential already exists among your users. When thrown while linking a credential to an existing user, an error.email and error.credential [ref auth.AuthCredential] fields are also provided. You have to link the credential to the existing user with that email if you wish to continue signing in with that credential. To do so, call [ref auth.Auth#fetchProvidersForEmail], sign in to error.email via one of the providers returned and then [ref auth.User#linkWithCredential] the original credential to that newly signed in user |
| auth/operation-not-allowed  | Thrown if you have not enabled the provider in the Firebase Console. Go to the Firebase Console for your project, in the Auth section and the **Sign in Method** tab and configure the provider. |
| auth/invalid-email  | Thrown if the email used in a [ref auth.EmailAuthProvider#credential] is invalid. |
| auth/wrong-password  | Thrown if the password used in a [ref auth.EmailAuthProvider#credential] is not correct or when the user associated with the email does not have a password. |
| auth/invalid-verification-code  | Thrown if the credential is a [ref auth.PhoneAuthProvider#credential] and the verification code of the credential is not valid. |
| auth/invalid-verification-id  | Thrown if the credential is a [ref auth.PhoneAuthProvider#credential] and the verification ID of the credential is not valid. |

### reauthenticateAndRetrieveDataWithCredential
[method]reauthenticateAndRetrieveDataWithCredential(credential) returns Promise containing [ref auth.UserCredential];[/method]

Re-authenticates a user using a fresh credential. Use before operations such as [ref auth.User#updatePassword] that require tokens from recent sign-in attempts.

?> This method is deprecated.

| Parameter |         |
| --------- | ------- |
| credential   | **[ref auth.AuthCredential]** <br /> The auth credential. <br /> Value must not be null. |

#### Error Codes

| Code | Message |
| --------- | ------- |
| auth/user-mismatch  | Thrown if the credential given does not correspond to the user. |
| auth/user-not-found  | Thrown if the credential given does not correspond to any existing user. |
| auth/invalid-credential  | Thrown if the provider's credential is not valid. This can happen if it has already expired when calling link, or if it used invalid token(s). See the Firebase documentation for your provider, and make sure you pass in the correct parameters to the credential method. |
| auth/invalid-email  | Thrown if the email used in a [ref auth.EmailAuthProvider#credential] is invalid. |
| auth/wrong-password  | Thrown if the password used in a [ref auth.EmailAuthProvider#credential] is not correct or when the user associated with the email does not have a password. |
| auth/invalid-verification-code  | Thrown if the credential is a [ref auth.PhoneAuthProvider#credential] and the verification code of the credential is not valid. |
| auth/invalid-verification-id  | Thrown if the credential is a [ref auth.PhoneAuthProvider#credential] and the verification ID of the credential is not valid. |

### reauthenticateWithCredential
[method]reauthenticateWithCredential(credential) returns Promise containing [ref auth.UserCredential];[/method]

Re-authenticates a user using a fresh credential. Use before operations such as [ref auth.User#updatePassword] that require tokens from recent sign-in attempts.

| Parameter |         |
| --------- | ------- |
| credential   | **[ref auth.AuthCredential]** <br /> The auth credential. <br /> Value must not be null. |

#### Error Codes

| Code | Message |
| --------- | ------- |
| auth/user-mismatch  | Thrown if the credential given does not correspond to the user. |
| auth/user-not-found  | Thrown if the credential given does not correspond to any existing user. |
| auth/invalid-credential  | Thrown if the provider's credential is not valid. This can happen if it has already expired when calling link, or if it used invalid token(s). See the Firebase documentation for your provider, and make sure you pass in the correct parameters to the credential method. |
| auth/invalid-email  | Thrown if the email used in a [ref auth.EmailAuthProvider#credential] is invalid. |
| auth/wrong-password  | Thrown if the password used in a [ref auth.EmailAuthProvider#credential] is not correct or when the user associated with the email does not have a password. |
| auth/invalid-verification-code  | Thrown if the credential is a [ref auth.PhoneAuthProvider#credential] and the verification code of the credential is not valid. |
| auth/invalid-verification-id  | Thrown if the credential is a [ref auth.PhoneAuthProvider#credential] and the verification ID of the credential is not valid. |

### reload
[method]reload() returns Promise containing void;[/method]

Refreshes the current user, if signed in.

### sendEmailVerification
[method]sendEmailVerification(actionCodeSettings) returns Promise containing void;[/method]

Send verification email to current user.

| Parameter |         |
| --------- | ------- |
| actionCodeSettings | **[ref auth.ActionCodeSettings]** (optional)

### toJSON
[method]toJSON() returns Object;[/method]

Returns a JSON-serializable representation of this object.

### unlink
[method]unlink(providerId) returns Promise containing [ref auth.User];[/method]

Unlinks a provider from a user account.

| Parameter |         |
| --------- | ------- |
| providerId   | **string** |

### updateEmail
[method]updateEmail(newEmail) returns Promise containing void;[/method]

Updates the user's email address.

An email will be sent to the original email address (if it was set) that allows to revoke the email address change, in order to protect them from account hijacking.

Important: this is a security sensitive operation that requires the user to have recently signed in. If this requirement isn't met, ask the user to authenticate again and then call [ref auth.User#reauthenticateWithCredential].

| Parameter |         |
| --------- | ------- |
| newEmail   | **string** |

#### Error Codes

| Code | Message |
| --------- | ------- |
| auth/invalid-email  | Thrown if the email used is invalid. |
| auth/email-already-in-use  | Thrown if the email is already used by another user. |
| auth/requires-recent-login  | Thrown if the user's last sign-in time does not meet the security threshold. Use [ref auth.User#reauthenticateWithCredential] to resolve. This does not apply if the user is anonymous. |

### updatePassword
[method]updatePassword(newPassword) returns Promise containing void;[/method]

Updates the user's password.

Important: this is a security sensitive operation that requires the user to have recently signed in. If this requirement isn't met, ask the user to authenticate again and then call [ref auth.User#reauthenticateWithCredential].

| Parameter |         |
| --------- | ------- |
| newPassword   | **string** |

#### Error Codes

| Code | Message |
| --------- | ------- |
| auth/weak-password  | Thrown if the password is not strong enough. |
| auth/requires-recent-login  | Thrown if the user's last sign-in time does not meet the security threshold. Use [ref auth.User#reauthenticateWithCredential] to resolve. This does not apply if the user is anonymous. |


### updatePhoneNumber
[method]updatePhoneNumber(credential: [ref auth.AuthCredential]) returns Promise containing void;[/method]

Update the current user's phone number with a phone AuthCredential - call [ref auth.Auth#verifyPhoneNumber] with the new phone number and pass the outputted credential to this method.

Important: this is a security sensitive operation that requires the user to have recently signed in. If this requirement isn't met, ask the user to authenticate again and then call [ref auth.User#reauthenticateWithCredential].

| Parameter |         |
| --------- | ------- |
| credential   | **[ref auth.AuthCredential]** |

#### Error Codes

| Code | Message |
| --------- | ------- |
| auth/requires-recent-login  | Thrown if the user's last sign-in time does not meet the security threshold. Use [ref auth.User#reauthenticateWithCredential] to resolve. This does not apply if the user is anonymous. |
| auth/invalid-verification-code  | Thrown if the verification code of the credential is not valid. |
| auth/invalid-verification-id  | Thrown if the verification ID of the credential is not valid. |


### updateProfile
[method]updateProfile(profile) returns Promise containing void;[/method]

Updates a user's profile data.

| Parameter |         |
| --------- | ------- |
| profile   | **Object** <br /> `{displayName: nullable string, photoUrl: nullable string }` <br /> The profile's displayName and photoURL to update. <br /> Value must not be null. |

## Properties

### displayName
[method]displayName returns string or null;[/method]

The user's display name (if available).

### email
[method]email returns string or null;[/method]

The user's email address (if available).

### emailVerified
[method]emailVerified returns boolean;[/method]

Returns `true` if the user's email address has been verified.

### isAnonymous
[method]isAnonymous returns boolean;[/method]

Returns `true` if the user is anonymous.

### metadata
[method]metadata returns [ref auth.UserMetadata];[/method]

Additional metadata about the user.

### phoneNumber
[method]phoneNumber returns string or null;[/method]

The phone number normalized based on the E.164 standard (e.g. +16505550101) for the current user. This is null if the user has no phone credential linked to the account.

### photoURL
[method]photoURL returns string or null;[/method]

The URL of the user's profile picture (if available).

Caveat: The Facebook profile picture URL provided by `firebase.auth().currentUser.photoUrl` has an expiration date: after a few days you will get an `URL signature expired` error. A workaround is either to store the image in your database or to use `firebase.auth().currentUser.providerData[0].photoURL + '?height=' + myCustomHeight`.

### providerData
[method]providerData returns Array of [ref auth.UserInfo];[/method]

Additional provider-specific information about the user.

### providerId
[method]providerId returns string;[/method]

The authentication provider ID for the current user. For example, 'facebook.com', or 'google.com'.

### uid
[method]uid returns string;[/method]

The user's unique ID.

## Unsupported Methods

The following methods are not supported in RNFirebase as they cannot work in the React Native environment or have a different implementation.

### linkWithPhoneNumber

### linkWithPopup

### linkWithRedirect

### reauthenticateWithPhoneNumber

### reauthenticateWithPopup

### reauthenticateWithRedirect

## Unsupported properties

The following properties are not supported in RNFirebase as they cannot work in the React Native environment or have a different implementation.

### refreshToken
