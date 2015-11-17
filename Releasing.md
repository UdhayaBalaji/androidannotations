# Introduction #

This page is addressed at `AndroidAnnotations` developers. It documents the steps that should be followed when creating a new `AndroidAnnotations` release.

# Needed software and configuration #

  * Install [Maven](http://maven.apache.org/download.html)
  * Add the user informations to your Settings.xml
```
<?xml version="1.0" encoding="UTF-8"?>
<settings xmlns="http://maven.apache.org/SETTINGS/1.0.0"
  xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="http://maven.apache.org/SETTINGS/1.0.0
  http://maven.apache.org/xsd/settings-1.0.0.xsd">
  <servers>
    <server>
      <id>sonatype-nexus-snapshots</id>
      <username>USERNAME</username>
      <password>PASSWORD</password>
    </server>
    <server>
      <id>sonatype-nexus-staging</id>
      <username>USERNAME</username>
      <password>PASSWORD</password>
    </server>
  </servers>
</settings>
```

# Releasing #

  * To create a new release, simply enter the following commands, after replacing `<release-ver>` (e.g. **2.0**) and `<next-dev-ver>` (e.g **2.1**) with the good values.
```
git checkout develop
git pull
git checkout -b release/<release-ver>
mvn clean release:prepare -DdevelopmentVersion=<next-ver> -DreleaseVersion=<release-ver> -Dtag=androidannotations-<release-ver>
mvn release:perform
git checkout master
git merge --no-ff androidannotations-<release-ver>
git checkout develop
git merge --no-ff release/<release-ver>
git push origin master develop
git branch -d release/<release-ver>
git push origin :release/<release-ver>
```

Then you need to close and release the staging repository on [Sonatype Nexus OSS](https://oss.sonatype.org/index.html). Once done, it will be synced to Maven Central a few hours later.

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

The snapshot should be available in the **snapshots** Maven [repository](http://repository.excilys.com/content/repositories/snapshots).

# Deploying a new frozen version of `CodeModel` #
The following conf is needed in settings.xml:
```
    <server>
      <id>excilys-thirdparty</id>
      <username>USERNAME</username>
      <password>PASSWORD</password>
    </server>
```
The following command line deploys all artifacts.
```
mvn deploy:deploy-file -Dfile=/home/pyricau/.m2/repository/com/sun/codemodel/codemodel/2.5-SNAPSHOT/codemodel-2.5-SNAPSHOT-sources.jar -Dversion=2.5-FROZEN-AA -Durl=http://repository.excilys.com/content/repositories/thirdparty -DrepositoryId=excilys-thirdparty -DgroupId=com.sun.codemodel -DartifactId=codemodel -Dpackaging=jar -Dclassifier=sources
```


# Releasing a bugfix version #
  * Create a hotfix branch from master
```
git flow hotfix start <previous-release>
```
  * Make the required changes
  * Run `mvn license:check` to check the license headers
  * Commit the needed changes
  * If you want to deploy a hotfix snapshot, update the version number to be a hotfix snapshot version number
```
mvn versions:set -DnewVersion=2.1.1-SNAPSHOT -DgenerateBackupPoms=false
```
  * Create a new hotfix release
```
mvn clean release:prepare --batch-mode -DdevelopmentVersion=<develop-version>-SNAPSHOT -DreleaseVersion=<hotfix-ver> -Dtag=androidannotations-<hotfix-ver>
mvn release:perform
```
  * Merge hotfix back on master
```
git flow hotfix finish <previous-release>
```
  * Merge the changes back on develop
```
git checkout develop
git merge--no-ff hotfix/<hotfix-ver>
```
  * Push the whole thing
```
git push && git push --tags 
```