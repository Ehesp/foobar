# Social Auth

A common misconception is that RNFirebase provides social login out of the box. This is somewhat true, it leaves the implementation of the login provider up to the user and only signs the user in once the provider data has been returned.

Firebase allows a number of social providers to be used out of the box; Facebook, Google, Twitter and Github. You can however choose any provider you wish assuming they have an oAuth API.

## Apple

For Apple Authentication please see our [`@invertase/react-native-apple-authentication`](https://github.com/invertase/react-native-apple-authentication) library which integrates well with Firebase and provides Firebase + Apple Auth examples.
The [@invertase/react-native-apple-authentication](https://github.com/invertase/react-native-apple-authentication) provides a library that helps manage Apple authentication easily.

**Step 1**: Login with Apple.

```js
import firebase from 'react-native-firebase';
import appleAuth, {
  AppleButton,
  AppleAuthRequestScope,
  AppleAuthRequestOperation
  } from '@invertase/react-native-apple-authentication';
/**
 * Note the sign in request can error, e.g. if the user cancels the sign-in.
 * Use `AppleAuthError` to determine the type of error, e.g. `error.code === AppleAuthError.CANCELED`
 */
async function onAppleButtonPress() {
  // 1). start a apple sign-in request
  const appleAuthRequestResponse = await appleAuth.performRequest({
    requestedOperation: AppleAuthRequestOperation.LOGIN,
    requestedScopes: [AppleAuthRequestScope.EMAIL, AppleAuthRequestScope.FULL_NAME],
  });
  // 2). if the request was successful, extract the token and nonce
  const { identityToken, nonce } = appleAuthRequestResponse;
}
```

**Step 2**: Create a Firebase credential with the `identityToken` & `nonce`.

```js
// can be null in some scenarios
if (identityToken) {
  // 3). create a Firebase `AppleAuthProvider` credential
  const appleCredential = firebase.auth.AppleAuthProvider.credential(identityToken, nonce);
}
```

**Step 3**: Sign in to Firebase with the created credential.

```js
// 4). use the created `AppleAuthProvider` credential to start a Firebase auth request,
//     in this example `signInWithCredential` is used, but you could also call `linkWithCredential`
//     to link the account to an existing user
const userCredential = await firebase.auth().signInWithCredential(appleCredential);
// user is now signed in, any Firebase `onAuthStateChanged` listeners you have will trigger
console.warn(`Firebase authenticated via Apple, UID: ${userCredential.user.uid}`);
```

## Facebook

Facebook provide a wrapper around their Android & iOS SDKs called [react-native-fbsdk](https://github.com/facebook/react-native-fbsdk). This module handles the flow of logging in a user and obtaining their `accessToken`. The main benefit of using the native SDK is that it detects whether the user has the Facebook app installed and falls back to the web if not.

The `react-native-fbsdk` library allows us to first login (using `LoginManager`) and then obtain the users `accessToken` (using `AccessToken`). Once we have the access token we need to create a credential using [ref auth.FacebookAuthProvider#credential] and then sign in with that credential using [ref auth#signInWithCredential]:

```js
import { AccessToken, LoginManager } from 'react-native-fbsdk';
import firebase from 'react-native-firebase'

// Calling the following function will open the FB login dialogue:
export async function facebookLogin() {
  try {
    const result = await LoginManager.logInWithReadPermissions(['public_profile', 'email']);

    if (result.isCancelled) {
      // handle this however suites the flow of your app
      throw new Error('User cancelled request'); 
    }

    console.log(`Login success with permissions: ${result.grantedPermissions.toString()}`);

    // get the access token
    const data = await AccessToken.getCurrentAccessToken();

    if (!data) {
      // handle this however suites the flow of your app
      throw new Error('Something went wrong obtaining the users access token');
    }

    // create a new firebase credential with the token
    const credential = firebase.auth.FacebookAuthProvider.credential(data.accessToken);

    // login with credential
    const firebaseUserCredential = await firebase.auth().signInWithCredential(credential);

    console.warn(JSON.stringify(firebaseUserCredential.user.toJSON()))
  } catch (e) {
    console.error(e);
  }
}
```

## Google

We recommend using [react-native-google-signin](https://github.com/react-native-community/react-native-google-signin) for Google authentication.  This module handles the flow of logging in a user and obtaining their `accessToken` and `idToken` by wrapping around the offical Google login library. This means you get a much smoother experience than using a standard OAuth library, particularly on Android.

The `react-native-google-signin` library allows us to login (using `GoogleSignin`) which returns an optional `accessToken` and `idToken`. Once we have the two tokens we need to create a credential using [ref auth.GoogleAuthProvider#credential] and then sign in with that credential using [ref auth#signInWithCredential]:

```js
import { GoogleSignin } from 'react-native-google-signin';
import firebase from 'react-native-firebase'

// Calling this function will open Google for login.
export async function googleLogin() {
  try {
    // add any configuration settings here:
    await GoogleSignin.configure();

    const data = await GoogleSignin.signIn();

    // create a new firebase credential with the token
    const credential = firebase.auth.GoogleAuthProvider.credential(data.idToken, data.accessToken)
    // login with credential
    const firebaseUserCredential = await firebase.auth().signInWithCredential(credential);

    console.warn(JSON.stringify(firebaseUserCredential.user.toJSON()));
  } catch (e) {
    console.error(e);
  }
}

```

## Twitter
You can use [`react-native-twitter-signin`](https://github.com/GoldenOwlAsia/react-native-twitter-signin) for Twitter authentication. This library handles the flow of logging in a user and accessing their `authToken` and `authTokenSecret` by wrapping around the official Twitter library.

The`react-native-twitter-signin` library allows us to login (using `RNTwitterSignIn`) which returns `authToken` and `authTokenSecret`

Make sure you thoroughly follow the instructions on setting up the necessary requirements to get `react-native-twitter-signin` working.


```js
import { NativeModules } from 'react-native';
import firebase from 'react-native-firebase';

const { RNTwitterSignIn } = NativeModules;
const { TwitterAuthProvider } = firebase.auth;

const TwitterKeys = {
  TWITTER_CONSUMER_KEY: 'PLACE_YOUR_TWITTER_CONSUMER_KEY_HERE',
  TWITTER_CONSUMER_SECRET: 'PLACE_YOUR_TWITTER_CONSUMER_SECRET_HERE'
};

export async function twitterLogin() {
  try {
    await RNTwitterSignIn.init(TwitterKeys.TWITTER_CONSUMER_KEY, TwitterKeys.TWITTER_CONSUMER_SECRET);

    // also includes: name, userID & userName
    const { authToken, authTokenSecret } = await RNTwitterSignIn.logIn();    
    
    const credential = TwitterAuthProvider.credential(authToken, authTokenSecret);
    
    const firebaseUserCredential = await firebase.auth().signInWithCredential(credential);

    console.warn(JSON.stringify(firebaseUserCredential.user.toJSON()));
  } catch (e) {
    console.error(e);
  }
}
```

## Github

> TODO - PRs Welcome.

## Custom Provider

> TODO - PRs Welcome.
