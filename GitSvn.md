**This page is now useless for `AndroidAnnotations`, since we do not use svn anymore. However, I'll keep it here just as a reminder ;-)**



This page is more of a reminder than a real doc page.

# Initial import #

Create the git svn repo
```
git svn clone --stdlayout https://androidannotations.googlecode.com/svn AndroidAnnotations
```

# Bugfixes after releases #

Checkout the release tag
```
git checkout tags/androidannotations-2.0.1
```

Create a remote svn branch
```
git svn branch -m "Branch to fix issue 48 on 2.0.1 release" 2.0.1-bugfix-48
```

Create a local branch tracking the remote branch
```
git checkout -b local/2.0.1-bugfix-48 2.0.1-bugfix-48
```

Pick a bug fix that was done on another branch
```
git cherry-pick 60125f9fbc3003eb6acbafabcfb682f7e5229862
```

Eventually edit the commit message
```
git commit --amend
```

Edit the project version and svn url in the pom.xml.

Push your changes
```
git svn dcommit
```

Then follow the standard [release procedure](Releasing.md).