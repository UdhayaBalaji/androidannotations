# Introduction #

`AndroidAnnotations` bug fixes, snapshot deployments and new releases are automatically tweeted on the [@AndAnnotations](http://twitter.com/AndAnnotations) twitter account. To do so, we use [ifttt](http://ifttt.com), which means _if this then that_.

Quote from ifttt website:

> ifttt puts the internet to work for you by creating tasks that fit this simple structure: if **this** then **that**

> Think of all the things you could do if you were able to define any task as: when something happens (**this**) then do something else (**that**).

_If may have some invitations left, ask @Piwai on twitter if you want to try out this nice service._


# Details #

## Tweeting bug fixes ##

We look for the "Fixed" keyword in the updates feed, rather than the issues feed, because the generated entry title is more readable.

### Trigger ###
  * **Feed** > New feed item matches
  * Keyword: Fixed
  * Feed url: http://code.google.com/feeds/p/androidannotations/updates/basic

### Action ###
  * **Twitter** > Post a new tweet
  * Content: Fixed: {{`EntryTitle`}} {{`EntryUrl`}}

## Tweeting new snapshot deployments ##

Since the Maven snapshot repository is hosted on the Google Code svn, we can use the svnchanges feed on the repository snapshot path. The trick here is to look for a .zip keyword (when the assembly zip is uploaded).

### Trigger ###
  * **Feed** > New feed item matches
  * Keyword: .zip
  * Feed url: http://code.google.com/feeds/p/androidannotations/gitchanges/basic?repo=maven-snapshots

### Action ###
  * **Twitter** > Post a new tweet
  * Content: New `#AndroidAnnotations` snapshot deployed on the snapshot repository! {{`EntryUrl`}}

## Tweeting new releases ##

Since the Maven release repository is hosted on the Google Code svn, we can use the svnchanges feed on the repository release path. We look for a commit where the maven-metadata.xml file is updated, for the androidannotations artifactId.

### Trigger ###
  * **Feed** > New feed item matches
  * Keyword: com/googlecode/androidannotations/androidannotations/maven-metadata.xml
  * Feed url: http://code.google.com/feeds/p/androidannotations/gitchanges/basic?repo=maven-releases

### Action ###
  * **Twitter** > Post a new tweet
  * Content: A new release of `#AndroidAnnotations` has been deployed on the Maven repository! {{`EntryUrl`}} (Release Notes: http://goo.gl/3RtiM)