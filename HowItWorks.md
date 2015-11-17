`AndroidAnnotations` works in a very simple way. It automatically adds an extra compilation step that generates source code, using the standard [Java Annotation Processing Tool](http://download.oracle.com/javase/6/docs/technotes/guides/apt/index.html).

What source code ? For each @EActivity annotated activity, a subclass of this activity is generated, with the same name plus an underscore appended at the end.

For instance, the following class:
```
package com.some.company;
@EActivity
public class MyActivity extends Activity {
[...]
```

Will generate the following subclass, in the same package but in another source folder:

```
package com.some.company;
public final class MyActivity_ extends MyActivity {
[...]
```

This subclass adds behavior to your activity by overriding some methods (for instance onCreate()), yet delegating the calls to super.

That is the reason why you must add "`_`" to your activity names in `AndroidManifest.xml`:
```
<activity android:name=".MyListActivity_" />
```

## Starting an annotated activity ##

In Android, you usually start an activity this way:
```
startActivity(this, MyListActivity.class);
```

However, with `AndroidAnnotations`, the real activity that must be started is `MyListActivity_`:
```
startActivity(this, MyListActivity_.class);
```

## Is there any performance impact? ##
The short answer is **no**. More on this subject in the [FAQ](FAQ#Does_AndroidAnnotations_have_any_perf_impact?.md).

Now that you get the basics, see how to bind the [layout & views](LayoutAndViews.md).