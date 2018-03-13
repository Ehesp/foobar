# iOS Installation

First ensure you have followed the [initial setup guide](version /installation/initial-setup).

## Add the pod

Add the following to your `Podfile`:

```ruby
pod 'Firebase/DynamicLinks'
```

Run `pod update`.

## Configure XCode

1. In your [Firebase console](https://console.firebase.google.com/), open the Dynamic Links section.
    1. Accept the terms of service if you are prompted to do so.
    2. Take note of your project's Dynamic Links domain, which is displayed at the top of the Dynamic Links page. You need your project's Dynamic Links domain to programmatically create Dynamic Links. A Dynamic Links domain looks like app_code.app.goo.gl.
    
        ![console](https://firebase.google.com/docs/dynamic-links/images/dynamic-links-domain.png)

2. Ensure that your app's App Store ID and your Apple Developer Team ID is specified in your app's settings. To view and edit your app's settings, go to your Firebase project's Settings page and select your iOS app.
   You can confirm that your Firebase project is properly configured to use Dynamic Links in your iOS app by opening the following URL:
   
   ```text
   https://app_code.app.goo.gl/apple-app-site-association
   ```
       
     If your app is connected, the apple-app-site-association file contains a reference to your app's App Store ID and bundle ID. For example:
       
   ```javascript
   {"applinks":{"apps":[],"details":[{"appID":"1234567890.com.example.ios","paths":["/*"]}]}}
   ```
       
     If the details field is empty, double-check that you specified your Team ID.
3. In the Info tab of your app's XCode project, create a new URL type to be used for Dynamic Links. Set the `Identifier` field to a unique value and the URL scheme field to either your bundle identifier or a unique value.

4. In the Capabilities tab of your app's Xcode project, enable Associated Domains and add the following to the Associated Domains list: `applinks:app_code.app.goo.gl` where `app_code` is your dynamic links domain application code as in step *1.2* above.

5. Update your `AppDelegate.m` file:
    1. Import RN Firebase Links header file:
    
        ```objectivec
        #import "RNFirebaseLinks.h"
        ```
        
    2. Add the following to the `didFinishLaunchingWithOptions` method before `[FIRApp Configure]`:

        ```objectivec
        [FIROptions defaultOptions].deepLinkURLScheme = CUSTOM_URL_SCHEME;
        ```

        ^-- where `CUSTOM_URL_SCHEME` is the custom URL scheme you defined in your Xcode project.
    3. For **iOS 8** and older add the following inside the `@implementation AppDelegate` annotation:
    
        ```objectivec
        - (BOOL)application:(UIApplication *)application
                    openURL:(NSURL *)url
                    options:(NSDictionary<NSString *, id> *)options {
            return [RNFirebaseLinks application:application
                                          openURL:url
                                          options:options];
        }
        ```
        
    4.  For **iOS 9** and newer add the following inside the `@implementation AppDelegate` annotation:
    
        ```objectivec
        - (BOOL)application:(UIApplication *)application
                    openURL:(NSURL *)url
                    options:(NSDictionary<NSString *, id> *)options {
            return [RNFirebaseLinks application:application
                                        openURL:url
                                        options:options];
        }

        - (BOOL)application:(UIApplication *)application
        continueUserActivity:(NSUserActivity *)userActivity
         restorationHandler:(void (^)(NSArray *))restorationHandler {
             return [RNFirebaseLinks application:application
                              continueUserActivity:userActivity
                                restorationHandler:restorationHandler];
        }
        ```

    > You might run into situation when you need to handle more than one link configuration
    > i.e. when using Facebook SDK to handle push notification / login links
    > if that is the case you can perform check below

    ```objectivec
    - (BOOL)application:(UIApplication *)application 
    openURL:(NSURL *)url 
    options:(NSDictionary<UIApplicationOpenURLOptionsKey,id> *)options {
    
        BOOL handled = [[FBSDKApplicationDelegate sharedInstance] 
        application:application 
        openURL:url 
        sourceApplication:options[UIApplicationOpenURLOptionsSourceApplicationKey] 
        annotation:options[UIApplicationOpenURLOptionsAnnotationKey]];
        
        if (!handled) {
            handled = [RNFirebaseLinks application:application openURL:url options:options];
        } 

        return handled;
    }
    ```
        
    
