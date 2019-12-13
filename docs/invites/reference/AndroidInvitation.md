# Invitation

!> Invites has been removed from the Firebase SDKs, and removed here as of v5.5.0. This documentation is only here for users of older versions of the library. Use Dynamic Links instead.

Android specific invitation settings.

## Methods

### setAdditionalReferralParameters
[method]setAdditionalReferralParameters(additionalReferralParameters) returns [ref invites.Invitation];[/method]

Adds query parameters to the play store referral URL when the app needs additional referral parameters for other application component referrals. These parameters are added to the referral URL sent from the play store and are available to be processed by other application components, for example Google Analytics. The parameters are set as name, value pairs that will be set as query parameter name and value on the referral URL.

| Parameter |         |
| --------- | ------- |
| additionalReferralParameters  | **Object** <br /> Referral parameters defined as name value pairs. |

### setEmailHtmlContent
[method]setEmailHtmlContent(emailHtmlContent) returns [ref invites.Invitation];[/method]

Sets the HTML-formatted (UTF-8 encoded, no JavaScript) content for invites sent through email. If set, this will be sent instead of the default email.

emailHtmlContent must be valid HTML for standard email processing. The pattern %%APPINVITE_LINK_PLACEHOLDER%% should be embedded in your htmlContent and will be replaced with the invitation URL. This url is a link that will launch the app if already installed or take the user to the appropriate app store if not. In both cases the deep link will be available if provided using setDeepLink(Uri).

| Parameter |         |
| --------- | ------- |
| emailHtmlContent  | **number** <br /> The html-formatted content for the email. |

### setEmailSubject
[method]setEmailSubject(emailSubject) returns [ref invites.Invitation];[/method]

Sets the subject for invites sent by email.

| Parameter |         |
| --------- | ------- |
| emailSubject  | **string** <br /> The subject for the email. |

### setGoogleAnalyticsTrackingId
[method]setGoogleAnalyticsTrackingId(googleAnalyticsTrackingId) returns [ref invites.Invitation];[/method]

Sets the Google Analytics Tracking id. The tracking id should be created for the calling application under Google Analytics. See more about how to get a tracking id . The tracking id is recommended so that invitations sent from the calling application are available in Google Analytics.

| Parameter |         |
| --------- | ------- |
| googleAnalyticsTrackingId  | **string** <br /> String of the form UA-xxxx-y |
