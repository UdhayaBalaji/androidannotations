**This page has been deprecated after migrating from SVN to Git. However, we'll keep it here as it contains useful information.**


# Introduction #

This page is addressed at `AndroidAnnotations` developers. It documents the steps that should be followed when creating a new `AndroidAnnotations` release.

# Needed software and configuration #

  * Install [Maven](http://maven.apache.org/download.html)
  * Configure [Subversion](http://subversion.apache.org) to automatically add the file mime types as svn properties (used when uploading the Javadoc). To do so, edit ~/.subversion/config and add the following properties:
```
enable-auto-props = yes

### Section for configuring automatic properties.
[auto-props]
*.png = svn:mime-type=image/png
*.jpg = svn:mime-type=image/jpeg
*.gif = svn:mime-type=application/octet-stream
*.xml = svn:eol-style=native;svn:mime-type=text/xml
*.css = svn:eol-style=native;svn:mime-type=text/css
*.js = svn:eol-style=native;svn:mime-type=text/javascript
*.sql = svn:eol-style=native;svn:mime-type=text/plain
*.txt = svn:eol-style=native;svn:mime-type=text/plain
*.html = svn:eol-style=native;svn:mime-type=text/html
*.properties = svn:eol-style=native;svn:mime-type=text/plain
*.php = svn:eol-style=native;svn:mime-type=text/plain
*.tpl = svn:eol-style=native;svn:mime-type=text/html
*.ptpl = svn:eol-style=native;svn:mime-type=text/plain
```

If you are using Eclipse/Subversive, go to menu Window/Preferences/Team/SVN/Properties Configuration/Automatic Properties, remove all existing items and import [this file](http://acra.googlecode.com/svn/wiki/files/svn-mimetypes.conf).

_This procedure is merely a [copy & paste](http://code.google.com/p/maven-googlecode-plugin/wiki/MavenSiteDeployOnSVN)._

  * Add the scm user informations to your Settings.xml
```
<?xml version="1.0" encoding="UTF-8"?>
<settings xmlns="http://maven.apache.org/SETTINGS/1.0.0"
  xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="http://maven.apache.org/SETTINGS/1.0.0
  http://maven.apache.org/xsd/settings-1.0.0.xsd">
  <servers>
    <server>
      <id>androidannotations-googlecode</id>
      <username>YOUR_GOOGLE_CODE_USERNAME</username>
      <password>YOUR_GOOGLE_CODE_PASSWORD</password>
    </server>
  </servers>
</settings>
```

  * Configure subversion to accept google certificate :

```
nano ~/.subversion/servers
ssl-authority-files = /path/to/AndroidAnnotations/google.pem
```

# Releasing #

  * To create a new release, simply enter the following commands, after replacing `<release-ver>` (e.g. **2.0**) and `<next-dev-ver>` (e.g **2.1**) with the good values.
```
mkdir release
cd release
svn checkout https://androidannotations.googlecode.com/svn/trunk/AndroidAnnotations .
mvn release:prepare --batch-mode -DdevelopmentVersion=<next-dev-ver>-SNAPSHOT -DreleaseVersion=<release-ver> -Dtag=androidannotations-<release-ver>
# To cancel the release after prepare, you may use "mvn release:rollback".
mvn release:perform
svn mkdir https://androidannotations.googlecode.com/svn/javadoc/<release-ver> -m "Creating Javadoc folder for version <release-ver>"
svn checkout https://androidannotations.googlecode.com/svn/javadoc/<release-ver>
cp -r target/checkout/target/apidocs/* <release-ver>
cd <release-ver>
svn add . --force
svn commit -m "Uploading Javadocs for version <release-ver>"
cd ../..
rm -rf release
```

# After releasing #

  * Update the HelloWorldEclipse project with the new `AndroidAnnotation` snapshot version number : In project properties, fix build path and annotation processing factory path.
  * Update the `RoboGuiceExample` project with the new `AndroidAnnotation` snapshot version number : In project properties, fix build path and annotation processing factory path.
  * Update the [download](Download.md) wiki page with the latest version number (2 places)
  * Update the [MavenEclipse](MavenEclipse.md) wiki page (maven conf + factory path)
  * Update the [release notes](ReleaseNotes.md) wiki page with this release notes (new features, bug fixes, etc)
  * Update the welcome page if necessary, from the "Administer" tab

# Deploying a snapshot #

You might want to deploy a snapshot, for instance to let users test a bugfix without having to create a stable release.

To do so, enter the following command :
```
mvn clean deploy
```

The snapshot should be available in the in the **snapshots** Maven [repository](http://androidannotations.googlecode.com/svn/repository/snapshots/com/googlecode/androidannotations/androidannotations/).

# Deploying a new frozen version of `CodeModel` #
```
 mvn deploy:deploy-file -Dfile=/home/pyricau/.m2/repository/com/sun/codemodel/codemodel/2.5-SNAPSHOT/codemodel-2.5-SNAPSHOT-sources.jar -Dversion=2.5-FROZEN-AA -Durl=file:///home/pyricau/projects/AndroidAnnotations/repository/repository/snapshots -DgroupId=com.sun.codemodel -DartifactId=codemodel -Dpackaging=jar -Dclassifier=sources
```