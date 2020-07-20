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


(stopped at 4.8 - tagging)

--------

questions
- what is HEAD, origin?

- common ancestor of branches? - what are the implications for merge, etc?

- how exactly can I resolve merge conflict in a file?




