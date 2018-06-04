# Authentication

```
firebase.auth
```

## Methods 

The following methods are accessed via the Auth instance `firebase.auth()`.

### onAuthStateChanged
[method]onAuthStateChanged(listener) returns function;[/method]

Adds an observer for changes to the user's sign-in state.

Returns an unsubscriber function.

| Parameter |         |
| --------- | ------- |
| listener  | **function([ref auth.User] or null)** |

### onUserChanged
[method]onUserChanged(listener) returns function;[/method]

> This is an experimental feature and is only part of React Native Firebase.

Adds a listener to observe changes to the [ref auth.User] object. This is a superset of everything from [ref auth.auth#onAuthStateChanged], [ref auth.auth#onIdTokenChanged] and user changes. The goal of this method is to provide easier listening to **all** user changes, such as when credentials are linked and unlinked, without manually having to call `.reload()`.

Returns an unsubscriber function.

| Parameter |         |
| --------- | ------- |
| listener  | **function([ref auth.User] or null)** |

[collapse Example]
```jsx
import React, { Component } from 'react';
import { View, Text } from 'react-native';
import firebase from 'react-native-firebase';

export default class MyComponent extends Component {

  componentDidMount() {
    this.unsubscribe = firebase.auth().onUserChanged(this.onUserChanged);
  }

  componentWillUnmount() {
    if (this.unsubscribe) this.unsubscribe();
  }

  onUserChanged = (currentUser) => {
    if (currentUser) {
      console.log(currentUser.toJSON())
    }
  }

  render () {
    return (
      <View>
        <Text>Hello World</Text>
      </View>
    );
  }
}
```
[/collapse]


### onIdTokenChanged
[method]onIdTokenChanged(listener) returns function;[/method]

Adds an observer for changes to the signed-in user's ID token, which includes sign-in, sign-out, and token refresh events.

Returns an unsubscriber function.

| Parameter |         |
| --------- | ------- |
| listener  | **function** |

### signOut
[method]signOut() returns Promise containing void;[/method]

Signs out the current user.

### signInAnonymously
[method]signInAnonymously() returns Promise containing [ref auth.User];[/method]

Asynchronously signs in as an anonymous user.

This method will be deprecated and will be updated to resolve with a `firebase.auth.UserCredential` as is returned in [ref auth.auth#signInAnonymouslyAndRetrieveData].

If there is already an anonymous user signed in, that user will be returned; otherwise, a new anonymous user identity will be created and returned.

#### Error Codes

| Code | Message |
| --------- | ------- |
| auth/operation-not-allowed   | Thrown if anonymous accounts are not enabled. Enable anonymous accounts in the Firebase Console, under the Auth tab.  |

### signInAnonymouslyAndRetrieveData
[method]signInAnonymously() returns Promise containing [ref auth.UserCredential];[/method]

Signs in a user anonymously and returns any additional user info data or credentials.

This method will be renamed to `signInAnonymously` replacing the existing method with the same name in the next major version change.

If there is already an anonymous user signed in, that user with additional date will be returned; otherwise, a new anonymous user identity will be created and returned.

#### Error Codes

| Code | Message |
| --------- | ------- |
| auth/operation-not-allowed   | Thrown if anonymous accounts are not enabled. Enable anonymous accounts in the Firebase Console, under the Auth tab.  |

### createUserAndRetrieveDataWithEmailAndPassword
[method]createUserAndRetrieveDataWithEmailAndPassword(email, password) returns Promise containing [ref auth.UserCredential];[/method]

Creates a new user account associated with the specified email address and password and returns any additional user info data or credentials.

This method will be renamed to `createUserWithEmailAndPassword` replacing the existing method with the same name in the next major version change.

On successful creation of the user account, this user will also be signed in to your application.

User account creation can fail if the account already exists or the password is invalid.

Note: The email address acts as a unique identifier for the user and enables an email-based password reset. This function will create a new user account and set the initial user password.

Parameter |         |
| --------- | ------- |
| email     | **string**  |
| password     | **string** |

#### Error Codes

| Code | Message |
| --------- | ------- |
| auth/invalid-email  | Thrown if the email address is not valid. |
| auth/user-disabled  | Thrown if the user corresponding to the given email has been disabled. |
| auth/user-not-found | Thrown if there is no user corresponding to the given email. |
| auth/wrong-password | Thrown if the password is invalid for the given email, or the account corresponding to the email does not have a password set. |

### createUserWithEmailAndPassword
[method]createUserWithEmailAndPassword(email, password) returns Promise containing [ref auth.User];[/method]

Creates a new user account associated with the specified email address and password.

This method will be deprecated and will be updated to resolve with a `firebase.auth.UserCredential` as is returned in [ref auth.auth#createUserAndRetrieveDataWithEmailAndPassword].

On successful creation of the user account, this user will also be signed in to your application.

User account creation can fail if the account already exists or the password is invalid.

Note: The email address acts as a unique identifier for the user and enables an email-based password reset. This function will create a new user account and set the initial user password.

| Parameter |         |
| --------- | ------- |
| email     | **string**  |
| password     | **string** |

#### Error Codes

| Code | Message |
| --------- | ------- |
| auth/invalid-email  | Thrown if the email address is not valid. |
| auth/user-disabled  | Thrown if the user corresponding to the given email has been disabled. |
| auth/user-not-found | Thrown if there is no user corresponding to the given email. |
| auth/wrong-password | Thrown if the password is invalid for the given email, or the account corresponding to the email does not have a password set. |

### signInAndRetrieveDataWithCredential
[method]signInAndRetrieveDataWithCredential(credential) returns Promise containing [ref auth.UserCredential];[/method]

Asynchronously signs in with the given credentials, and returns any available additional user information, such as user name.

This method will be renamed to `signInWithCredential` replacing the existing method with the same name in the next major version change.

| Parameter |         |
| --------- | ------- |
| credential     | **Credential** <br /> A credential returned from a provider. |

#### Error Codes

| Code | Message |
| --------- | ------- |
| auth/account-exists-with-different-credential  | Thrown if there already exists an account with the email address asserted by the credential. Resolve this by calling [ref auth#fetchSignInMethodsForEmail] and then asking the user to sign in using one of the returned providers. Once the user is signed in, the original credential can be linked to the user with [ref auth.User#linkWithCredential]. |
| auth/invalid-credential  | Thrown if the credential is malformed or has expired. |
| auth/operation-not-allowed  | Thrown if the type of account corresponding to the credential is not enabled. Enable the account type in the Firebase Console, under the Auth tab. |
| auth/user-disabled  | Thrown if the user corresponding to the given credential has been disabled. |
| auth/user-not-found  | Thrown if signing in with a credential from [ref auth.EmailAuthProvider#credential] and there is no user corresponding to the given email. |
| auth/wrong-password  | Thrown if signing in with a credential from [ref auth.EmailAuthProvider#credential] and the password is invalid for the given email, or if the account corresponding to the email does not have a password set. |
| auth/invalid-verification-code  | Thrown if the credential is a [ref auth.PhoneAuthProvider#credential] and the verification code of the credential is not valid. |
| auth/invalid-verification-id  | Thrown if the credential is a [ref auth.PhoneAuthProvider#credential] and the verification ID of the credential is not valid. |

### signInAndRetrieveDataWithCustomToken
[method]signInAndRetrieveDataWithCustomToken(customToken) returns Promise containing [ref auth.UserCredential];[/method]

Signs in a user asynchronously using a custom token and returns any additional user info data or credentials.

This method will be renamed to `signInWithCustomToken` replacing the existing method with the same name in the next major version change.

Custom tokens are used to integrate Firebase Auth with existing auth systems, and must be generated by the auth backend.

Fails with an error if the token is invalid, expired, or not accepted by the Firebase Auth service.

| Parameter |         |
| --------- | ------- |
| customToken     | **string**  |

#### Error Codes

| Code | Message |
| --------- | ------- |
| auth/custom-token-mismatch  | Thrown if the custom token is for a different Firebase App. |
| auth/invalid-custom-token  | Thrown if the custom token format is incorrect. |

### signInAndRetrieveDataWithEmailAndPassword
[method]signInAndRetrieveDataWithEmailAndPassword(email, password) returns Promise containing [ref auth.UserCredential];[/method]

Asynchronously signs in using an email and password and returns any additional user info data or credentials.

This method will be renamed to `signInWithEmailAndPassword` replacing the existing method with the same name in the next major version change.

Fails with an error if the email address and password do not match.

Note: The user's password is NOT the password used to access the user's email account. The email address serves as a unique identifier for the user, and the password is used to access the user's account in your Firebase project.

See also: [ref auth.Auth#createUserAndRetrieveDataWithEmailAndPassword].

| Parameter |         |
| --------- | ------- |
| email     | **string**  |
| password     | **string** |

#### Error Codes

| Code | Message |
| --------- | ------- |
| auth/invalid-email  | Thrown if the email address is not valid. |
| auth/user-disabled  | Thrown if the user corresponding to the given email has been disabled. |
| auth/user-not-found | Thrown if there is no user corresponding to the given email. |
| auth/wrong-password | Thrown if the password is invalid for the given email, or the account corresponding to the email does not have a password set. |

### signInWithEmailAndPassword
[method]signInWithEmailAndPassword(email, password) returns Promise containing [ref auth.User];[/method]

Asynchronously signs in using an email and password.

This method will be deprecated and will be updated to resolve with a `firebase.auth.UserCredential` as is returned in [ref auth.Auth#signInAndRetrieveDataWithEmailAndPassword].

Fails with an error if the email address and password do not match.

**Note:** The user's password is NOT the password used to access the user's email account. The email address serves as a unique identifier for the user, and the password is used to access the user's account in your Firebase project.

| Parameter |         |
| --------- | ------- |
| email     | **string**  |
| password     | **string** |

#### Error Codes

| Code | Message |
| --------- | ------- |
| auth/invalid-email  | Thrown if the email address is not valid. |
| auth/user-disabled  | Thrown if the user corresponding to the given email has been disabled. |
| auth/user-not-found | Thrown if there is no user corresponding to the given email. |
| auth/wrong-password | Thrown if the password is invalid for the given email, or the account corresponding to the email does not have a password set. |

### signInWithCustomToken
[method]signInWithCustomToken(customToken) returns Promise containing [ref auth.User];[/method]

Asynchronously signs in using a custom token.

This method will be deprecated and will be updated to resolve with a `firebase.auth.UserCredential` as is returned in [ref auth.Auth#signInAndRetrieveDataWithCustomToken].

Custom tokens are used to integrate Firebase Auth with existing auth systems, and must be generated by the auth backend.

Fails with an error if the token is invalid, expired, or not accepted by the Firebase Auth service.

| Parameter |         |
| --------- | ------- |
| customToken     | **string**  |

#### Error Codes

| Code | Message |
| --------- | ------- |
| auth/custom-token-mismatch  | Thrown if the custom token is for a different Firebase App. |
| auth/invalid-custom-token  | Thrown if the custom token format is incorrect. |

### signInWithCredential
[method]signInWithCredential(credential) returns Promise containing [ref auth.User];[/method]

Asynchronously signs in with the given credentials.

This method will be deprecated and will be updated to resolve with a `firebase.auth.UserCredential` as is returned in [ref auth.Auth#signInAndRetrieveDataWithCredential].

| Parameter |         |
| --------- | ------- |
| credential     | **Credential** <br /> A credential returned from a provider. |

#### Error Codes

| Code | Message |
| --------- | ------- |
| auth/account-exists-with-different-credential  | Thrown if there already exists an account with the email address asserted by the credential. Resolve this by calling [ref auth#fetchSignInMethodsForEmail] and then asking the user to sign in using one of the returned providers. Once the user is signed in, the original credential can be linked to the user with [ref auth.User#linkWithCredential]. |
| auth/invalid-credential  | Thrown if the credential is malformed or has expired. |
| auth/operation-not-allowed  | Thrown if the type of account corresponding to the credential is not enabled. Enable the account type in the Firebase Console, under the Auth tab. |
| auth/user-disabled  | Thrown if the user corresponding to the given credential has been disabled. |
| auth/user-not-found  | Thrown if signing in with a credential from [ref auth.EmailAuthProvider#credential] and there is no user corresponding to the given email. |
| auth/wrong-password  | Thrown if signing in with a credential from [ref auth.EmailAuthProvider#credential] and the password is invalid for the given email, or if the account corresponding to the email does not have a password set. |
| auth/invalid-verification-code  | Thrown if the credential is a [ref auth.PhoneAuthProvider#credential] and the verification code of the credential is not valid. |
| auth/invalid-verification-id  | Thrown if the credential is a [ref auth.PhoneAuthProvider#credential] and the verification ID of the credential is not valid. |

### signInWithPhoneNumber
[method]signInWithPhoneNumber(phoneNumber) returns Promise containing [ref auth.ConfirmationResult];[/method]

Asynchronously signs in using a phone number.

Returns a [ref auth.ConfirmationResult]. Use [ref auth.ConfirmationResult#confirm] with the verification code to confirm the phone number. In case of Android auto verification, use [ref auth#onAuthStateChanged] to listen incase the SMS is not shown to the user. See [this guide](version /auth/phone-auth#signInWithPhoneNumber) for more information.

| Parameter |         |
| --------- | ------- |
| phoneNumber | **string** <br /> Phone number containing country code (e.g. +44) |

#### Error Codes

TODO

### verifyPhoneNumber
[method]verifyPhoneNumber(phoneNumber) returns TODO;[/method]

TODO

| Parameter |         |
| --------- | ------- |
| credential     | **string** <br /> Phone number containing country code |

#### Error Codes

| Code | Message |
| --------- | ------- |
| auth/invalid-email  | Thrown if the email address is not valid. |
| auth/user-not-found | Thrown if there is no user corresponding to the email address. |

### sendPasswordResetEmail
[method]sendPasswordResetEmail(email, actionCodeSettings) returns Promise containing void;[/method]

Sends a password reset email to the given email address.

To complete the password reset, call [ref auth#confirmPasswordReset] with the code supplied in the email sent to the user, along with the new password specified by the user.

| Parameter |         |
| --------- | ------- |
| email     | **string** |
| actionCodeSettings | **[ref auth.ActionCodeSettings]** (optional)

#### Error Codes

| Code | Message |
| --------- | ------- |
| auth/invalid-email  | Thrown if the email address is not valid. |
| auth/user-not-found | Thrown if there is no user corresponding to the email address. |

### confirmPasswordReset
[method]confirmPasswordReset(code, newPassword) returns Promise containing void;[/method]

Completes the password reset process, given a confirmation code and new password.

| Parameter |         |
| --------- | ------- |
| code     | **string** |
| newPassword  | **string** |

#### Error Codes

| Code | Message |
| --------- | ------- |
| auth/expired-oob  | Thrown if the password reset code has expired. |
| auth/invalid-oob | Thrown if the password reset code is invalid. This can happen if the code is malformed or has already been used. |
| auth/user-disabled  | Thrown if the user corresponding to the given password reset code has been disabled. |
| auth/user-not-found  | Thrown if there is no user corresponding to the password reset code. This may have happened if the user was deleted between when the code was issued and when this method was called. |
| auth/weak-password  | Thrown if the new password is not strong enough. |

### applyActionCode
[method]applyActionCode(code) returns Promise containing void;[/method]

Applies a verification code sent to the user by email or other out-of-band mechanism.

| Parameter |         |
| --------- | ------- |
| code     | **string** <br /> A verification code sent to the user. |

#### Error Codes

| Code | Message |
| --------- | ------- |
| auth/expired-action-code  | Thrown if the password reset code has expired. |
| auth/invalid-action-code | Thrown if the password reset code is invalid. This can happen if the code is malformed or has already been used. |
| auth/user-disabled  | Thrown if the user corresponding to the given password reset code has been disabled. |
| auth/user-not-found  | Thrown if there is no user corresponding to the password reset code. This may have happened if the user was deleted between when the code was issued and when this method was called. |

### checkActionCode
[method]checkActionCode(code) returns Promise containing [ref auth.ActionCodeInfo];[/method]

Checks a verification code sent to the user by email or other out-of-band mechanism.

Returns metadata about the code.

| Parameter |         |
| --------- | ------- |
| code     | **string** <br /> A verification code sent to the user. |

#### Error Codes

| Code | Message |
| --------- | ------- |
| auth/expired-oob  | Thrown if the password reset code has expired. |
| auth/invalid-oob | Thrown if the password reset code is invalid. This can happen if the code is malformed or has already been used. |
| auth/user-disabled  | Thrown if the user corresponding to the given password reset code has been disabled. |
| auth/user-not-found  | Thrown if there is no user corresponding to the password reset code. This may have happened if the user was deleted between when the code was issued and when this method was called. |

### fetchSignInMethodsForEmail
[method]fetchSignInMethodsForEmail(email) returns Promise containing Array of string;[/method]

Returns a list of authentication methods that can be used to sign in a given user (identified by its main email address).

Useful for an "identifier-first" sign-in flow.

| Parameter |         |
| --------- | ------- |
| email     | **string** |


### sendSignInLinkToEmail
[method]sendSignInLinkToEmail(email, actionCodeSettings) returns Promise containing void;[/method]

Sends a sign-in email link to the user with the specified email.

To complete sign in with the email link, call [ref auth.auth#signInWithEmailLink] with the email address and the email link supplied in the email sent to the user.

| Parameter |         |
| --------- | ------- |
| email     | **string** |
| actionCodeSettings | **[ref auth.ActionCodeSettings]**

[collapse Example]
```js
const email = 'foo@example.com';
const actionCodeSettings = {
    url: 'http://example.com/something?foobar=1234',
    handleCodeInApp: true, // must always be true for sendSignInLinkToEmail
    iOS: {
      bundleId: 'com.testing',
    },
    android: {
      packageName: 'com.testing',
      installApp: true,
      minimumVersion: '12',
    },
};

firebase.auth().sendSignInLinkToEmail(email, actionCodeSettings);
    // .then()
    // .catch(error) -> error.code
```
[/collapse]

#### Error Codes

| Code | Message |
| --------- | ------- |
| auth/argument-error  | Thrown if handleCodeInApp is false. |
| auth/invalid-email  | Thrown if the email address is not valid. |
| auth/operation-not-allowed  | Thrown if 'Email/Password > Email link (passwordless sign-in)' authentication mode is not enabled on the Firebase console |
| auth/missing-android-pkg-name  | An Android package name must be provided if the Android app is required to be installed. |
| auth/missing-continue-uri | A continue URL must be provided in the request. |
| auth/missing-ios-bundle-id | An iOS Bundle ID must be provided if an App Store ID is provided. |
| auth/invalid-continue-uri | The continue URL provided in the request is invalid. |
| auth/unauthorized-continue-uri | The domain of the continue URL is not whitelisted. Whitelist the domain in the Firebase console. |

### signInWithEmailLink
[method]signInWithEmailLink(email, emailLink) returns Promise containing [ref auth.UserCredential];[/method]

Asynchronously signs in using an email and sign-in email link.

Fails with an error if the email address is invalid or the email link has expired.

> Use [ref auth.auth#isSignInWithEmailLink] to check if an inbound dynamic link is a sign-in link. None sign-in links will fail.

| Parameter |         |
| --------- | ------- |
| email     | **string** |
| emailLink | **string**

[collapse Example]
```js
const email = 'foo@example.com';

// link from firebase.links().getInitialLink() or it's link listener
const link = '';

firebase.auth().signInWithEmailLink(email, link);
    // .then()
    // .catch(error) -> error.code
```
[/collapse]

### isSignInWithEmailLink
[method]isSignInWithEmailLink(emailLink) returns boolean;[/method]

Checks if an incoming link is a sign-in with email link. Use on incoming links via [ref links.links#getInitialLink] or [ref links.links#onLink]

| Parameter |         |
| --------- | ------- |
| emailLink | **string**

[collapse Example]
```js
firebase.links()
    .getInitialLink()
    .then((url) => {
        if (firebase.auth().isSignInWithEmailLink(url)) {
            // call signInWithEmailLink or make a credential from the url using
            // firebase.auth.EmailAuthProvider.credentialWithLink(email, url)
            // and use any of the credential based auth flows with it, e.g. linkWithCredential
        } else {
           // not a sign-in link - must be some other type of link
        }
    });
```
[/collapse]

### verifyPasswordResetCode

[method]verifyPasswordResetCode(code) returns Promise containing string;[/method]

Checks a password reset code sent to the user by email or other out-of-band mechanism.

Returns the user's email address if valid.

| Parameter |         |
| --------- | ------- |
| code      | **string** |

#### Error Codes

| Code | Message |
| --------- | ------- |
| auth/expired-oob  | Thrown if the password reset code has expired. |
| auth/invalid-oob | Thrown if the password reset code is invalid. This can happen if the code is malformed or has already been used. |
| auth/user-disabled  | Thrown if the user corresponding to the given password reset code has been disabled. |
| auth/user-not-found  | Thrown if there is no user corresponding to the password reset code. This may have happened if the user was deleted between when the code was issued and when this method was called. |

## Properties

The following properties are accessed via the Auth instance `firebase.auth()`.

### app
[method]app return [ref core.App];[/method]

The app associated with this Auth service instance.

### currentUser
[method]currentUser returns [ref auth.User] or null;[/method]

The currently signed-in user (or null if no user signed in).

### languageCode
[method]languageCode returns String or null;[/method]

The current Auth instance's language code. This is a readable/writable property. When set to null, the default Firebase Console language setting is applied. The language code will propagate to email action templates (password reset, email verification and email change revocation) and SMS templates for phone authentication operations provided the specified providers support localization with the language code specified.

[collapse Example]
```js
console.log(firebase.auth().languageCode); // null
firebase.auth().languageCode = 'fr';
console.log(firebase.auth().languageCode); // 'fr'
```
[/collapse]

## Unsupported Methods

The following methods are not supported in RNFirebase as they cannot work in the React Native environment or have a different implementation.

### getRedirectResult

### setPersistence

### signInWithPopup

### signInWithRedirect

### useDeviceLanguage

An outstanding iOS SDK bug is preventing `useDeviceLanguage` from being supported. Until this is fix, we recommend using `languageCode` to set the language by using an external [library](https://github.com/rebeccahughes/react-native-device-info) to get the device locale.

