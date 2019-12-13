# Invitation

!> Invites has been removed from the Firebase SDKs, and removed here as of v5.5.0. This documentation is only here for users of older versions of the library. Use Dynamic Links instead.

```
firebase.invites.Invitation
```

### Constructor
[method]new firebase.invites.Invitation(title, message);[/method]

Create an invitation.

To send an Invitation, first populate it by using the `setX` methods described below, then pass it to `firebase.invites().sendInvitation(invitation)`;

| Parameter |         |
| --------- | ------- |
| title    | **string** |
| message     | **string** |

## Properties

### android
[method]android returns nullable [ref invites.AndroidInvitation];[/method]

Access Android specific invitation methods.

## Methods

### setAndroidClientId
[method]setAndroidClientId(androidClientId) returns [ref invites.Invitation];[/method]

Set the Android target client ID for the invitation.

| Parameter |         |
| --------- | ------- |
| androidClientId  | **string** <br /> The android client ID. |

### setAndroidMinimumVersionCode
[method]setAndroidMinimumVersionCode(androidMinimumVersionCode) returns [ref invites.Invitation];[/method]

Sets the minimum version of the android app installed on the receiving device. If this minimum version is not installed then the install flow will be triggered.

| Parameter |         |
| --------- | ------- |
| androidMinimumVersionCode  | **number** <br /> Minimum version of the android app. |

### setCallToActionText
[method]setCallToActionText(callToActionText) returns [ref invites.Invitation];[/method]

Text shown on the email invitation for the user to accept the invitation. Default install text used if not set.

| Parameter |         |
| --------- | ------- |
| callToActionText  | **string** <br /> Text to use on the invitation button. |

### setCustomImage
[method]setCustomImage(customImage) returns [ref invites.Invitation];[/method]

Sets an image for invitations.

| Parameter |         |
| --------- | ------- |
| customImage  | **string** <br /> the image Uri. The Uri is required to be in absolute format. The supported image formats are "jpg", "jpeg" and "png". |

### setDeepLink
[method]setDeepLink(deepLink) returns [ref invites.Invitation];[/method]

Sets the deep link that is made available to the app when opened from the invitation. This deep link is made available both to a newly installed application and an already installed application. The deep link can be sent to Android and other platforms so should be formatted to support deep links across platforms.

| Parameter |         |
| --------- | ------- |
| deepLink  | **string** <br /> The app deep link. |

### setIOSClientId
[method]setIOSClientId(iosClientId) returns [ref invites.Invitation];[/method]

Set the iOS target client ID for the invitation.

| Parameter |         |
| --------- | ------- |
| iosClientId  | **string** <br /> The iOS client ID. |
