`AndroidAnnotations` works with `ProGuard`, and **you don't have any special adjustment to make** !

For those who do not already know how to enable `ProGuard`, here is a little tutorial.

## Enabling `ProGuard` ##

To enable `ProGuard`, you just have to set the following line in the `default.properties`.

```
proguard.config=proguard.cfg
```

## proguard.cfg ##

When you create an new Android project, the file `proguard.cfg` should be automatically generated, but sometimes it's not. You will find here the default content of this file. This content is usable with `ProGuard`.

```
-optimizationpasses 5
-dontusemixedcaseclassnames
-dontskipnonpubliclibraryclasses
-dontpreverify
-verbose
-optimizations !code/simplification/arithmetic,!field/ *,!class/merging/ *

-keep public class * extends android.app.Activity
-keep public class * extends android.app.Application
-keep public class * extends android.app.Service
-keep public class * extends android.content.BroadcastReceiver
-keep public class * extends android.content.ContentProvider
-keep public class * extends android.app.backup.BackupAgentHelper
-keep public class * extends android.preference.Preference
-keep public class com.android.vending.licensing.ILicensingService

-keepclasseswithmembernames class * {
    native <methods>;
}

-keepclasseswithmembernames class * {
    public <init>(android.content.Context, android.util.AttributeSet);
}

-keepclasseswithmembernames class * {
    public <init>(android.content.Context, android.util.AttributeSet, int);
}

-keepclassmembers enum * {
    public static **[] values();
    public static ** valueOf(java.lang.String);
}

-keep class * implements android.os.Parcelable {
  public static final android.os.Parcelable$Creator *;
}

```

## More informations ##
Sometimes, because of the using of some libraries or of some special classes, you need to configure a bit more the behaviour of `ProGuard`. You will find below some useful links :

http://developer.android.com/guide/developing/tools/proguard.html

http://proguard.sourceforge.net