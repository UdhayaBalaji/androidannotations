# @Extra #

The **@Extra** annotation indicates that an activity **field** should be injected with the corresponding [Extra](http://developer.android.com/reference/android/content/Intent.html#getExtras%28%29) from the **intent** that was used to start the activity.

The extra key **must** be set in the annotation parameter, ie `@Extra("someExtraKey")`.

The field must not be private. The extra can be of any type.

Usage example:
```
@Extra("my_string_extra")
String myMessage;
	
@Extra("my_date_extra")
Date myDateExtraWithDefaultValue = new Date();
```

Equivalent boilerplate code:

```
String myMessage;
	
Date myDateExtraWithDefaultValue = new Date();

@Override
public void onCreate(Bundle savedInstanceState) {
    [...]
    Intent intent = getIntent();
    Bundle extras = intent.getExtras();

    if (extras.containsKey("my_string_extra")) {
        try {
            myMessage = (String) extras.get("my_string_extra");
        } catch (ClassCastException e) {
            Log.e(TAG, "Could not cast extra to expected type, the field is left to its default value", e);
        }
    }

    if (extras.containsKey("my_date_extra")) {
        try {
            myDateExtraWithDefaultValue = (Date) extras.get("my_date_extra");
        } catch (ClassCastException e) {
            Log.e(TAG, "Could not cast extra to expected type, the field is left to its default value", e);
        }
    }
}
```