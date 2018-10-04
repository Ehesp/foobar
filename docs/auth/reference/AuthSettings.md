# AuthSettings

```js
firebase.auth().settings;
```

Interface representing an Auth instance's settings, currently used for enabling/disabling app verification for phone Auth testing.

In order to use this feature, you will need to [whitelist your phone number](https://firebase.google.com/docs/auth/web/phone-auth#test-with-whitelisted-phone-numbers) via the Firebase Console.

?> These are for testing purposes, ensure you're not using them in the public release version of your app.

An example use in e2e testing can be seen in our tests suite [here](https://github.com/invertase/react-native-firebase/blob/master/tests/e2e/auth/phone.e2e.js).

## Properties

### appVerificationDisabledForTesting
[method]appVerificationDisabledForTesting returns boolean;[/method]

> **iOS only**

When set, this property disables app verification for the purpose of testing phone authentication. 
For this property to take effect, it needs to be set calling any phone auth methods.
When this is disabled, a mock reCAPTCHA is rendered instead. This is useful for manual testing during development or for automated integration tests.

The default value is false (app verification is enabled).

```js
// example

// disable verification
firebase.auth().settings.appVerificationDisabledForTesting = true;
// enable verification
firebase.auth().settings.appVerificationDisabledForTesting = false;
```

## Methods

### setAutoRetrievedSmsCodeForPhoneNumber
[method]setAutoRetrievedSmsCodeForPhoneNumber(phoneNumber, smsCode) returns Promise<null>;[/method]

> **Android only**

| Parameter |         |
| --------- | ------- |
| phoneNumber      | **string** |
| smsCode      | **string** |

Once this has been called, every call to [ref auth.Auth#verifyPhoneNumber] or [ref auth.Auth#signInWithPhoneNumber] with the
same phone number as the one that is configured here will automatically trigger verification (auto verify) without manual input of the code being required.


> The phone number and SMS code here must have been configured in the Firebase Console (Authentication > Sign In Method > Phone).


Calling this method a second time will overwrite the previously passed parameters. Only one number can be configured at a given time.


Calling this method with either parameter set to null removes this functionality until valid parameters are passed. Verifying a phone number other than the one configured here will trigger normal behaviour. If the phone number is configured as a test phone number in the console, the regular testing flow occurs. Otherwise, normal phone number verification will take place.

```js
// example
await firebase
.auth()
.settings
.setAutoRetrievedSmsCodeForPhoneNumber(
  TEST_PHONE_A,
  TEST_CODE_A
);
```
