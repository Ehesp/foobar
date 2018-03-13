# AndroidPriority

```
firebase.notifications.Android.Priority
```

## Constants

### Default

Default notification priority for `setPriority`. If your application does not prioritise its own notifications, use this value for all notifications.

```
firebase.notifications.Android.Priority.Default
```

### High

Higher notification priority for `setPriority`, for more important notifications or alerts. The UI may choose to show these items larger, or at a different position in notification lists, compared with your app's `Priority.Default` items.

```
firebase.notifications.Android.Priority.High
```

### Low

Lower notification priority for `setPriority`, for items that are less important. The UI may choose to show these items smaller, or at a different position in the list, compared with your app's `Priority.Default` items.
    
```
firebase.notifications.Android.Priority.Low
```

### Max

Highest notification priority for `setPriority`, for your application's most important items that require the user's prompt attention or input.
    
```
firebase.notifications.Android.Priority.Max
```

### Min

Lowest notification priority for `setPriority`; these items might not be shown to the user except under special circumstances, such as detailed notification logs.
    
```
firebase.notifications.Android.Priority.Min
```