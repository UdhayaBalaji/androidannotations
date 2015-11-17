Looking for a working example? See [this project](http://code.google.com/p/androidannotations/source/browse/maveneclipse).

# Create / import a project #

Follow the [GettingStarted](http://code.google.com/a/eclipselabs.org/p/m2eclipse-android-integration/wiki/GettingStarted) page of the m2eclipse-android-integration plugin to create / import your project as a Maven+Android project.

# POM configuration #
The **pom.xml** configuration is quite straightforward.

As well as the following dependencies:

```
<dependencies>
        <!-- [...] -->
	<dependency>
		<groupId>com.googlecode.androidannotations</groupId>
		<artifactId>androidannotations</artifactId>
		<version>2.2</version>
		<scope>provided</scope>
	</dependency>
	<dependency>
		<groupId>com.googlecode.androidannotations</groupId>
		<artifactId>androidannotations</artifactId>
		<classifier>api</classifier>
		<version>2.2</version>
	</dependency>
</dependencies>
```

Make sure your project is built with Java 1.6:

```
<build>
	<plugins>
		<!-- [...] -->
		<plugin>
			<artifactId>maven-compiler-plugin</artifactId>
			<version>2.3.2</version>
			<configuration>
				<source>1.6</source>
				<target>1.6</target>
			</configuration>
		</plugin>
	</plugins>
</build>
```

# Eclipse configuration #
The previous configuration enables `AndroidAnnotations` usage from the command line (e.g using `mvn package`). However, since Eclipse uses its own compiler, you'll need to configure it to use too.

The steps are quite simple though:

  * Right-click your project, choose **Properties**
  * Go to **Java Compiler - Annotation Processing** and choose **Enable annotation processing**
  * Go to **Java Compiler - Annotation Processing - Factory Path**, click on **Add Variable**, select on **M2\_REPO** and click on **Extend...** and select the following JAR : **com/googlecode/androidannotations/androidannotations/2.2/androidannotations-2.2.jar**
  * Confirm the workspace rebuild

Done!

The previous manual configuration can also be created by adding the following files at the root of your project:

**.factorypath**
```
<factorypath>
    <factorypathentry kind="PLUGIN" id="org.eclipse.jst.ws.annotations.core" enabled="true" runInBatchMode="false"/>
    <factorypathentry kind="VARJAR" id="M2_REPO/com/googlecode/androidannotations/androidannotations/2.2/androidannotations-2.2.jar" enabled="true" runInBatchMode="false"/>
</factorypath>
```

**.settings/org.eclipse.jdt.apt.core.prefs**
```
eclipse.preferences.version=1
org.eclipse.jdt.apt.aptEnabled=true
org.eclipse.jdt.apt.genSrcDir=.apt_generated
org.eclipse.jdt.apt.reconcileEnabled=true
```

# Snapshots #

_If you want to use snapshot versions of AndroidAnnotations, you should configure your project with the snapshot repository:_

```
<repositories>
	<repository>
		<id>snapshots-repository</id>
		<name>Sonatype oss snapshot repo</name>
		<url>https://oss.sonatype.org/content/repositories/snapshots</url>
	</repository>
</repositories>
```

## When using a central company repository ##

Some companies use a central nexus repository that works as a cache, so that all artifacts are download from this repository to accelerate artifact download. Usually, you will find the following configuration in settings.xml :

```
<settings>
       <mirrors>
               <mirror>
                       <id>internal-repo</id>
                       <name>Maven 2 Repository</name>
                       <url>http://maven.mycompany.com/content/groups/mycompany</url>
                       <mirrorOf>*</mirrorOf>
               </mirror>
       </mirrors>
<!-- ... -->
</settings>
```

If you don't have access to the configuration of this repository to add `AndroidAnnotations`' repository, or if it takes time, don't panic, and change your settings.xml to match the following configuration :
```
<settings>
       <mirrors>
               <mirror>
                       <id>internal-repo</id>
                       <name>Maven 2 Repository</name>
                       <url>http://maven.mycompany.com/content/groups/mycompany</url>
                       <mirrorOf>*,!snapshots-repository</mirrorOf>
               </mirror>
       </mirrors>
       <profiles>
               <profile>
                       <id>AndroidAnnotationsRepository</id>
                       <activation>
                               <activeByDefault>true</activeByDefault>
                       </activation>
                       <repositories>
				<repository>
					<id>snapshots-repository</id>
					<name>Sonatype oss snapshot repo</name>
					<url>https://oss.sonatype.org/content/repositories/snapshots</url>
				</repository>
                       </repositories>
               </profile>
       </profiles>
</settings>
```
The key setting here is **`<mirrorOf>*,!snapshots-repository</mirrorOf>`**, it says : "download everything from the central repository, except artifacts coming from the `AndroidAnnotations` repository".