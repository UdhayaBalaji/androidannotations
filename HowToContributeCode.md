# Contributing is not a crime #

`AndroidAnnotations` greatly welcomes any contribution. Here is a small guide on how to contribute code, such as **bug fixes**, new **features**, **javadoc** or refactoring.

You should provide contributions by pushing changes on a clone of the git repository, and letting us know by creating a new issue.

## General Steps ##

  * Go [here](http://code.google.com/p/androidannotations/source/clones) and click on **Create a clone**
  * Create a local clone of your remote clone of `AndroidAnnotations`, create a branch based on the **develop** branch, commit some code on this branch, and push it on your remote clone.
  * Your branch names must start with the issue number. The branch name should not contain the developer name, it should only contain the id of the issue and a meaningful name. For instance: **123\_fragment\_support**.
  * Do not include in your commit message anything related to automatic issue closing, such as **Fixes [issue 113](https://code.google.com/p/androidannotations/issues/detail?id=113)**. We'll do that when merging to **develop**.
  * Create a [new issue](http://code.google.com/p/androidannotations/issues/entry) or contribute to an [existing one](http://code.google.com/p/androidannotations/issues/list), letting us know the branch that should be integrated back in `AndroidAnnotations`. This is the equivalent of a GitHub Pull Request.

## Checklist for contributed code ##

  * All files should have an [apache 2 license](http://www.apache.org/licenses/LICENSE-2.0) header. To do so, simply run this command in the `AndroidAnnotations` parent project :

```
mvn license:format
```

  * You may add an @author comment to any class you have contributed to, as well as the usual Javadoc comments of course.
```
/**
 * This class handles the blah blah blah
 * @author Pierre-Yves Ricau
 */
public class MyClass {
[...]
```

## Merging a pull request ##

Update the local **develop** branch
```
git checkout develop
git pull
```

### If the branch is on a clone ###

Add a remote if not already done
```
git remote add xxxclone https://code.google.com/r/xxx-clone/
```

Fetch its latest changes
```
git fetch xxxclone
```

Merge the branch on your local develop
```
git merge xxxclone/xxxbranch
```

### If the branch is on the main repository ###

Merge the branch on your local develop
```
git merge origin/xxxbranch
```

### Check and push ###

Check and test the code changes, verify that AndroidAnnotations still builds :

```
mvn clean package
```

Check that the license headers are set :

```
mvn license:check
```

Deploy a new snapshot
```
mvn clean deploy
```

If anything went wrong, you can remove the merge commit :

```
git reset HEAD^1
```

Edit the merge message to add issue closing information (e.g. Fixes [issue 113](https://code.google.com/p/androidannotations/issues/detail?id=113)).
```
git commit --amend --allow-empty
```

Remove the remote branch

```
git push origin :xxxbranch
```