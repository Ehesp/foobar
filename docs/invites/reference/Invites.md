# Dynamic Links

!> Invites has been removed from the Firebase SDKs, and removed here as of v5.5.0. This documentation is only here for users of older versions of the library. Use Dynamic Links instead.

[Firebase Invites](https://firebase.google.com/docs/invites/) are an out-of-the-box solution for app referrals and sharing via email or SMS.

## Methods

The following methods are accessed via the default app's Invites instance `firebase.invites()`.

### getInitialInvitation
[method]getInitialInvitation() returns Promise containing nullable [ref invites.InvitationOpen];[/method]

Returns the Invitation that the app has been launched from. If the app was not launched from an Invitation the return value will be null.

[collapse Example]
```javascript
firebase.invites()
    .getInitialInvitation()
    .then((invitation) => {
        if (invitation) {
            // app opened from an Invitation
        } else {
           // app NOT opened from an invitation
        }
    });
```
[/collapse]

### onInvitation
[method]onInvitation(listener) returns Function;[/method]

When an invitation is opened whilst the app is open, the listener is invoked with the invitation.

Returns an unsubscribe function.

Parameter |         |
| --------- | ------- |
| listener   | **function([ref invitations.InvitationOpen])**<br /> This function is called when an invitation is opened. |

[collapse Example]
```javascript
// subscribe
const unsubscribe = firebase.invites().onInvitation((invitation) => {
  // ...
});

// unsubscribe
unsubscribe();
```
[/collapse]

### sendInvitation
[method]sendInvitation(invitation) returns Promise containing Array of string;[/method]

!> on iOS, the user must be signed in with their Google Account for this to work.

Displays the invitation dialog which allows the user to select who received the invitation.

Returns a promise that resolves with the created invitation IDs if the invitation is sent, otherwise it is rejected with an error.

| Parameter |         |
| --------- | ------- |
| invitation   | **[ref invitations.Invitation]** <br /> The invitation to send.  |

[collapse Example]
```javascript
// create invitation
const invitation = new firebase.invites.Invitation('Title', 'Message');
invitation.setDeepLink('https://je786.page.link/testing');
// send the invitation
const invitationIds = await firebase.invites().sendInvitation(invitation);
// use the invitationIds as you see fit
```
[/collapse]
