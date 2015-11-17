This page has been deprecated after migrating from SVN to Git. However, we'll keep it here as it contains useful information.

# Contributing is not a crime #

`AndroidAnnotations` greatly welcomes any contribution. Here is a small guide on how to contribute code, such as bug fixes, new functionalities, javadoc or refactoring.

You should provide contributions through svn patches.

## Creating a svn patch ##

  * Checkout the `AndroidAnnotations` svn
```
svn checkout https://androidannotations.googlecode.com/svn/trunk/ .
```

  * Import the HelloWorldEclipse project, to be able to test your changes.

  * Make your changes

  * Update the `AndroidAnnotations` svn (so that your patch works with the latest code base)
```
svn update
```

  * Create a patch file
```
svn diff > my_patch.diff
```

## Sending a patch ##

  * Create a [new issue](http://code.google.com/p/androidannotations/issues/entry) or contribute to an [existing one](http://code.google.com/p/androidannotations/issues/list)

  * Click on the "Attach a file" link and send the patch

## Checklist for contributed code ##

  * All files should have an [apache 2 license](http://www.apache.org/licenses/LICENSE-2.0) header. Here is an example:
```
/*
 * Copyright 2010-2011 Pierre-Yves Ricau (py.ricau at gmail.com)
 *
 * Licensed under the Apache License, Version 2.0 (the "License"); you may not
 * use this file except in compliance with the License. You may obtain a copy of
 * the License at
 *
 * http://www.apache.org/licenses/LICENSE-2.0
 *
 * Unless required by applicable law or agreed to in writing, software
 * distributed under the License is distributed on an "AS IS" BASIS, WITHOUT
 * WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied. See the
 * License for the specific language governing permissions and limitations under
 * the License.
 */
```

  * You should add an @author comment to any class you have contributed to, as well as the usual Javadoc comments of course.
```
/**
 * This class handles the blah blah blah
 * @author Pierre-Yves Ricau
 */
public class MyClass {
[...]
```

## Integrating a patch ##

Once you have svn access, you can contribute your own patches, but you can also integrate patches from other contributors. Here is how:

  * Update the `AndroidAnnotations` svn (so that your patch works with the latest code base)
```
svn update
```

  * Apply the patch
```
patch -p0 -i my_patch.diff
```

  * Check that the code works (test test test), check the "Checklist for contributed code".

  * Commit, using a specific message that names the contributing author and closes the related issue (add a line that contains "fixes issue X"). Example:
```
svn commit -m "Integrating patch contributed by py.ricau for issue 42
Add support for a new @Dummy annotation
fixes issue 42
"
```