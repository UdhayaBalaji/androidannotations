  * We now use the **functional-test-1-5** project to test functional changes. It uses Robolectric, which enables functional tests without having to start an emulator.

# Instructions #

`HelloWorldEclipse` is mainly used as a test project to develop new features on `AndroidAnnotations`. Therefore, it should not be imported as a standalone project.

  * Checkout `AndroidAnnotations` : http://code.google.com/p/androidannotations/source/checkout
  * Run "mvn package" to create the jar in the target folder of the `AndroidAnnotations` project
  * Import the `AndroidAnnotations` project into Eclipse, as a Maven project (using [M2Eclipse](http://m2eclipse.sonatype.org/installing-m2eclipse.html))
  * Import the `HelloWorldEclipse` project into Eclipse.