## git setup

* after installing git need to initialize config

```
git config --global user.email "you@example.com"
git config --global user.name "Your Name"
git config --global core.editor "vim"
```

## git general information

* git has three file levels:
  - commits
  - stage index
  - working directory

* commit is a full snapshot of the repository, that is saved in the
database. Every state of the files that are committed, will be recoverable later at any moment

* git index is where the data that is going to
be saved in the commit is stored temporarily, until the commit is done

* working directory is the state of files in the git dir before they are staged or commited

* any change in files is automatically reflected in the git working repository 

* ```git status``` show the deltas between the three git trees


## creating repo

* ```git init``` to create a repo


## staging

* *staging* - process of adding files to the index (via ```git add```)

* at first new or changed files are not selected to be committed

* ```git add file_name``` is used to add file to be committed (can use --all)
* to undo add use ```git reset filename``` or ```git reset```


## committing

* ```git commit -m "message"``` to commit

* add the current change to the last commit (should be used locally)

```
git commit --amend
```

* orphaned commits - commits that are not on any branch (e.g. created at a detached HEAD, without later creating a new branch from them) - they will be cleared by git garbage collector (every 30 days)



## commit log, changes, files

* ```git log``` to view commits 
* ```git log -n 3``` to view e.g. last 3 commits
* ``git log --oneline``` to skip commit extra info (reduce to one line)
* ```git log --all --graph --decorate --oneline``` to view commits nicely put in a graph
* ```git log --oneline --branches=*``` to include commits from all branches

* ```git diff``` difference between working directory and last commit
* ```git show commit_code``` show different for a specific commit (can use HEAD, HEAD~1, direct code, etc)

* each commit also saves a snapshot of the stage index at the moment of commit

* ```git ls-files``` to specify a list of repo files (add -s to include staging code (SHA-1 hash) for each file)

* blame is best to use via GUI and it allows to know the history of modification of particular file/lines (to later 'blame' the author), 
the command itself won't do anything (safe to use, the name is somewhat misleading)


## HEAD ref

* HEAD is a reference to the current git branch, and it's turn - to the last commit in this branch
* if we checkout a specific commit (see further), this create a detached HEAD state, so that HEAD is not pointing to a specific branch
* HEAD~1, HEAD~2 etc is equivalent to the commit codes 1, 2, etc steps before

* ```HEAD~``` (remove one commit) will always work, but a conflit may happen if there are more than 1 parent (result of non-fast-forwarded merge), 
in this case specify the parent number to use , like this (^2, i.e. second parent is used)
```
git reset --hard HEAD~2^2
```

* it is always prefered to use just ```HEAD~```




## branches

* branch - independent development path
* ```git branch new-branch``` create new branch
* ```git branch -a``` list all branches
* ```git branch -d branch_name``` delete local branch (while not being on it)
* ```git checkout new-branch``` start working with new branch, 
HEAD is now pointing to ```new-branch```


## merging branches

* merge master branch with another branch

```
git checkout master
git merge new-branch
```

* fast-forwarding will be the default option of merge if the two branches have common ancestor

* ```--no-ff``` option avoids fast-forwarding, and show much more clear history, it is always advisable not to use fast-forward mode!

* ```git branch -d new-branch``` - delete branch (usually when it was used for developing new feature and it's now merged to master)

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
use ours to stay with HEAD and theirs to stay with the other branch version;

* otherwise, if we want to manually adjust the current branch, make the changes in the current branch (or local version if merge during pull), use ```git add . ``` to add corrected conflict files; then run ```git commit``` - vim will open to enter the merge commit message; after that the conflict is resolved

* if we started a merge and got a conflict, we can return to the previous correct state before the merge using
```
git merge --abort
```


* rebase to remote branch (if some commits were done to remote branch, I also did some commits, now I want to make my local 
version if like I pull the current remote branch first and than added my commits)
```
git fetch origin            # Updates origin/master
git rebase origin/master    # Rebases current branch onto origin/master
```
or even simpler
```
git pull --rebase origin master
```
(master branch taken as an example)



## tags

* used to mark import points in the commit history
* usually used for releases (final and also development stages)

* to make a tag - need tag name and message (e.g.)

```
git tag -a v0.1 -m ’v0.1 stable release, changes from...’
```

* delete tag

```
git tag -d <tag-name>
```

* get tag pointing on current commit
```
git tag --points-at HEAD
```

* checkout tag (go to detached HEAD state, similar to commit checkout; branch name is optional)
```
git checkout tags/tag_name -b branch_name
```

## git checkout

* can be used with branch, with path or both, or a commit

* ```git checkout branch_name``` move HEAD to a different branch
* ```git checkout -b new_branch_name``` create new branch starting from the current HEAD (can be last commit of the current branch or a detached HEAD pointing to any commit)
* before detaching head need to commit or stash all current changes (to properly save the current state, so that it's not lost)
* ```git checkout commit_code``` move HEAD to specific commit (creates detached HEAD), instead of commit code can use HEAD~1 etc.

* at detached HEAD we can experiment (make changes, create commits)
* if we want to save these commits/staged index in a branch - can use ```git branch -b new_branch_name```, else go back to an existing branch (e.g. ```git checkout master```); 
in this case the commits will be orphaned; any file changes will be still there but can undone using ```git reset```

* ```git checkout commit_code file_name``` will restore the file to the stage index of the commit (thus undoing the working directory changes) - can be used without commit_code (defaults to HEAD, though there may be a conflict if file has the same name as a branch)

* can also specify a specify SHA-1 (staging hash code) to revert file to (though it's rarely used)

* ```git checkout .``` will undo all unstaged changes in the working directory (. means all files, 
HEAD is the default commit)



## git revert

* use to revert a commit that's already public in a forward way 
* undo action will appear as a new commit
* can select specific commit to undo (not necessarily the latest, the intermediate commits will be left untouched)
* ```git revert commit_code``` will attemp to revert the commit, editor for commit message will open (similar to merge)
* if the file addition commit is reverted, the file will be deleted permanently (not left as unstaged!)


## git reset

* use to undo changes locally (never use for public pushed commits - this will leave other's local repos in a broken state with orphaned commits)

* unlike checkout ```git reset``` will move HEAD pointer and also current branch ref pointer to a specified commit

* ```git reset``` with commit defaults to HEAD

* options:
  * --hard means that all the work after the specified commit is removed and lost (meaning all subsequent commits, staged changes and unstaged changes are no longer present in the working directory)

  * --mixed (default) - moves the ref pointer to the specified commit, stage index will move to the saved stage index of the commit, any changes w.r.t. the current working directory will remain as unstaged

  * --soft - moves the ref pointer, working directory is unchanges,  the intermediate removed commits are moved to stage index (so all changes removed will be now stages)

  * can also specify file(s) to reset, need to specify HEAD explicitly, e.g.
  ```git reset HEAD file_name``` (default is --mixed mode) will unstage a particular file (move from staging index to just working dir changes)

  * to completely overwrite local branch with remote brach use (from the branch you're overwriting)
  ```
  git reset --hard origin/branch_name
  ```

## git clean

* used to remove untracked files
* ```git clean -n``` dry run - shows what files would be removed
* ```git clean -f``` remove untracked files
* ```git clean -df``` remove with directories
* ```git clean -xf``` remove including files from .gitignore (normally they're left untouched)

## git rm 

* used to remove files either only from staging index or both from staging index and working directory

* ```git rm file_name -f``` remove file
* use -r (recursive) to remove dir with its content
* if --cached is passed - remove the files only from the staged index
* using ```git rm``` is a shortcut for linux rm plus staging change via ```git add```

----------------------------------------------------

## repo branching strategies

* single main running version strategy:

	- have master, dev branches, and separate branch from dev for each feature
	- when feature is developed its branch is integrated with dev and removed
	- dev is merged with master after a set of features was developed that results in a stable version
	- separate branch is also recommended for each bug fix (can split and merge directly to master)



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

* before running ```pull``` or ```push``` for the first time run 

```
git branch --set-upstream-to=origin/<branch> master
```
(can using -u as short form, typically ```git push -u origin master);
the idea to create a new branch on remote if not create, which will be the upstream to the given local branch (most often the same branch name)

* ```git push remote_name --delete branch_name``` delete remove branch (remote_name is usually origin)

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

* remove remote upstream (e.g. name origin)
``` git remote remove origin ```


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



* if while connecting git local repo and remote getting the following
``` fatal: refusing to merge unrelated histories ```

simply run 
```
git pull --allow-unrelated-histories
```

* to correct last commit message
```
git commit --amend -m "New commit message."
```


*  Adding 'add all and commit'

run (outside any git repo)

```
git config --global alias.ca '!git add --all && git commit'
```
(```git config --global --unset alias.ca``` to remove; works with any other alias)

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
.pytest_cache/
```

* use ```git mv old_name new_name``` to properly rename folder or file, while keeping change history (rather that having deletion and new file/folder)

--------

**questions and further work**

- common ancestor of branches? - what are the implications for merge, etc?
- how exactly can I resolve merge conflict in a file?
- git push w/o args is to origin and the current branch, right?
- so how to resolve conflicts with remote, and how to visualize code where the conflict happened??
- what is ```git stash```
- next step is learn more about working with remote repo, origin etc



