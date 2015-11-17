`AndroidAnnotations` fully integrates with [RoboGuice](http://code.google.com/p/roboguice/) 1.1.1.

_If you have any problems integrating `AndroidAnnotations` with versions of `RoboGuice` superior to 1.1.1, please [let us know](http://code.google.com/p/androidannotations/issues/list) so that we can fix any issue._

<a href='http://code.google.com/p/androidannotations/wiki/GettingStarted'><img src='http://androidannotations.googlecode.com/svn/trunk/logo.png' /></a>
<a href='http://code.google.com/p/roboguice/'><img width='100' height='100' src='http://roboguice.googlecode.com/files/roboguice.png' /></a>

## Integrating `RoboGuice` and `AndroidAnnotation` ##
  1. [Add AndroidAnnotations](GettingStarted.md) to your project.
  1. [Add RoboGuice](http://code.google.com/p/roboguice/wiki/Installation) to your project.
  1. Instead of having activities that inherit from `RoboActivity`, simply annotate them with `@RoboGuice`.
  1. Looking for a working example ? Have a look [RoboGuiceExample](http://code.google.com/p/androidannotations/source/browse/RoboGuiceExample)!
```
@EActivity(R.layout.main)
@RoboGuice({AstroListener.class, AnotherListener.class})
public class AstroGirl extends Activity {
	
	@ViewById
	EditText edit;
	
	@Inject
	GreetingService greetingService;
	
	@Click
	void button() {
		String name = edit.getText().toString();
		greetingService.greet(name);
	}
}
```
```
public class AstroListener {

        @Inject
        Context context;

        public void doSomethingOnResume(@Observes OnResumeEvent onResume) {
                Toast.makeText(context, "Activity has been resumed", Toast.LENGTH_LONG).show();
        }
}
```

## What are the advantages of using `RoboGuice` ? ##
[RoboGuice](http://code.google.com/p/roboguice/) brings the power of the [Guice framework](http://code.google.com/p/google-guice/) to your Android application. It means that you can benefit from dependency injection advantages : low coupling, higher maintainability. Furthermore, `RoboGuice` allow injection of Android components in any class (whereas `AndroidAnnotations` only works on activities).

## What are the advantages of using `AndroidAnnotations` ? ##
  * Compile time injection of Android components (=> no perf impact)
  * Extending `RoboActivity` is not needed any more. This basically mean that you can inherit from any activity class, even those not supported by `RoboGuice`. Think about it if you want to use other frameworks that require you to extends their own base activity class.
  * Support for @Click, @Background, `@UiThread`, `@UiThreadDelayed`, `@ItemSelected`, etc.