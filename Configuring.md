Once you have [downloaded](Download.md) `AndroidAnnotations`, you may add it to your projects.

_Annotation processing is not well implemented on Eclipse **3.4.X**. Please use at least Eclipse **3.5**._

_If you use **Maven** in your Android projects, please follow the [Maven + Eclipse](MavenEclipse.md) instructions instead._

# Configuring Eclipse #

Do the following to use `AndroidAnnotations` within the Eclipse IDE:

  * Right-click your project, choose "Properties"
  * Go to "Java Compiler" and make sure that "Compiler compliance level" is set to "1.6", otherwise the processor won't be activated
  * Go to "Java Compiler - Annotation Processing" and choose "Enable annotation processing"
  * Go to "Java Compiler - Annotation Processing - Factory Path" and add the processor JAR : [androidannotations-X.X.X.jar](Download.md)
  * Go to "Java Build Path - Libraries" and add the API JAR : [androidannotations-X.X.X-api.jar](Download.md)
  * Confirm the workspace rebuild
  * You can [start using](FirstActivity.md) `AndroidAnnotations` and you should now see any annotation problems as regular error markers within the editor and in the _Problem_ view.

---

This documentation is highly inspired (not to say c&p) from the [Hibernate Validation Annotation Processor](http://docs.jboss.org/hibernate/validator/4.1/reference/en-US/html/ch08.html). If you do not use Eclipse, you will find it quite helpful.