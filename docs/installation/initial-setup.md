## Install

Install React Native Firebase from NPM:

```bash
npm install --save react-native-firebase
```

## Firebase

The first thing you'll need to have is an active Firebase project.

If you already have an existing project you can skip to the [Platform Specific Installation](#Platform-Specific-Installation) section.

### Creating a new project

 - Visit the [Firebase console](https://firebase.google.com/console).
 - Click the `Add project` box as shown below: 
 
 ![Dashboard](https://i.imgur.com/ZsSH1bJ.png)

 - A dialog will appear as shown below
   - Enter your new **project name** and modify the **project id** and **region** if necessary
   - Click `Create Project` when finished
   - Your project will now be created - this can take a few seconds
   - Once created click the `Continue` button

 ![New Project Dialog](https://i.imgur.com/50I2bvj.png)

 - Once created you'll be redirected to the project homepage as show below
 
 ![New Project Homepage](https://i.imgur.com/vebPTf1.png)

## Platform Specific Installation

Both Android and iOS require additional installation steps, please follow the platform specific guides bellow:
 
 - [Android](version /installation/android) 
 - [iOS](version /installation/ios).
 
---
 
## Usage

Once you've completed setting up React Native Firebase you can now use the library within your JavaScript code like any other node module

> The default app is pre-initialized natively therefore there is **no** need to call `initializeApp` for the default app instance.

### Example Usage

```javascript
import firebase from 'react-native-firebase';

firebase.auth()
  .signInAnonymously()
  .then(credential => {
    if (credential) {
      console.log('default app user ->', credential.user.toJSON());
    }
  });
```

### Creating multiple app instances

React Native Firebase supports multiple app instances. For more information see the [initializing multiple apps documentation](version /core/initialize-apps).


---


## Guides

We've curated some articles we love below to help you get started.

### By Invertase

| Links |
|:---------:|
|[Getting started with Cloud Firestore on React Native](https://blog.invertase.io/getting-started-with-cloud-firestore-on-react-native-b338fb6525b9)|

> Found an article you like that's not listed below? Submit a PR to add it here and we'll review it (hint: click on the ✏️ edit button at the top of this page to edit this file on GitHub).


### By the community

These guides are written by the community and may or may not be up to date.

| Links |
|:---------:|
|[Building a Google Analytics Funnel from Firebase in React-Native](https://blog.theodo.fr/2018/01/building-google-analytics-funnel-firebase-react-native/)|
|[Getting started with Firebase Authentication on React Native](https://blog.invertase.io/getting-started-with-firebase-authentication-on-react-native-a1ed3d2d6d91)|
|[React Native Push Notifications with Firebase Cloud Functions](https://medium.com/the-modern-development-stack/react-native-push-notifications-with-firebase-cloud-functions-74b832d45386)|
|[Firebase Environments with React Native (Dev/Staging/Prod)](https://medium.com/@egunsoma/firebase-environments-with-react-native-dev-staging-prod-3832d7d22a80)|
|[Adding Firebase Analytics to your React Native app](https://www.measurelab.co.uk/blog/adding-firebase-analytics-react-native-app/)|

---

Made with 💛 by [Invertase](http://invertase.io)
