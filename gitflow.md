Gitflow
=======
Thanks to Daniel Kummer: http://danielkummer.github.io/git-flow-cheatsheet/


# Workflow: Release Sequence #
```
#!bat

git checkout master
git pull origin master
git merge develop

:: Run Build
:: Archive Build
:: Distribute Build

git push origin master
git checkout develop

```

# Workflow: Hotfix Sequence #
```
#!bat

:: Create the hotfix branch and change to that branch

git checkout master
git pull origin master
git checkout -b hotfix-v.2.00.003 master
```
 
(fix the code)
 

```
#!bat

:: Merge to the master branch
git checkout master
git pull origin master
git merge --no-ff hotfix-v.2.00.003
git tag -m "hotfix-v.2.00.003" -a v.2.00.003
git push origin master
```
 

```
#!bat

:: Merge to the develop branch

git checkout develop
git pull origin develop
git merge --no-ff hotfix-v.2.00.003
git push origin develop
```
 

```
#!bat

:: Delete hotfix branch(es)

git branch -D hotfix-v.2.00.003
git push origin --delete hotfix-v.2.00.003
```
