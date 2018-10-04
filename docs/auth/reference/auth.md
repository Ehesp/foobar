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
[method]signInAnonymously() returns Promise containing [ref auth.UserCredential];[/method]

Asynchronously signs in as an anonymous user.

If there is already an anonymous user signed in, that user will be returned; otherwise, a new anonymous user identity will be created and returned.

#### Error Codes

| Code | Message |
| --------- | ------- |
| auth/operation-not-allowed   | Thrown if anonymous accounts are not enabled. Enable anonymous accounts in the Firebase Console, under the Auth tab.  |

### signInAnonymouslyAndRetrieveData
[method]signInAnonymouslyAndRetrieveData() returns Promise containing [ref auth.UserCredential];[/method]

Signs in a user anonymously and returns any additional user info data or credentials.

?> This method has been deprecated.

If there is already an anonymous user signed in, that user with additional date will be returned; otherwise, a new anonymous user identity will be created and returned.

#### Error Codes

| Code | Message |
| --------- | ------- |
| auth/operation-not-allowed   | Thrown if anonymous accounts are not enabled. Enable anonymous accounts in the Firebase Console, under the Auth tab.  |

### createUserAndRetrieveDataWithEmailAndPassword
[method]createUserAndRetrieveDataWithEmailAndPassword(email, password) returns Promise containing [ref auth.UserCredential];[/method]

Creates a new user account associated with the specified email address and password and returns any additional user info data or credentials.

?> This method has been deprecated.

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
| auth/email-already-in-use  | Thrown if there already exists an account with the given email address. |
| auth/invalid-email  | Thrown if the email address is not valid. |
| auth/operation-not-allowed | Thrown if email/password accounts are not enabled. Enable email/password accounts in the Firebase Console, under the Auth tab. |
| auth/weak-password | Thrown if the password is not strong enough. |

### createUserWithEmailAndPassword
[method]createUserWithEmailAndPassword(email, password) returns Promise containing [ref auth.UserCredential];[/method]

Creates a new user account associated with the specified email address and password.

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
| auth/email-already-in-use  | Thrown if there already exists an account with the given email address. |
| auth/invalid-email  | Thrown if the email address is not valid. |
| auth/operation-not-allowed | Thrown if email/password accounts are not enabled. Enable email/password accounts in the Firebase Console, under the Auth tab. |
| auth/weak-password | Thrown if the password is not strong enough. |

### signInAndRetrieveDataWithCredential
[method]signInAndRetrieveDataWithCredential(credential) returns Promise containing [ref auth.UserCredential];[/method]

Asynchronously signs in with the given credentials, and returns any available additional user information, such as user name.

?> This method has been deprecated.

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

?> This method has been deprecated.

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

?> This method has been deprecated.

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
[method]signInWithEmailAndPassword(email, password) returns Promise containing [ref auth.UserCredential];[/method]

Asynchronously signs in using an email and password.

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
[method]signInWithCustomToken(customToken) returns Promise containing [ref auth.UserCredential];[/method]

Asynchronously signs in using a custom token.

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
[method]signInWithCredential(credential) returns Promise containing [ref auth.UserCredential];[/method]

Asynchronously signs in with the given credentials.

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
[method]signInWithPhoneNumber(phoneNumber: string, forceResend?: boolean) returns Promise containing [ref auth.ConfirmationResult];[/method]

Asynchronously signs in using a phone number.

Returns a [ref auth.ConfirmationResult]. Use [ref auth.ConfirmationResult#confirm] with the verification code to confirm the phone number. In case of Android auto verification, use [ref auth#onAuthStateChanged] to listen incase the SMS is not shown to the user. See [this guide](version /auth/phone-auth#signInWithPhoneNumber) for more information.

[collapse Example]

```js
import React, { Component } from 'react';
import { View, Button, Text, TextInput, Image } from 'react-native';

import firebase from 'react-native-firebase';

const successImageUri = 'https://cdn.pixabay.com/photo/2015/06/09/16/12/icon-803718_1280.png';

export default class PhoneAuthTest extends Component {
  constructor(props) {
    super(props);
    this.unsubscribe = null;
    this.state = {
      user: null,
      message: '',
      codeInput: '',
      phoneNumber: '+44',
      confirmResult: null,
    };
  }

  componentDidMount() {
    this.unsubscribe = firebase.auth().onAuthStateChanged((user) => {
      if (user) {
        this.setState({ user: user.toJSON() });
      } else {
        // User has been signed out, reset the state
        this.setState({
          user: null,
          message: '',
          codeInput: '',
          phoneNumber: '+44',
          confirmResult: null,
        });
      }
    });
  }

  componentWillUnmount() {
     if (this.unsubscribe) this.unsubscribe();
  }

  signIn = () => {
    const { phoneNumber } = this.state;
    this.setState({ message: 'Sending code ...' });

    firebase.auth().signInWithPhoneNumber(phoneNumber)
      .then(confirmResult => this.setState({ confirmResult, message: 'Code has been sent!' }))
      .catch(error => this.setState({ message: `Sign In With Phone Number Error: ${error.message}` }));
  };

  confirmCode = () => {
    const { codeInput, confirmResult } = this.state;

    if (confirmResult && codeInput.length) {
      confirmResult.confirm(codeInput)
        .then((user) => {
          this.setState({ message: 'Code Confirmed!' });
        })
        .catch(error => this.setState({ message: `Code Confirm Error: ${error.message}` }));
    }
  };

  signOut = () => {
    firebase.auth().signOut();
  }

  renderPhoneNumberInput() {
   const { phoneNumber } = this.state;

    return (
      <View style={{ padding: 25 }}>
        <Text>Enter phone number:</Text>
        <TextInput
          autoFocus
          style={{ height: 40, marginTop: 15, marginBottom: 15 }}
          onChangeText={value => this.setState({ phoneNumber: value })}
          placeholder={'Phone number ... '}
          value={phoneNumber}
        />
        <Button title="Sign In" color="green" onPress={this.signIn} />
      </View>
    );
  }

  renderMessage() {
    const { message } = this.state;

    if (!message.length) return null;

    return (
      <Text style={{ padding: 5, backgroundColor: '#000', color: '#fff' }}>{message}</Text>
    );
  }

  renderVerificationCodeInput() {
    const { codeInput } = this.state;

    return (
      <View style={{ marginTop: 25, padding: 25 }}>
        <Text>Enter verification code below:</Text>
        <TextInput
          autoFocus
          style={{ height: 40, marginTop: 15, marginBottom: 15 }}
          onChangeText={value => this.setState({ codeInput: value })}
          placeholder={'Code ... '}
          value={codeInput}
        />
        <Button title="Confirm Code" color="#841584" onPress={this.confirmCode} />
      </View>
    );
  }

  render() {
    const { user, confirmResult } = this.state;
    return (
      <View style={{ flex: 1 }}>

        {!user && !confirmResult && this.renderPhoneNumberInput()}

        {this.renderMessage()}

        {!user && confirmResult && this.renderVerificationCodeInput()}

        {user && (
          <View
            style={{
              padding: 15,
              justifyContent: 'center',
              alignItems: 'center',
              backgroundColor: '#77dd77',
              flex: 1,
            }}
          >
            <Image source={{ uri: successImageUri }} style={{ width: 100, height: 100, marginBottom: 25 }} />
            <Text style={{ fontSize: 25 }}>Signed In!</Text>
            <Text>{JSON.stringify(user)}</Text>
            <Button title="Sign Out" color="red" onPress={this.signOut} />
          </View>
        )}
      </View>
    );
  }
}
```

[/collapse]

| Parameter |         |
| --------- | ------- |
| phoneNumber | **string** <br /> Phone number containing country code (e.g. +44) |
| forceResend | **boolean** <br /> Android only - Force resend sms code - only applies to subsequent requests after sending the first code. |

#### Error Codes

TODO

### verifyPhoneNumber
[method]verifyPhoneNumber(phoneNumber, autoVerifyTimeoutOrForceResend?: number | boolean, forceResend?: boolean) returns TODO;[/method]

This implementation gives you full control of the phone number verification flow on either platform as well as a flexible api to suit any UI flow and should be familiar to use if you've used things like storage, upload tasks / database on listeners. It is of particular use if you want to link a phone credential with an existing account rather than just sign the user in.

[collapse Example]

```js
firebase.auth()
  .verifyPhoneNumber(phoneNumber)
  .on('state_changed', (phoneAuthSnapshot) => {
    // How you handle these state events is entirely up to your ui flow and whether
    // you need to support both ios and android. In short: not all of them need to
    // be handled - it's entirely up to you, your ui and supported platforms.

    // E.g you could handle android specific events only here, and let the rest fall back
    // to the optionalErrorCb or optionalCompleteCb functions
    switch (phoneAuthSnapshot.state) {
      // ------------------------
      //  IOS AND ANDROID EVENTS
      // ------------------------
      case firebase.auth.PhoneAuthState.CODE_SENT: // or 'sent'
        console.log('code sent');
        // on ios this is the final phone auth state event you'd receive
        // so you'd then ask for user input of the code and build a credential from it
        // as demonstrated in the `signInWithPhoneNumber` example above
        break;
      case firebase.auth.PhoneAuthState.ERROR: // or 'error'
        console.log('verification error');
        console.log(phoneAuthSnapshot.error);
        break;

      // ---------------------
      // ANDROID ONLY EVENTS
      // ---------------------
      case firebase.auth.PhoneAuthState.AUTO_VERIFY_TIMEOUT: // or 'timeout'
        console.log('auto verify on android timed out');
        // proceed with your manual code input flow, same as you would do in
        // CODE_SENT if you were on IOS
        break;
      case firebase.auth.PhoneAuthState.AUTO_VERIFIED: // or 'verified'
        // auto verified means the code has also been automatically confirmed as correct/received
        // phoneAuthSnapshot.code will contain the auto verified sms code - no need to ask the user for input.
        console.log('auto verified on android');
        console.log(phoneAuthSnapshot);
        // Example usage if handling here and not in optionalCompleteCb:
        // const { verificationId, code } = phoneAuthSnapshot;
        // const credential = firebase.auth.PhoneAuthProvider.credential(verificationId, code);

        // Do something with your new credential, e.g.:
        // firebase.auth().signInWithCredential(credential);
        // firebase.auth().currentUser.linkWithCredential(credential);
        // etc ...
        break;
    }
  }, (error) => {
    // optionalErrorCb would be same logic as the ERROR case above,  if you've already handed
    // the ERROR case in the above observer then there's no need to handle it here
    console.log(error);
    // verificationId is attached to error if required
    console.log(error.verificationId);
  }, (phoneAuthSnapshot) => {
    // optionalCompleteCb would be same logic as the AUTO_VERIFIED/CODE_SENT switch cases above
    // depending on the platform. If you've already handled those cases in the observer then
    // there's absolutely no need to handle it here.

    // Platform specific logic:
    // - if this is on IOS then phoneAuthSnapshot.code will always be null
    // - if ANDROID auto verified the sms code then phoneAuthSnapshot.code will contain the verified sms code
    //   and there'd be no need to ask for user input of the code - proceed to credential creating logic
    // - if ANDROID auto verify timed out then phoneAuthSnapshot.code would be null, just like ios, you'd
    //   continue with user input logic.
    console.log(phoneAuthSnapshot);
  });
// optionally also supports .then & .catch instead of optionalErrorCb &
// optionalCompleteCb (with the same resulting args)
```

[/collapse]

| Parameter |         |
| --------- | ------- |
| phoneNumber | **string** <br /> Phone number containing country code (e.g. +44) |
| autoVerifyTimeout | **number** <br /> Android only -  On some devices Google Play services can automatically detect the incoming verification SMS and perform verification without user action; this option sets the timeout for how long this will try and automatically detect the code. |
| forceResend | **boolean** <br /> Android only - Force resend sms code - only applies to subsequent requests after sending the first code. |

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
| auth/expired-action-code  | Thrown if the password reset code has expired. |
| auth/invalid-action-code | Thrown if the password reset code is invalid. This can happen if the code is malformed or has already been used. |
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
| auth/expired-action-code  | Thrown if the password reset code has expired. |
| auth/invalid-action-code | Thrown if the password reset code is invalid. This can happen if the code is malformed or has already been used. |
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
| auth/expired-action-code  | Thrown if the password reset code has expired. |
| auth/invalid-action-code | Thrown if the password reset code is invalid. This can happen if the code is malformed or has already been used. |
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

### settings
[method]settings returns [ref auth.AuthSettings];[/method]

The current Auth instance's settings. This is used to edit/read configuration related options like app verification mode for phone authentication.

## Unsupported Methods

The following methods are not supported in RNFirebase as they cannot work in the React Native environment or have a different implementation.

### getRedirectResult

### setPersistence

### signInWithPopup

### signInWithRedirect

### useDeviceLanguage

An outstanding iOS SDK bug is preventing `useDeviceLanguage` from being supported. Until this is fix, we recommend using `languageCode` to set the language by using an external [library](https://github.com/rebeccahughes/react-native-device-info) to get the device locale.

