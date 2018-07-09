Gitflow
=======
Thanks to Daniel Kummer: http://danielkummer.github.io/git-flow-cheatsheet/

## Gitflow Setup
https://datasift.github.io/gitflow/IntroducingGitFlow.html

* Clone a copy of the remote origin repository and switch to the develop branch.
* cd /IVP
* git clone https://insidevaluation.unfuddle.com/git/insidevaluation_gitsourcecode/ work
* cd work
* git checkout develop
* Setup default exclusions.
* Open Visual Studio
* From the 'Git' menu, select 'Edit .gitignore'
* 'Add Default Ignores'
* Be sure that *.suo *.sln and *.csproj are included.
* 'Save'
* Set Visual Studio to use Git
* Set 'Tools->Options->Source Control->Plug-in Selection' to 'Git source control provider'
* Command-line Extensions
* If you have a P: drive mapped to a network user folder, you may want to:
* Create a 'p:\bin' folder and add it to your PATH env variable.
* Place the following commands in that folder to extend you command-line flexibility.
* e.bat (Edit a file from the command line.  Allows for editing files in the user folder using 'e ~\.gitignore' format.)
* clone.py (Allows the two types of clone used in GitFlow to be done easily.)

* Getting Started
* GitFlow Scripts
* GitFlow process explanation
* Release Process
* Hot-Fix Process
* Peer to Peer
* Feature Branch
* Reversion
* Reference

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
