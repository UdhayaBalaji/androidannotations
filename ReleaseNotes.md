<a href='http://www.ebusinessinformation.fr'><img src='http://wiki.androidannotations.googlecode.com/git/providedbylogo.png' /></a>

Releases are available as [standalone jars](Download.md) or via [Maven](MavenEclipse.md).

_Items in **bold** are not backward compatible._

# Upcoming release: 2.3 #

_A snapshot is available on the [snapshot repository](https://oss.sonatype.org/content/repositories/snapshots)._

  * [Issue 147](https://code.google.com/p/androidannotations/issues/detail?id=147): Allow mocking of BackgroundExecutor to unit test @Background methods
  * [Issue 99](https://code.google.com/p/androidannotations/issues/detail?id=99): Enhancement and injection of any kind of class, thanks to @Enhanced, @Inject and @RootContext
  * [Issue 155](https://code.google.com/p/androidannotations/issues/detail?id=155) (evolving from [issue 143](https://code.google.com/p/androidannotations/issues/detail?id=143)): builders to start enhanced activities, taking extras into account

# Latest release: 2.2 #

Released on Dec 8, 2011

  * [Issue 93](https://code.google.com/p/androidannotations/issues/detail?id=93): **View binding & `@AfterViews` are executed every time setContentView is called**
  * [Issue 94](https://code.google.com/p/androidannotations/issues/detail?id=94): **Deploy `AndroidAnnotations` to Maven Central**
  * [Issue 102](https://code.google.com/p/androidannotations/issues/detail?id=102): **Rename pref.field().get(default) to getOr(default)**
  * [Issue 83](https://code.google.com/p/androidannotations/issues/detail?id=83): **@Click & friends with multiple id parameters**
  * [Issue 125](https://code.google.com/p/androidannotations/issues/detail?id=125): **Dropped support for Eclipse 3.4.X**
  * [Issue 55](https://code.google.com/p/androidannotations/issues/detail?id=55): Rest API using Spring Android.
  * [Issue 95](https://code.google.com/p/androidannotations/issues/detail?id=95): `@HtmlRes` & @FromHtml annotations to inject spanned html strings
  * [Issue 107](https://code.google.com/p/androidannotations/issues/detail?id=107): abstract annotated activities generate abstract activities instead of final activities
  * [Issue 111](https://code.google.com/p/androidannotations/issues/detail?id=111): Convention over configuration can now do "camel case => snake case" conversion.
  * [Issue 112](https://code.google.com/p/androidannotations/issues/detail?id=112): Adding Null checkers for view injection & binding
  * [Issue 41](https://code.google.com/p/androidannotations/issues/detail?id=41): Setting the dev project as an eclipse plugin, to ease development (hotreplace & debug)
  * [Issue 117](https://code.google.com/p/androidannotations/issues/detail?id=117) & [Issue 116](https://code.google.com/p/androidannotations/issues/detail?id=116) : More doc on how to develop AndroidAnnotations, and being able to run functional tests from eclipse
  * [Issue 113](https://code.google.com/p/androidannotations/issues/detail?id=113) & [issue 63](https://code.google.com/p/androidannotations/issues/detail?id=63): @EViewGroup (equivalent of @EActivity for ViewGroups)
  * [Issue 118](https://code.google.com/p/androidannotations/issues/detail?id=118): Pref are sometimes not generated / injected
  * [Issue 123](https://code.google.com/p/androidannotations/issues/detail?id=123): long not supported in prefs
  * [Issue 109](https://code.google.com/p/androidannotations/issues/detail?id=109), [Issue 126](https://code.google.com/p/androidannotations/issues/detail?id=126) & [Issue 128](https://code.google.com/p/androidannotations/issues/detail?id=128): Support for dozens of new types of Android Managers injection with @SystemService, even for API level 14 and even hidden system services (useful for custom Android builds).
  * [Issue 104](https://code.google.com/p/androidannotations/issues/detail?id=104): Support for @OptionsMenu and @OptionsItems
  * [Issue 127](https://code.google.com/p/androidannotations/issues/detail?id=127): @NoTitle and @Fullscreen on activities
  * [Issue 87](https://code.google.com/p/androidannotations/issues/detail?id=87): @Trace to trace methods and durations
  * [Issue 134](https://code.google.com/p/androidannotations/issues/detail?id=134): Exception in @Rest when using @Get without value
  * [Issue 137](https://code.google.com/p/androidannotations/issues/detail?id=137): Disable warning on @EActivity when the activity is abstract
  * [Issue 136](https://code.google.com/p/androidannotations/issues/detail?id=136): New tests for @ItemClick Annotation
  * [Issue 133](https://code.google.com/p/androidannotations/issues/detail?id=133): @EActivity on abstract classes generated errors when doing a clean build
  * [Issue 135](https://code.google.com/p/androidannotations/issues/detail?id=135): Support for "setRestTemplate()" in @Rest
  * [Issue 138](https://code.google.com/p/androidannotations/issues/detail?id=138): onCreate() visibility adapted in abstract activities

# 2.1.2 #

Released on Sep 17, 2011

_Bugfix release_

  * [Issue 103](https://code.google.com/p/androidannotations/issues/detail?id=103): @UiThread & @Background didn't work with generic parameters

# 2.1.1 #

Released on Sep 8, 2011

_Bugfix release_

  * [Issue 100](https://code.google.com/p/androidannotations/issues/detail?id=100): `@RoboGuice` doesn't work with `MapActivity`
  * [Issue 97](https://code.google.com/p/androidannotations/issues/detail?id=97): `AndroidAnnotations` releases failed at perform goal.

# 2.1 #

Released on Aug 29, 2011

  * [Issue 73](https://code.google.com/p/androidannotations/issues/detail?id=73): **View injection happens after onCreate() and before `@AfterViews` annotated methods**
  * [Issue 64](https://code.google.com/p/androidannotations/issues/detail?id=64): **The generated classes are now final.**
  * [Issue 91](https://code.google.com/p/androidannotations/issues/detail?id=91): **Switched Maven repository from Google Code to Excilys.** The new repository is [here](http://repository.excilys.com/content/repositories/releases/)
  * `BackgroundExecutor` is now part of the API package instead of being generated at compile time ([r858](https://code.google.com/p/androidannotations/source/detail?r=858)).
  * Added a compile scoped dependency on Android for `AndroidAnnotations`, which allows Javadoc links as well as including some classes in the API Jar ([r856](https://code.google.com/p/androidannotations/source/detail?r=856) and [r857](https://code.google.com/p/androidannotations/source/detail?r=857)).
  * [Issue 46](https://code.google.com/p/androidannotations/issues/detail?id=46): handling of [Activity.onBackPressed](http://developer.android.com/reference/android/app/Activity.html#onBackPressed%28%29) for pre ECLAIR (2.0) Android versions.
  * [Issue 47](https://code.google.com/p/androidannotations/issues/detail?id=47): Creating helpers for `SharedPreferences`
  * [Issue 49](https://code.google.com/p/androidannotations/issues/detail?id=49): Create an assembly Zip for releases
  * [Issue 51](https://code.google.com/p/androidannotations/issues/detail?id=51): Add automatic functional tests
  * Added NOTE messages at compile time to let the user know which files are generated. Can be viewed in Eclipse with the _Error log_ view. Done at [r976](https://code.google.com/p/androidannotations/source/detail?r=976).
  * [Issue 55](https://code.google.com/p/androidannotations/issues/detail?id=55): Partial implementation of a Rest API using Spring Android. Not officially supported yet.
  * [Issue 74](https://code.google.com/p/androidannotations/issues/detail?id=74): `InputMethodManager` service can not be injected
  * [Issue 69](https://code.google.com/p/androidannotations/issues/detail?id=69): `SensorManager` service can not be injected
  * [Issue 75](https://code.google.com/p/androidannotations/issues/detail?id=75): Using @Extra without value adds an additional unexpected compile error
  * [Issue 68](https://code.google.com/p/androidannotations/issues/detail?id=68): @Extra does not work with Generics
  * [Issue 70](https://code.google.com/p/androidannotations/issues/detail?id=70): @Extra does not work with Arrays
  * Added compiler notes when activities declared in the manifest are not found in the compile path. Done at [r1139](https://code.google.com/p/androidannotations/source/detail?r=1139).
  * [Issue 61](https://code.google.com/p/androidannotations/issues/detail?id=61): Inject Application with @App
  * [Issue 79](https://code.google.com/p/androidannotations/issues/detail?id=79): Add a license checker
  * [Issue 78](https://code.google.com/p/androidannotations/issues/detail?id=78): Switch source repository to Git
  * [Issue 88](https://code.google.com/p/androidannotations/issues/detail?id=88): `@AnimationRes` can now be used to inject Animation fields

# 2.0.2 #

_Bugfix release_

Released on Apr 13, 2011

  * [Issue 48](https://code.google.com/p/androidannotations/issues/detail?id=48): Unexpected warnings for registered activities that have a different package than the application package.

# 2.0.1 #

_Bugfix release_

Released on Apr 9, 2011

  * [Issue 42](https://code.google.com/p/androidannotations/issues/detail?id=42): `AndroidAnnotations` could not find the `AndroidManifest.xml` file if there was a space in the project path.

# 2.0 #

Released on Apr 6, 2011

The version number went from **1.0.3** to **2.0** because we made some API changes that are not backward compatible (@EActivity, startActivity`*` methods), and because a whole part of the internals has been rewritten (i.e. code generation).

  * [Issue 7](https://code.google.com/p/androidannotations/issues/detail?id=7): Code generation using [CodeModel](http://codemodel.java.net/) instead of Strings
  * [Issue 37](https://code.google.com/p/androidannotations/issues/detail?id=37): Created a [sample project](http://code.google.com/p/androidannotations/source/browse/trunk/maveneclipse) to show how to integrate Maven and `AndroidAnnotations`. Also created a dedicated [wiki page](MavenEclipse.md).
  * [Issue 27](https://code.google.com/p/androidannotations/issues/detail?id=27): **Removed overriding of startActivity`*`() methods. One cannot anymore start an enhanced activity without using the generated name (ie `MyActivity`**`_`**).**
  * Better stack trace printing of compile time unexpected exceptions.
  * [Issue 36](https://code.google.com/p/androidannotations/issues/detail?id=36): **Created a [snapshots](http://androidannotations.googlecode.com/svn/repository/snapshots/) and a [releases](http://androidannotations.googlecode.com/svn/repository/releases/) Maven repository, instead of a common repository. The old repository is still available for previous releases.**
  * Activities do not need any more to be in the same package as the R class (we read the `AndroidManifest.xml` to determine the R class package)
  * [Issue 29](https://code.google.com/p/androidannotations/issues/detail?id=29): Added online [Javadoc](http://androidannotations.googlecode.com/svn/javadoc/2.0/index.html)
  * [Issue 39](https://code.google.com/p/androidannotations/issues/detail?id=39): Removed compile errors on class members when @EActivity is available but has compile errors.
  * [Issue 34](https://code.google.com/p/androidannotations/issues/detail?id=34): **Compile errors are issued when @EActivity annotated activities are not registered in the `AndroidManifest.xml` file.**
  * [Issue 4](https://code.google.com/p/androidannotations/issues/detail?id=4): Using a shared executor service instead of creating a new thread each time an @Background method is called.
  * [Issue 35](https://code.google.com/p/androidannotations/issues/detail?id=35): **Renamed @Enhance to @EActivity.**
  * Global improvements based on the Hibernate Metamodel Generator (which is an annotation processor).

Bug fixes:
  * [Issue 26](https://code.google.com/p/androidannotations/issues/detail?id=26): RClassFinder returned null when the r class was not found, which led to NPE in CoumpoundRClass at compile time instead of a clear error message.
  * Compile time bug when an `@ItemSelect` method had no parameter (the generated code did not compile)
  * @Transactional overridden method did not call through super (Stack overflow)


_**Pre 2.0** releases are available on the old [Maven repository](http://androidannotations.googlecode.com/svn/repository/com/googlecode/androidannotations/androidannotations/)._

# 1.0.3 #

Released on Mar 17, 2011

  * Fixed [issue 25](https://code.google.com/p/androidannotations/issues/detail?id=25): Missing View import when using `@RoboGuice` without some other annotations.
  * Removed an unused @Inject import in some cases

# 1.0.2 #

Released on Mar 13, 2011

  * [Issue 22](https://code.google.com/p/androidannotations/issues/detail?id=22): **Support for `RoboGuice` 1.1.1, removed support for `RoboGuice` 1.0 and 1.1 (too much hassle). `RoboGuice` 1.1.1 bug fixes have been successfully backported to `AndroidAnnotations`.**
  * [Issue 24](https://code.google.com/p/androidannotations/issues/detail?id=24): **synchronized keyword is not allowed anymore on `@UiThread` and @Background methods.**
  * [Issue 21](https://code.google.com/p/androidannotations/issues/detail?id=21): Created a thin API JAR that should be included in the build path instead of the whole preprocessor JAR. `AndroidAnnotations` has a much smaller footprint !

# 1.0.1 #

Released on Jan 25, 2011

  * Retrofitted a bug fix from `RoboGuice` ([r557](https://code.google.com/p/androidannotations/source/detail?r=557))

# 1.0 #

Released on Jan 25, 2011

  * [Issue 17](https://code.google.com/p/androidannotations/issues/detail?id=17): support for `RoboGuice` 1.0 and 1.1. Event listeners (`RoboGuice 1.1`) are supported as well.
  * [Issue 18](https://code.google.com/p/androidannotations/issues/detail?id=18): **injection happens before `@BeforeCreate` method calls (except view injection of course)**
  * [Issue 2](https://code.google.com/p/androidannotations/issues/detail?id=2): **@Click and other listener methods cannot be used twice for the same id**
  * Improved javadocs
  * Improved code generation, with support for imports
  * @Enhance annotated classes may now be abstract (useful with `RoboGuice` : you can let your activity implement `InjectorProvider` and call the getInjector method, which will be implemented in the generated subclass)

# 1.0-RC4 #

Released on Jan 17, 2011

  * [Issue 11](https://code.google.com/p/androidannotations/issues/detail?id=11): overriding more startActivity`*`() methods
  * [Issue 12](https://code.google.com/p/androidannotations/issues/detail?id=12): **@Extra throws NPE when extra not set**
  * [Issue 13](https://code.google.com/p/androidannotations/issues/detail?id=13): Support for `@BeforeCreate`
  * **Renamed @Layout to @Enhance**
  * [Issue 10](https://code.google.com/p/androidannotations/issues/detail?id=10): remove the need for @Layout

# 1.0-RC3 #

Released on Jan 9, 2011

  * Support for integrating with [RoboGuice](http://code.google.com/p/roboguice/)

# 1.0-RC2 #
Released on Jan 6, 2011
  * android.R support
  * @Transactional
  * Events : `@LongClick`, `@ItemClick`, `@ItemSelect`, `@LongItemClick`, @Touch
  * method names for events can have a specific suffix (myButtonClicked, myButtonSelected)
  * **constraints on event methods: no exception allowed**

# 1.0-RC1 #

Released on Jan 5, 2011

  * Support for `@UiThreadDelayed`
  * Enough wiki documentation to easily get started and discover all the use cases
  * Added exception handling to `@UiThread` and @Background

# 0.5 #

Released on Jan 4, 2011

  * Support for @Extra, `@SystemService`, all @XXXRes (replacing @XXXValue)
  * startActivity is now overriden to replace `MyActivity` with `MyActivity_` in Intents

# 0.4 #

Released on Jan 4, 2011

  * Support for `@Background` and `@UiThread`
  * @Value is replaced by `@StringArrayValue`, `@ColorValue` and `@StringResValue` (will be necessary to support more values)

# 0.3 #

Released on Dec 22, 2010

  * **Replaced `@UiView` with `@ViewById`**
  * **Added more constraints : private modifier not allowed**
  * Support for @Value on Strings, String arrays and colors