# DynamicLink

```
firebase.links.DynamicLink
```

### Constructor
[method]new firebase.links.DynamicLink(link, dynamicLinkDomain);[/method]

Builds a dynamic link.

To create a DynamicLink, first populate it by using the `setX` methods available on the properties described below, then pass it to `firebase.links().createDynamicLink(link)` or `firebase.links().createShortDynamicLink(link)`;

| Parameter |         |
| --------- | ------- |
| link    | **string** <br/> The link the target app will open. You can specify any URL the app can handle, such as a link to the app’s content, or a URL that initiates some app-specific logic such as crediting the user with a coupon, or displaying a specific welcome screen. This link must be a well-formatted URL, be properly URL-encoded, and use the HTTP or HTTPS scheme. |
| domainURIPrefix     | **string** <br/> The Firebase project’s Dynamic Links domain. You can find this value in the Dynamic Links section of the Firebase console. It must begin with `https://` |

## Properties

### analytics
[method]analytics returns nullable [ref links.AnalyticsParameters];[/method]

Access Google Analytics specific link properties.

### android
[method]android returns nullable [ref links.AndroidParameters];[/method]

Access Android specific link properties.

### ios
[method]ios returns nullable [ref links.IOSParameters];[/method]

Access iOS specific link properties.

### itunes
[method]itunes returns nullable [ref links.ITunesParameters];[/method]

Access iTunes Connect specific link properties.

### navigation
[method]navigation returns nullable [ref links.NavigationParameters];[/method]

Access navigation specific link properties.

### social
[method]social returns nullable [ref links.SocialParameters];[/method]

Access social specific link properties.
