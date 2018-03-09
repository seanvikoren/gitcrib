gitcrib
======================
My personal disorganized set of reminders on how to get things done in git.


Thank You: http://danielkummer.github.io/git-flow-cheatsheet/

Undo git add
```
git reset
```

Setup

```
#!bat

:: Windows Editor Setup
git config --global core.editor '"C:/Program Files (x86)/Notepad++/notepad++.exe"'

:: Mac Editor Setup
ln -s "/Applications/Sublime Text 2.app/Contents/SharedSupport/bin/subl" ~/bin/subl
export EDITOR='subl -w'
git config --global core.editor "subl -n -w"

::    Use
git config --global --edit
::    to add this
[diff]
    tool = bcomp
[difftool]
    prompt = false
[difftool "bcomp"]
    trustExitCode = true
    cmd = "/usr/local/bin/bcomp" "$LOCAL" "$REMOTE"
[merge]
    tool = bcomp
[mergetool]
    prompt = false
[mergetool "bcomp"]
    trustExitCode = true
    cmd = "/usr/local/bin/bcomp" "$LOCAL" "$REMOTE" "$BASE" "$MERGED"

:: Other
git config --global core.excludesfile ~/.gitignore
git config --global mergetool.keepBackup false
git config --global push.default upstream
git config --global core.sharedrepository 1
git config --global receive.denyNonFastforwards true
git config --global http.postBuffer 500000000
git config --global core.autocrlf false
git config --global core.excludesfile "%USERPROFILE%\.gitignore"
:: Optional
:: this is a pain...git config --global --add core.pager cat

:: a few handy macros
git config --global alias.s "status -sb"
git config --global alias.b branch
git config --global alias.d "diff --stat --color -r"
git config --global alias.wd "diff --color-words"
git config --global alias.ci commit
git config --global alias.co checkout
git config --global alias.lg "log --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit --date=relative"

```

Merge and Diff with Beyond Compare 4

```
:: BC4 Setup
:: Launch Beyond Compare, go to the Beyond Compare menu and run "Install Command Line Tools"

::  This will get you set up to use 'git mergetool' and 'git difftool' while leaving git merge and git diff as-is
git config --global mergetool.keepBackup false
git config --global diff.tool bc4
git config --global difftool.prompt false
git config --global merge.tool bc4
git config --global difftool.bc4.path "C:\Program Files\Beyond Compare 4\BCompare.exe"
git config --global merge.tool bc4
git config --global mergetool.bc4.path "C:\Program Files\Beyond Compare 4\BCompare.exe"

:: Delete the leftover merge files
find . -name '*.orig' -delete

```

Check out a single file

```
#!bat

:: To get the revision
git branch -v

:: Then
git checkout -m <revision> <yourfilepath>
git add <yourfilepath>
git commit
```

Windows Setup

```
* Install GitExtensions (Install middle choice; Run git from the Windows Command prompt.)
* Install for all users
* Include MysysGit & KDiff3
* Choose PuTTY
* Install for Windows Command Prompt (Middle Choice)
* Choose Checkout As-Is, Commit As-Is line endings during the actual Git Install process.
* Install git-credential-winstore (BE SURE to Run as Admin)

SyncBack (For syncing your local repository to a network drive)
 
SyncBack Filter Exclusions
* *.aps
* *.bak
* *.cache
* *.exe
* *.ilk
* *.lib
* *.log
* *.ncb
* *.obj
* *.pch
* *.pdb
* *.sbr
* *.tlb
* *.tlh
* *.user
* *.vspscc
* *_i.c
* *_p.c
* _ReSharper*/
* Bin/
* Debug/
* obj/
* Release*/
* TestResult*
* Thumbs.db
* (Optional) Download Beyond Compare 3
* (Optional) Using Beyond Compare 3 With Git Extensions
* Configure name and e-mail
* 
```

```
#!bat

git config --global user.name "Your Name"
git config --global user.email "you@example.com"

```


Setup

```
#!bat
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
* 
* Getting Started
* GitFlow Scripts
* GitFlow process explanation
* Release Process
* Hot-Fix Process
* Peer to Peer
* Feature Branch
* Reversion
* Reference
* 
```

Reset a branch to another branch

```
#!bat
git checkout hotfixes
git reset --hard master
git push --force origin hotfixes
```

Edit Global Configuration
```
#!bat
subl ~/.gitconfig
```

Configuration Management

```
#!bat

:: Edit global config
git config --global --edit

:: Shows all inherited values from: system, global and local
git config --list

:: Shows values from: global
git config --global --list

:: Add a file that is on the ignore list 
git add -f <filename>

:: Get up-to-date on the develop branch
git pull origin develop

``` 
```
#!bat

:: Or in the case of a conflict where you want the differences in origin to take precedence.
git pull -s recursive -X theirs origin develop
Work on a shared feature branch through origin
:: On feature creation
git checkout -b feature26 develop
(make changes)
git commit -am "First feature commit"
git push -u origin feature26 # -u sets the upstream
 
:: On collaborators machine
git fetch origin
git checkout --track origin/feature26
 
:: Or to cause an existing local branch to track against an existing branch in origin:


git branch -u origin/fnc
```

Delete Remote Branch

```
#!bat

git push --delete origin feature9
```
 
Or remove dead branches from remote repository:

```
#!bat

git remote prune origin
```


Throw away unneeded changes

```
#!bat

:: Stash staged and unstaged changes
git stash
 
:: Stash only unstaged changes
git stash save --keep-index
 
:: Undo stash
git stash pop
 
:: Clear the Stash stack
git stash clear

```
Set Upstream Branch

```
#!bat

git branch --track fnc origin/fnc
```

Resolve Conflicts

```
#!bat
:: See file difference in origin
git diff origin/master -- [local-path-to-file]

:: This method seems to not be working
git checkout --ours -- <filename>
git checkout --theirs -- <filename>
 
:: This is working
git checkout branch -- src/MyFile.cs
 
:: To do an actual merge
git mergetool
```
Edit or Locate your active git config file 

```
#!bat

git config --global --edit

```

Check Status

```
#!bat

:: Show status of source code with respect to local repository
git status
 
:: Show branch status
git branch -a
:: or
git branch -vv   # doubly verbose!
 
:: Show remote brances and all tracking relationships
git remote -v show origin
 
::Update Image of origin 
git fetch origin && git remote prune origin && git branch -a

```
#!bat

:: Create empty branch
git checkout --orphan EmptyBranch
```

```
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


