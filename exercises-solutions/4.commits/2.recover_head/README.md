# Recovering the HEAD - with solutions

The goal of this exercise is to learn to identify a "detached HEAD" situation
and recover from it. Enter the `repository/` directory and perform the following
steps:

 1. Enter the `repository/` directory and check whether the HEAD is detached. 
 
 2. If the HEAD is detached, return the `HEAD` back to the tip of the branch. 
 
 3. Confirm that that the `HEAD` indeed points to the tip of the branch`

Hints:

 - git checkout <ref>
 - rev-parse
 - cat .git/something


**Solution**

 1. The `HEAD` is indeed detached.

```shell
$ git status
HEAD detached at 3aee0ad
nothing to commit, working tree clean
```

or

```shell
$ git log --oneline --all --graph   
* 47e9c43 (master) Add remaining ingredients and directions
* 3aee0ad (HEAD) Add some ingredients
* 8806db1 This is going to be a cake recipe
```

 2. `git checkout master`

 3. There are several ways one can confirm that `HEAD` points to the tip of the `master`/`main` branch:

```shell
$ git status
On branch master
nothing to commit, working tree clean
```

or

```shell
$ git log --oneline --all --graph
* 47e9c43 (HEAD -> master) Add remaining ingredients and directions
* 3aee0ad Add some ingredients
* 8806db1 This is going to be a cake recipe
```

or

```shell
$ cat .git/HEAD    
ref: refs/heads/master
```

