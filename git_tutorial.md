* after installing git need to initialize config

```
git config --global user.email "you@example.com"
git config --global user.name "Your Name"
```

* ```git init``` to create a repo

* A commit is a full snapshot of the repository, that is saved in the
database. Every state of the files that are committed, will be recoverable later at any moment

* not all the repo has to be commited

* *staging* - process of adding files to the index

* git index is where the data that is going to
be saved in the commit is stored temporarily, until the commit is done

* at first new or changed files are not selected to be committed

* ```git add file_name``` is used to add file to be committed (can use --all)

* ```git commit -m "message"``` to commit

* ```git log``` to view commits

* ```git log --all --graph --decorate --oneline``` to view commits nicely put in a graph

* branch - independent development path

* ```git branch new-branch``` create new branch

* ```git checkout new-branch``` start working with new branch
HEAD is now pointing to ```new-branch```

* merge

```
git checkout master
git merge new-branch
```

* fast-forwarding will be the default option of merge if the two branches have common ancestor

* ```--no-ff``` option avoids fast-forwarding, and show much more clear history, it is always advisable not to use fast-forward mode!

* ```git branch -d new-branch``` - delete branch (usually when it was used for developing new feature and it's now merged to master)

--------------------------

* confict arises during merge when it cannot be done automatically (same file part modified differently in two different branches)

* if we open conflicting file, we will see smth like

```
one
two
<<<<<<< HEAD
three
=======
three (from second-branch)
>>>>>>> second-branch
```
need to resolve the conflict and run git add, git commit


* knowing in advance which version to stay with, use

```
git merge -X <ours|theirs> <branch-name>
```
use ours to stay with HEAD and theirs to stay with the other branch version


* ```git diff``` difference between working directory and last commit

---------------------------------


## Tags

* used to mark import points in the commit history
* usually used for releases (final and also development stages)

* to make a tag - need tag name and message (e.g.)

```
git tag -a v0.1 -m ’v0.1 stable release, changes from...’
```


---------

## Undoing and deleting things

* add the current change to the last commit

```
git commit --amend
```

* move file to the state of the last commit 

```
git checkout file_name
```


* deleting commits is done by moving HEAD or branch pointer

* soft and hard reset (soft by default):
if you make a soft reset, the commit(s) will be removed, but the modifications saved in that/those
commit(s) will remain; and a hard reset, won’t leave change made in the commit(s).

* to make reset use 

```
git reset --hard HEAD~
```

(that's to remove the last commit, use ```HEAD~3``` to remove more parent commits, e.g. 3 here)

* ```HEAD~``` (remove one commit) will always work, but a conflit may happen if there are more than 1 parent (result of non-fast-forwarded merge), 
in this case specify the parent number to use , like this (^2, i.e. second parent is used)
```
git reset --hard HEAD~2^2
```

* it is always prefer to use just ```HEAD~```

* delete tag

```
git tag -d <tag-name>
```


--------------------

## Branching strategies

* single main running version strategy:

	- have master, dev branches, and separate branch from dev for each feature
	- when feature is developed its branch is integrated with dev and removed
	- dev is merged with master after a set of features was developed that results in a stable version
	- separate branch is also recommended for each bug fix (can split and merge directly to master)


-----------------------

## Working with remote repos

* command to add remote to the current local repo

```
remote add <remotename> <repo-url>
```

smth like 

```
git remote add origin https://hosting-service.com/username/repository-name
```

origin is the default name that we choose in git when creating remote repos, same as master; but anything can be used, e.g.

```
git remote add github https://github.com/username/repository-name
git remote add bitbucket https://bitbucket.org/username/repository-name
```

if multiple remotes are used


* examples of using git push

```
git push origin --all # Updates the remote with all the local branches
git push origin master dev # Updates remote’s mater and dev branches
git push origin --tags # Sends tags to remotes
```

* before running ```pull``` for the first time run 

```
git branch --set-upstream-to=origin/<branch> master
```


* Cloning

```
git clone https://hosting-service.com/username/repository-name
```

usually only master branch will be copies, to check (remote) branch list use ```git branch -r```, 
add branch to local repo by applying ```checkout``` to it


* Fetch - updating local repo reference to the changes in the remote (but not actually applying changes!), (here ```origin``` - remote name, ```master``` - branch name)
```
git fetch origin master
```
or can use 
```
git fetch --all
```
to fetch all branches
(after fetch the reference is updated but the changes are not applied in the local repo)

To apply change would have to use ```git merge origin/master``` after ```git fetch origin master```


* ```pull``` is simply ```fetch``` followed by the ```merge``` can do 

```
git pull origin master
```

* confict with remote repo : trying to push a new commit without pulling commit(s) from remote that you don't yet have locally, 
will get error like this

```
! [rejected] master -> master (fetch first)
error: failed to push some refs to ’https://hosting-service.com/alice/repository-name.git’
hint: Updates were rejected because the remote contains work that you do
hint: not have locally. This is usually caused by another repository pushing
hint: to the same ref. You may want to first integrate the remote changes
hint: (e.g., ’git pull ...’) before pushing again.
hint: See the ’Note about fast-forwards’ in ’git push --help’ for details.
```

* using ```git push --force``` is not recommended, the new commit in the remote will be lost, and (!) this will leave the local repo 
of other users that made this commit in broken state (!)

so it's very bad even if the lost commit were useless.

* deleting commit

```
git push origin HEAD~2:master --force
```

(general syntax is ```git push origin <source>:<destination>```)


* cherry-pick only some commits from another branch

```
git cherry-pick -x aba6c1b # Several commits can be cherry picked
```

(should not be a recurrent practice)



*  Adding 'add all and commit'

run

```
git config --global alias.ca '!git add --all && git commit'
```

then use as

```
git ca -m 'Commit message'
```


* in .gitignore: if a folder is specified - it will be ignored in all nested subfolders as well, 
can add multiple .gitignore files in various subfolders to apply this ignore logic to all of them

* .gitignore example for vscode python package

```
.env/
__pycache__/
*.egg-info/
.pytest_cache/
.vscode/
```

--------

questions
- what is HEAD, origin?
HEAD is a pointer to last commit of the current branch, from which the commit history for a branch is read

- common ancestor of branches? - what are the implications for merge, etc?

- how exactly can I resolve merge conflict in a file?

- what exactly are tags used for?

- full options and args list of git commit, push, pull, add etc

- git push w/o args is to origin and the current branch, right?

- switching branches in vscode and sublime git projects (how to choose which branch contents to show??)

- what happens if I move the HEAD pointer (delete last commit) and then push this change to remote?

- so how to resolve conflicts with remote, and how to visualize code where the conflict happened??








