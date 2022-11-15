# Discarding the latest commit - with solutions

The goal of this exercise is to learn to discard the latest commit. Enter the
`repository/` directory and perform the following steps:

 1. Discard the latest commit. Also discard the changes in the working tree.
 
 2. Confirm that the commit is no longer reachable from `master`. Confirm that
    the `recipe.txt` no longer contains the section "Other ideas and hints".
 
 3. Try to restore the discarded commit. (optional)

**Solution**

 1. Having a look at the repository:

```shell
$ git log --oneline --all --graph
* 2690c4f (HEAD -> master) Add other ideas and hints
* 9552f3f Add directions
* 9b751b9 Add ingredients
* ddfe74e Better name for the cake
* d290aa4 This is going to be a cake recipe
$ git status
On branch master
nothing to commit, working tree clean
```

Discard the latest commit; also discard changes in the working directory:

```shell
$ git reset --hard HEAD~
HEAD is now at 9552f3f Add directions
```

 2. The previous commit is no longer reachable from the `master` branch:

```shell
$ git log --oneline
9552f3f (HEAD -> master) Add directions
9b751b9 Add ingredients
ddfe74e Better name for the cake
d290aa4 This is going to be a cake recipe
```
Open `recipe.txt` with your favourite editor to confirm it does not contain "Other ideas and hints" or `cat recipe.txt`.

 3. Checking the reflog for the lost commit: 

```shell
$ git reflog
9552f3f (HEAD -> master) HEAD@{0}: reset: moving to HEAD~
2690c4f HEAD@{1}: commit: Add other ideas and hints
9552f3f (HEAD -> master) HEAD@{2}: commit: Add directions
9b751b9 HEAD@{3}: commit: Add ingredients
ddfe74e HEAD@{4}: commit: Better name for the cake
d290aa4 HEAD@{5}: commit (initial): This is going to be a cake recipe
```
Reset to the previously-discarded commit:

```shell
$ git reset --hard HEAD@{1}
HEAD is now at 2690c4f Add other ideas and hints
```

or `git reset --hard 2690c4f`.

