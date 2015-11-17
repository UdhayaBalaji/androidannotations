# General Questions #

  * [Does AndroidAnnotations have any perf impact?](#Does_AndroidAnnotations_have_any_perf_impact?.md)

  * [Generating code ? Yuk! C'mon man, it's 2011!](#Generating_code_?_Yuk!_C%27mon_man,_it%27s_2011!.md)

  * [How do you compare to RoboGuice](#How_do_you_compare_to_?.md)

  * [Why generate subclasses instead of directly modifying the activities ?](#Why_generate_subclasses_instead_of_directly_modifying_the_activi.md)

# Technical Questions #

`AndroidAnnotations` not working? See the [Troubleshooting](Troubleshooting.md) guide.

  * [Warning / error related to AndroidManifest.xml, won't disappear?](#Warning_/_error_related_to_AndroidManifest.xml_won%27t_disapp.md)

  * ["XXX cannot be resolved or is not a field" error in the generated code](#%22XXX_cannot_be_resolved_or_is_not_a_field%22_error_in_th.md)

  * [Nothing gets generated](#Nothing_gets_generated.md)

  * [Can I use AndroidAnnotations in a Scala Android Project?](#Can_I_use_in_a_Scala_Android_Project?.md)

# General Answers #

## Does `AndroidAnnotations` have any perf impact? ##

Short answer: **no**. `AndroidAnnotations` has a little compilation overhead (see [how it works](HowItWorks.md)), but the generated classes are good old classic Android code. No **reflection**. No **startup** time, and no runtime impact.

## Generating code ? Yuk! C'mon man, it's 2011! ##
Some people will argue that generating code should be avoided as much as possible. Here are the reasons why I think it can still be a good idea:

  * Thanks to Java6's Annotation Processing Tool, the code is automatically generated each time you compile. Which means the generated code is **always up to date**.
  * Android does not (yet) provide quick reflection and dynamic code generation. Which means that we are currently have the choice with either **slow reflection**/Java dynamic proxies (limited to implementing interfaces), or generating code.
  * Most tools and IDEs **integrate seamlessly** with Java's Annotation Processing Tool : Maven, Ant, Eclipse, Netbeans...

↑[Back to top](#Questions.md)

## How do you compare to [RoboGuice](http://code.google.com/p/roboguice) ? ##

[RoboGuice](http://code.google.com/p/roboguice) is a great project that enables dependency injection on Android, using Guice. It also provides specific annotations that are very similar to  `AndroidAnnotations` ones (injection of views, etc).

However, `RoboGuice` read those annotations at **runtime**, and inject the fields using reflection, which may impact the runtime **performances**.

`AndroidAnnotations` generates the boilerplate code in subclasses at **compile time**, which obviously leads to **no runtime impact** on performances.

`AndroidAnnotations` and `RoboGuice` do not compete, but are rather complementary, depending on your needs. Actually, you can even use [both at the same time](RoboGuiceIntegration.md).

To be honest, I have used and contributed a [little bit](http://code.google.com/p/roboguice/people/list) to `RoboGuice`, which is why `AndroidAnnotations` usage looks similar.

↑[Back to top](#Questions.md)

## Why generate subclasses instead of directly modifying the activities ? ##
Because Java's Annotation Processing Tool does not allow code modification. The only exception to that rule is [project Lombok](http://projectlombok.org/), which is great but does not work with all Java compilers.

↑[Back to top](#Questions.md)

# Technical Answers #

## Warning / error related to `AndroidManifest.xml` won't disappear. ##

`AndroidAnnotations` is activated when you compile your classes. If an activity is annotated with @EActivity but not registered in your `AndroidManifest.xml`, a warning is added to the activity. When you fix your `AndroidManifest.xml`, the warning won't disappear: you have to recompile the class. This can be done in eclipse either by modifying the class and saving it, or by doing a "project > clean".

↑[Back to top](#Questions.md)

## "XXX cannot be resolved or is not a field" error in the generated code ##

The most probable cause to this error is the R class not being found by Eclipse, although `AndroidAnnotations` was able to access it at compile time. There seems to be a bug with the latest releases of the ADT plugin (especially on Mac), related to the generation of the R class.

To fix the error, try to do the following in Eclipse: "Project > Clean" and clean your Android project. Ensure that "Build automatically" is activated in Eclipse. Then, right click on your project, and hit "Refresh".

If it still does not work, please consider creating [an issue](http://code.google.com/p/androidannotations/issues/entry).

↑[Back to top](#Questions.md)

## Nothing gets generated ##

_I have followed the docs to configure Eclipse but nothing gets generated._

Be careful that you have used the good jar for annotation processing: androidannotations-X.X.X.jar, not androidannotations**-api**-X.X.X.jar.

See [issue 89](https://code.google.com/p/androidannotations/issues/detail?id=89) for details. If that doesn't solve your issue, please [create an issue](http://code.google.com/p/androidannotations/issues/list).

↑[Back to top](#Questions.md)

## Can I use AndroidAnnotations in a Scala Android Project? ##

AndroidAnnotations is a Java annotation processor, and Scala does not seem  doesn't seem to support the Java annotation processing tool. However, AndroidAnnotations may still be used in the Java source code in a Scala mixed-source project. See this [Stack Overflow question](http://stackoverflow.com/questions/7454018/using-androidannotations-with-scala-and-gradle) for more details.

↑[Back to top](#Questions.md)