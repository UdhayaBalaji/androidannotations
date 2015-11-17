**This page is not up to date, the introduction of `CodeModel` to generate code removed the need to use Instruction classes.**

This page describes the process to follow when adding annotations and code generation :

  1. First, check the [How to contribute code](HowToContributeCode.md) wiki page
  1. Import the `AndroidAnnotations` project **and** the HelloWorldEclipse project. You'll need it to test your changes.
  1. Create a new annotation in the package `com.googlecode.androidannotations.annotations`. It should have a **source retention policy**. Example: [@EActivity](http://code.google.com/p/androidannotations/source/browse/AndroidAnnotations/androidannotations/src/main/java/com/googlecode/androidannotations/annotations/EActivity.java).
  1. Create a validator for your annotation, in the package `com.googlecode.androidannotations.validation`. It must implement [ElementValidator](http://code.google.com/p/androidannotations/source/browse/AndroidAnnotations/androidannotations/src/main/java/com/googlecode/androidannotations/validation/ElementValidator.java). It can extend [ValidatorHelper](http://code.google.com/p/androidannotations/source/browse/AndroidAnnotations/androidannotations/src/main/java/com/googlecode/androidannotations/helper/ValidatorHelper.java) which provides helper methods. Example: [ExtraValidator](http://code.google.com/p/androidannotations/source/browse/AndroidAnnotations/androidannotations/src/main/java/com/googlecode/androidannotations/validation/ExtraValidator.java).
  1. Create a source generator for your annotation, in the package `com.googlecode.androidannotations.generation`. It must implement [Instruction](http://code.google.com/p/androidannotations/source/browse/AndroidAnnotations/androidannotations/src/main/java/com/googlecode/androidannotations/model/Instruction.java). Example: [ValueInstruction](http://code.google.com/p/androidannotations/source/browse/AndroidAnnotations/androidannotations/src/main/java/com/googlecode/androidannotations/generation/ValueInstruction.java).
  1. Create a processor that will take validated elements, and create and add the corresponding instructions in the model, in the package `com.googlecode.androidannotations.processing`. It must implement [ElementProcessor](http://code.google.com/p/androidannotations/source/browse/AndroidAnnotations/androidannotations/src/main/java/com/googlecode/androidannotations/processing/ElementProcessor.java). Example: [ClickProcessor](http://code.google.com/p/androidannotations/source/browse/AndroidAnnotations/androidannotations/src/main/java/com/googlecode/androidannotations/processing/ClickProcessor.java).
  1. Bind everything in [AndroidAnnotationProcessor](http://code.google.com/p/androidannotations/source/browse/AndroidAnnotations/androidannotations/src/main/java/com/googlecode/androidannotations/AndroidAnnotationProcessor.java):
    1. Add your annotation to the [@SupportedAnnotationClasses](http://code.google.com/p/androidannotations/source/browse/AndroidAnnotations/androidannotations/src/main/java/com/googlecode/androidannotations/annotationprocessor/SupportedAnnotationClasses.java) class list at the top of the [AndroidAnnotationProcessor](http://code.google.com/p/androidannotations/source/browse/AndroidAnnotations/androidannotations/src/main/java/com/googlecode/androidannotations/AndroidAnnotationProcessor.java) class.
    1. Register your validator in the `buildModelValidator()` method.
    1. Register your processor in the `buildModelProcessor()` method.
  1. Test your new annotation with the HelloWorldEclipse project. Once you've configured everything, you only need to delete the `AndroidAnnotation` JAR in the target folder from Eclipse to see it automatically rebuilt and reloaded in HelloWorldEclipse.