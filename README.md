gitcrib
======================

My personal set of reminders on how to get things done in git.

### Create new branch from existing branch
```
git checkout -b develop master
```

### Create branch that tracks upstream branch
```
git branch --track fnc origin/fnc
```

### Create remote branch and cause the local branch to track against it
```
git push --set-upstream origin feature97
```

### Cause an existing local branch to track against an existing branch in origin:
```
git branch -u origin/fnc
```

### Undo git add
```
git reset
```

### Check out a single file
```
#!bat

:: To get the revision
git branch -v

:: Then
git checkout -m <revision> <yourfilepath>
git add <yourfilepath>
git commit
```

### Reset a branch to another branch

```
git checkout hotfixes
git reset --hard master
git push --force origin hotfixes
```

### Edit Global Configuration
```
subl ~/.gitconfig
```

### Delete Remote Branch
```
git push --delete origin feature9
```
 
### Or remove dead branches from remote repository:
```
git remote prune origin
```


### Throw away unneeded changes
```
:: Stash staged and unstaged changes
git stash
 
:: Stash only unstaged changes
git stash save --keep-index
 
:: Undo stash
git stash pop
 
:: Clear the Stash stack
git stash clear
```

### Resolve Conflicts
```
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

### Edit or Locate your active git config file 
```
git config --global --edit
```

### Check Status
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

### Create empty branch
```
git checkout --orphan EmptyBranch
```

### Merge with remote taking precedence
```
git pull -s recursive -X theirs origin develop
```

### Work on a shared feature branch through origin
```
:: On feature creation
git checkout -b feature26 develop
(make changes)
git commit -am "First feature commit"
git push -u origin feature26 # -u sets the upstream
 
:: On collaborators machine
git fetch origin
git checkout --track origin/feature26
```

### Create a new branch from a prior commit
```
:: Get the target commit
git checkout -m 913f7cf

:: Set the now detached head to a new branch
git checkout -b uwp

:: Set the upstream branch
git push --set-upstream origin uwp
```
