# Social Auth

A common misconception is that RNFirebase provides social login out of the box. This is somewhat true, it leaves the implementation of the login provider up to the user and only signs the user in once the provider data has been returned.

Firebase allows a number of social providers to be used out of the box; Facebook, Google, Twitter and Github. You can however choose any provider you wish assuming they have an oAuth API.

## Facebook

Facebook provide a wrapper around their Android & iOS SDKs called [react-native-fbsdk](https://github.com/facebook/react-native-fbsdk). This module handles the flow of logging in a user and obtaining their `accessToken`. The main benefit of using the native SDK is that it detects whether the user has the Facebook app installed and falls back to the web if not.

The `react-native-fbsdk` library allows us to first login (using `LoginManager`) and then obtain the users `accessToken` (using `AccessToken`). Once we have the access token we need to create a credential using [ref auth.FacebookAuthProvider#credential] and then sign in with that credential using [ref auth#signInWithCredential]:

```js
import { AccessToken, LoginManager } from 'react-native-fbsdk';
import firebase from 'react-native-firebase'

// Calling the following function will open the FB login dialogue:
const facebookLogin = async () => {
  try {
    const result = await LoginManager.logInWithReadPermissions(['public_profile', 'email']);

    if (result.isCancelled) {
      throw new Error('User cancelled request'); // Handle this however fits the flow of your app
    }

    console.log(`Login success with permissions: ${result.grantedPermissions.toString()}`);

    // get the access token
    const data = await AccessToken.getCurrentAccessToken();

    if (!data) {
      throw new Error('Something went wrong obtaining the users access token'); // Handle this however fits the flow of your app
    }

    // create a new firebase credential with the token
    const credential = firebase.auth.FacebookAuthProvider.credential(data.accessToken);

    // login with credential
    const currentUser = await firebase.auth().signInAndRetrieveDataWithCredential(credential);

    console.info(JSON.stringify(currentUser.user.toJSON()))
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
export const googleLogin = async () => {
  try {
    // Add any configuration settings here:
    await GoogleSignin.configure();

    const data = await GoogleSignin.signIn();

    // create a new firebase credential with the token
    const credential = firebase.auth.GoogleAuthProvider.credential(data.idToken, data.accessToken)
    // login with credential
    const currentUser = await firebase.auth().signInAndRetrieveDataWithCredential(credential);

    console.info(JSON.stringify(currentUser.user.toJSON()));
  } catch (e) {
    console.error(e);
  }
}

```

## Twitter

## Github

## Custom Provider
