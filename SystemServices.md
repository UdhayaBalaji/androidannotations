# `@SystemService` #

The **`@SystemService`** annotation indicates that an activity **field** should be injected with the corresponding Android **System service**. It is the same as calling the [getSystemService](http://developer.android.com/reference/android/content/Context.html#getSystemService%28java.lang.String%29) method.

The **field type** is used to determine which system service should be injected. The field must not be private.

Usage example:
```
@SystemService
NotificationManager notificationManager;
```

Equivalent boilerplate code:

```
NotificationManager notificationManager;

@Override
public void onCreate(Bundle savedInstanceState) {
    [...]
    notificationManager = (NotificationManager) getSystemService(Context.NOTIFICATION_SERVICE);
}
```