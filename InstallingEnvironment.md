# Introduction #

Developing an AnnotationProcessor is not something very common, but hopefully we went through many different bugs and solved them. We now have a quite stable and clean dev environment, so you should be able to contribute to AndroidAnnotations by following simple steps.

# Installing the environment #

  * Install [Git](http://git-scm.com/)
  * Install [Maven](http://maven.apache.org/download.html)
  * Install [Eclipse Indigo](http://www.eclipse.org/indigo/)
  * Install the [latest version](http://developer.android.com/sdk/installing.html) of the **Android SDK** and the **Android Eclipse Plugin** (ADT)
  * In Eclipse, go to Help > Install New Software, in Work with select **Indigo**, and tick **Collaboration >     m2e - Maven Integration for Eclipse**, click **Next**, accept and **Finish**. Restart Eclipse.
  * In Eclipse, go to Help > Eclipse Marketplace, search for _m2e-android_ and install **Android Configurator for M2E**

# Getting the sources #

  * Go [here](http://code.google.com/p/androidannotations/source/clones) and click on **Create a clone**
  * Follow the instructions on your clone page to checkout a local clone of the AndroidAnnotations project.
  * If you already have the rights to commit on AndroidAnnotations, you don't need to create a clone, you can use the [main repository](http://code.google.com/p/androidannotations/source/checkout).
  * Checkout the develop branch
```
git checkout develop
```

# Importing in Eclipse #

  * Go to File > Import > General > Existing Projects into Workspace, and import the **androidannotations-dependencies** project.
  * Go to File > Import > Maven >Existing Maven Projects, open the **AndroidAnnotations** folder and import all the projects (all the pom.xml filles).
  * Please note that you won't need the functional-test-1-5 and the rest-api-test-1-5 projects in this eclipse workspace, so you can remove them immediately after importing. However, we need to import them to benefit from the automatic discovery and installation of m2e plugin (namely, the connectors for the maven-android-plugin and the maven-jar-plugin).

  * In project androidannotations, open src/main, right click on **eclipse** and select **Build Path** > **Use as source folder**. Then open the build path configuration and add the eclipse core runtime plugin dependency to the build path.

  * Go to **Run > Run Configurations...** and double click on **Eclipse Application**, and click Run. Note : I encountered a problem with running Eclipse on a 32bits JVM [with a 64bits Mac](http://ysasaki600.wordpress.com/2009/09/19/week2-tutorial-for-eclipse-wtp/), which was simply solved by adding **-D32** to the VM arguments of the run configuration.
  * This new eclipse is launched on a new workspace.
  * Go to File > Import > Maven >Existing Maven Projects, open the **AndroidAnnotations** folder and import the **functional-test-1-5** (functional-test-1-5/pom.xml) and the **rest-api-test-1-5** projects (rest-api-test-1-5/pom.xml).
  * The generated classes are not there yet, so do a Project > Clean to let AndroidAnnotations generate them.
  * If you still have compilation errors on a project, claiming that the generated classes are missing, open the project  properties > Java compiler > Annotation Processing  and change the name of the Generated source directory. Click Apply, then change it back to **.apt\_generated** and apply again. You should be good to go, if not, then let us know ;-) .

# Running the functional tests #

**Select the**functional-test-1-5**then click on Run > Run Configurations... and double click on JUnit. Change the test runner to JUnit4. In the bottom part, select the Eclipse JUnit Runner.** Go to Classpath and click Advanced on the right. Select Add Folders, and select functional-test-1-5 > target > android-classes. Also add the folder functional-test-1-5 > bin > classes

Notes :

  * To start the tests, just run the previously created Run Configuration
  * You can start the "Eclipse application" in debug mode, and put breakpoints in your code. You will also benefit from hot replace of code (only inside methods)
  * To see your changes in the code, you have to restart the 2nd eclipse. We didn't find any better solution, but tell us if you do!