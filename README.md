# React Native Firebase Docs

This repository contains the documentation for the [RNFirebase documentation](https://invertase.io/oss/react-native-firebase).

## Internal Links

Along with the normal markdown linking (`[text](link)`), the following markdown can also be used to make linking easier around the site:

### ref

Creates a link to a module reference file and method under the same version:

```
[ref auth] // to /docs/<version>/auth/auth/auth
[ref auth#signInWithEmailAndPassword] // to /docs/<version>/auth/reference/auth#signInWithEmailAndPassword
[ref auth.User#uid] // to /docs/<version>/auth/reference/User#uid
```

### version

Creates a link to the path on the documentation under the current version:

```
[A link](version /auth/getting-started) // to /docs/<version>/auth/getting-started
```

## Alerts

There is 3 types of alert, informational, warning and important:

```
> Informational
!> Warning
?> Error
```

## Headers

Any headers with either a double or triple hash will appear as linkable, and appear in the table of contents.

## Color

Wrapping text in color tags will wrap it in a span with the given hex code:

```
[color #fff]White Text[/color]
[color #000000]Black Text[/color]
```

## Config

Each version has a custom config file (`_config.yaml`) which is converted . The contents of which will be parsed and flattened. Within the markdown, adding a flattened dot-noted path wrapped in double curly braces will print out the config:

```
{
  android: {
    firebase: {
      core: '11.4.2',
    },
  },
}
```

```
{{ android.firebase.core }} // 11.4.2
```
