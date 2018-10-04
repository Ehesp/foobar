# Phone Auth

RNFirebase provides two methods to sign users in with their phone number; [ref auth#signInWithPhoneNumber] and [ref auth#verifyPhoneNumber]. Both provide a different workflow to tie it best into your app; `signInWithPhoneNumber` will sign the user in automatically once the user had confirmed their phone number, whilst `verifyPhoneNumber` will provide feedback on the current verification state but requires you to manually sign the user in once confirmed.

## signInWithPhoneNumber

`signInWithPhoneNumber` is a more straight-forward implementation of handling the auth flow, however it provides less flexibility to handle the various situations which may occur. 

### 1. Trigger phone auth

```js
firebase.auth().signInWithPhoneNumber(phoneNumber)
  .then(confirmResult => // save confirm result to use with the manual verification code)
  .catch(error => /error);
```

### 2. Confirm verification code

```js
confirmResult.confirm(verificationCode)
  .then(user => // User is logged in){
  .catch(error => // Error with verification code);
```

On iOS, this is all that is required.

However Android also provides "auto verification" if Google Play service can automatically detect the incoming message (and doesn't display it!).

### 3. [Android] Handle Auto Verification

To handle auto verification, we need to listen to [ref auth#onAuthStateChanged]:

```js
firebase.auth().onAuthStateChanged((user) => {
  if (user) // user is verified and logged in
});
```

### Full Example

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

## verifyPhoneNumber

This implementation gives you full control of the phone number verification flow on either platform as well as a flexible api to suit any UI flow and should be familiar to use if you've used things like storage, upload tasks / database on listeners.  It is of particular use if you want to link a phone credential with an existing account rather than just sign the user in.

### Example

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


