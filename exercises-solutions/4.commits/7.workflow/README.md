# Proper commit workflow - with solutions

This exercise is meant to demonstrate the proper workflow for making multiple
commits from a **single set of edits**. The overall goal is to make sure that
each commit produces a valid revision. This type of workflow is beneficial when
working with source code since each revision should both compile and function
correctly. The workflow is not that beneficial with the the example below but
it is used as an example only.

Enter the `repository/` directory and perform the following steps:

 1. You can confirm (`git diff HEAD`) that the `repository/recipe.txt` file
    contains uncommitted changes. That is, the recipe have been converted to
    metric system.

 2. You can also confirm (`git diff --cached`) that some of these changes have
    been already staged. 
    
    As you can probably guess, the **first commit** we are creating is going to
    convert the measurements to metric.
    
    The changes that are related to the pan size and the oven temperature (8th
    step the the directions) are going to be committed **separately**.

 3. Store the the unstaged changes to the stash:
 
    ```
    $ git stash --keep-index
    ```
    
    The `--keep-index` options tells Git to keep the staged changes. Otherwise
    Git would stash them.

 4. Now, investigate the content of the `repository/recipe.txt` file. You can
    see that the 7th step in the directions contains an unconverted measurement.
    This means that whoever created this exercise forgot to stage this line.
    This would correspond to a situation where the source code does not compile
    or does not function correctly.

    Commit the staged file.

 5. Pop the unstaged changes, and stage and commit changes that are related to
    the pan size and the oven temperature.
 
    ```
    $ git stash pop
    ```
    
    This is going to be the **second commit**.

Confirm that the two commits you created indeed contain the desired changes.


**Solution**

 1. Investigate the repository:

```shell
$ git status
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
	modified:   recipe.txt

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
	modified:   recipe.txt

$ git log --oneline --all --graph
* 47e9c43 (HEAD -> master) Add remaining ingredients and directions
* 3aee0ad Add some ingredients
* 8806db1 This is going to be a cake recipe
```

`git status` and `git diff HEAD` confirm that there are uncommitted changes.

 2. `git diff --cached`

 3. Stash the changes, but keep the staged ones:
```shell
$ git stash --keep-index
Saved working directory and index state WIP on master: 47e9c43 Add remaining ingredients and directions
$
$ git stash list
stash@{0}: WIP on master: 47e9c43 Add remaining ingredients and directions
$
$ git status    
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
	modified:   recipe.txt

```

 4. View `recipe.txt`.

 Do the first commit:

```shell
$ git commit -m "transform to metric measurements"
[master ff9714d] transform to metric measurements
 1 file changed, 6 insertions(+), 5 deletions(-)
```

 5. Pop the unstaged changes from stash:

```shell
$ $ git stash pop 0
Auto-merging recipe.txt
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
	modified:   recipe.txt

no changes added to commit (use "git add" and/or "git commit -a")
Dropped refs/stash@{0} (93383ced14ac15405558556c9dcc217d04b84eb7)
```
Do the second commit:

```shell
$ git add recipe.txt 
$    
$ git commit -m "oven size and temperature update"
[master aa84b99] oven size and temperature update
 1 file changed, 2 insertions(+), 2 deletions(-)
```

