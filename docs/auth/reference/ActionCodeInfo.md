# ActionCodeInfo

A response from [ref auth#checkActionCode].

## Properties

### data
[method]data returns Object;[/method]

The data associated with the action code.

For the `PASSWORD_RESET`, `EMAIL_SIGNIN`, `VERIFY_EMAIL`, and `RECOVER_EMAIL` actions, this object contains an `email` field with the address the email was sent to.

For the `RECOVER_EMAIL` action, which allows a user to undo an email address change, this object also contains a `fromEmail` field with the user account's new email address. After the action completes, the user's email address will revert to the value in the `email` field from the value in `fromEmail` field.

```js
{
  email: string,
  fromEmail: string,
}
```

### operation
[method]operation returns string;[/method]

The type of operation that generated the action code. This could be:

- `PASSWORD_RESET`: password reset code generated via [ref auth.Auth#sendPasswordResetEmail].
- `VERIFY_EMAIL`: email verification code generated via [ref auth.User#sendEmailVerification].
- `RECOVER_EMAIL`: email change revocation code generated via [ref auth.User#updateEmail].
- `EMAIL_SIGNIN`: email sign-in code generated via [ref auth.Auth#sendSignInLinkToEmail].
