---
title: "Lecture 5: Branches"
tags: Lecture, Diana, day 3, 4
description: "Branches, merges and conflicts"
---

<!-- Lecture material made by Birgitte Brydsö for the version of the course that was given in fall 2020. Lecture was first given by Birgitte Brydsö in fall 2020. 
Minor modifications done for the fall 2021/2022/2023 versions of the course. -->

<!-- Slides: https://hackmd.io/@git-fall-2024/L5-branches --> 

# Lecture 5: Branches

---

## Objectives

- Get some more hands-on working with branches
    - creation
    - switching
    - merging
    - deletion
    - handling uncommitted changes
        - stashing
        - discarding
        - checkout with merge
    - merging and merge conflicts
    - rebasing: combining a sequence of commits to a new base commit.
    - cherry-picking


---

## What is a Git branch?

* A pointer to a commit (ref: named pointer)
* Defined as all points reachable in the commit graph from the named commit (the "tip" of the branch)
* The ref HEAD determines what branch you are on. 
* If HEAD is a symbolic ref for an existing branch, then you are “on” that branch. 
* If HEAD is a simple ref directly naming a commit by its SHA-1 ID, you are  not “on” any branch - you are in “detached HEAD” mode, which happens when you check  out some earlier commit to examine. 

---

## Why use branches?

There are many uses for branches:

- Test different directions for a project
- Several projects members would like to work on their own copy of the code
- Bug fixes that are not yet tested, but will later be merged into the main version

---

## What is a Git branch?

Until now, we have worked with a repository that only have one branch, with the commits done one at a time: 

![Git branch](../images/git-branch.png)

In the above picture, the master branch points to a commit. The current position is HEAD. (Time goes rightwards)

---

### What is a Git branch - basic concepts

Now we want to look at repositories with several branches: 

![Git several branches](../images/git-several-branches.png)

Branches are used to create another line of development.  They are "individual projects" within a git repository.

---

* The branch is the commit and all its parent commits, not just the one we are currently pointing at. 
* The main line of development is usually called the "master" branch.
* Different branches within a repository can have
  * completely different files and folders
  * almost everything the same except for a few lines of code in a file

---

<!-- .slide: data-background="#ffffff" -->

<!-- .slide: style="font-size: 32px;" -->

Usually, a branch is created to work on a new feature. Once the feature is completed, it is merged back with the master branch.


![](https://i.imgur.com/9Y4ymjG.png)


---

<!-- .slide: data-background="#ffffff" -->

## Branches: Creation

<!-- .slide: style="font-size: 36px;" -->

Creating a new branch does not change the repository, it just adds a new reference to the commit. 

Note that the branch is created from the current HEAD.

To create a new branch (called cool-feature in the following): 

```shell
$ git branch cool-feature
```

---

<!-- .slide: data-background="#ffffff" -->

<!-- .slide: style="font-size: 36px;" -->

To move to another branch (switch): 

```shell
$ git checkout cool-feature
```
or...
```shell
$ git switch cool-feature
```

If you wish to switch to a new branch that is not yet created, you can do so by adding the flag `-b` to `git checkout`.

To see which branch you are on:

```shell
$ git branch
```


---

<!-- .slide: data-background="#ffffff" -->

## Branches: merging, deletion

<!-- .slide: style="font-size: 30px;" -->

- When you have decided you are happy with the changes you made to the new branch, merge it back to the master branch (or another branch)
- Note: The branch is always merged to the current HEAD.
- First switch to the branch you are merging it to:

```shell
$ git checkout master
```

- Then merge them:
```shell
$ git merge cool-feature
```
- You can now delete the extra branch:
```shell
$ git branch -d cool-feature
```

---

<!-- .slide: data-background="#ffffff" -->

### Example - Type along if you wish

<!-- .slide: style="font-size: 32px;" -->

* Create a directory. Initialize a repository
* Create a file, stage it, and commit it

```shell
$ mkdir my-project; cd my-project/
$ git init
Initialized empty Git repository in /home/bbrydsoe/my-project/.git/
$ touch file.txt
$ git add file.txt 
$ git commit -m "Committing the first file"
[master (root-commit) 1006b51] Committing the first file
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 file.txt
```


---

<!-- .slide: data-background="#ffffff" -->

<!-- .slide: style="font-size: 32px;" -->

* Create a new branch, then switch to that branch
* Make some changes - add files and text ( > overwrites or are suitable for new file)
* Stage the file and commit it
```shell
$ git branch cool-feature
$ git checkout cool-feature 
Switched to branch 'cool-feature'
$ echo "This is a text" > file.txt 
$ git add file.txt 
$ git commit -m "Added text to the first file" 
[cool-feature 5bad966] Added text to the first file
 1 file changed, 1 insertion(+)
```

---

<!-- .slide: data-background="#ffffff" -->

<!-- .slide: style="font-size: 30px;" -->

- Switch back to the master branch, make some changes 
```shell
$ git checkout master
Switched to branch 'master'
$ echo "Text to the second file" > second-file.txt 
$ git add second-file.txt 
$ git commit -m "Added a second file"
[master bdec2cf] Added a second file
 1 file changed, 1 insertion(+)
 create mode 100644 second-file.txt
```
- We should check the effect of the changes. I will use this command: 
```shell
$ git log --graph --oneline --decorate --all
``` 
- or, if you made an alias before.
```shell
$ git graph
```
- Otherwise make the alias:
```shell
$ git config --global alias.graph "log --all --graph --decorate --oneline"
```

---

<!-- .slide: data-background="#ffffff" -->

<!-- .slide: style="font-size: 32px;" -->

This is on the master branch 

```shell
$ git graph
* bdec2cf (HEAD -> master) Added a second file
| * 5bad966 (cool-feature) Added text to the first file
|/  
* 1006b51 Committing the first file
```

We now merge the branches and check again 

```shell
$ git merge cool-feature 
Merge made by the 'recursive' strategy.
 file.txt | 1 +
 1 file changed, 1 insertion(+)
```

- Note that in recent git versions (>=2.33) the default "recursive" strategy is replaced by the "ort" strategy.
```shell
$ git graph
*   cf3e6b7 (HEAD -> master) Merge branch 'cool-feature'
|\  
| * 5bad966 (cool-feature) Added text to the first file
* | bdec2cf Added a second file
|/ 
* 1006b51 Committing the first file
```


---

<!-- .slide: data-background="#ffffff" -->

<!-- .slide: style="font-size: 36px;" -->

Now we can delete the new branch we had created, since all the content is now in the master branch. 

```shell
$ git branch -d cool-feature 
Deleted branch cool-feature (was 5bad966).
```
Comment: It is good practice to keep old branches for understanding of the development. Deletion could however be done for very evident mistakes or insignificant issues.

---

<!-- .slide: data-background="#ffffff" -->

<!-- .slide: style="font-size: 26px;" -->

In a somewhat nicer format, it looks like this: 

We commit stuff to both branches
```graphviz
digraph {
  rankdir=LR
  "commitX" -> "commit1"
  "commit2" -> "commit1"
  "commitY" -> "commitX"
  "commit3" -> "commit2"
  "master" -> "commit3" [style=dashed]
  "cool-feature" -> "commitY"[style=dashed]
  master [shape=plaintext]
  "cool-feature" [shape=plaintext]
}
```
(Time goes leftwards)

---

<!-- .slide: data-background="#ffffff" -->

<!-- .slide: style="font-size: 26px;" -->

Merge 'cool-feature' to 'master'
```graphviz
digraph {
  rankdir=LR
  "commit2" -> "commit1"
  "commitX" -> "commit1"
  "commit3" -> "commit2"
  "commitY" -> "commitX"
  "master" -> "commit4" [style=dashed]
  "cool-feature" -> "commitY" [style=dashed]
  "commit4" -> "commit3"
  "commit4" -> "commitY"
  master [shape=plaintext]
  "cool-feature" [shape=plaintext]
}
```

Delete 'cool-feature'
```graphviz
digraph {
  rankdir=LR
  "commit2" -> "commit1"
  "commitX" -> "commit1"
  "commit3" -> "commit2"
  "commitY" -> "commitX"
  "master" -> "commit4" [style=dashed]
  "commit4" -> "commit3"
  "commit4" -> "commitY"
  master [shape=plaintext]
}
```
(Time goes leftwards)

---

<!-- .slide: data-background="#ffffff" -->

## Switching with uncommitted changes

<!-- .slide: style="font-size: 26px;" -->

As mentioned above, you switch between branches with: 

```shell
$ git checkout <branch>
```

What happens if you have uncommitted changes (and/or new files added) when you try to switch?

- The uncommitted changes will be carried to the new branch that you switch to, if possible. 
 
- Changes that you commit will be committed to the newly switched branch.

What if there is a conflict?
- You will **not** be allowed to switch to the other branch.
- You must commit or stash any conflicting changes before switching branches.

---

<!-- .slide: data-background="#ffffff" -->

### Example - new file

<!-- .slide: style="font-size: 30px;" -->

**We continue in the same repository!**
Here we create a new branch, switch to it, then add a new file. Then we switch back to the master branch without committing the changes: 

```shell
$ git checkout -b cool-feature 
Switched to a new branch 'cool-feature'
$ touch newfile.txt
$ git add newfile.txt 
$ git checkout master
A	newfile.txt
Switched to branch 'master'
```

Git warns that there is a file added (`A`) in one branch but not the other, but the switch is allowed. 

---

<!-- .slide: data-background="#ffffff" -->

### Example - modified file

<!-- .slide: style="font-size: 32px;" -->

**We continue in the same repository!**
First commit the `newfile.txt` in the cool-feature branch to clean the environment.
If we make changes to the file in one of the branches (go back to `cool-feature`) but not on the other and do not commit it, then git will again warn: 

```shell
$ git switch cool-feature
$ git commit -m "newfile.txt"
$ echo "Adding some text" >> second-file.txt
$ git add second-file.txt 
$ git checkout master
M	second-file.txt
Switched to branch 'master'
```

Git warns that there is a file that is modified (`M`) in one branch but not the other, but the switch is allowed. 

---

<!-- .slide: data-background="#ffffff" -->

### Example - uncommitted, conflicting changes

<!-- .slide: style="font-size: 32px;" -->

**We continue in the same repository!**
Assume two branches, "cool-feature" and "morefeatures"

Create the branch "morefeatures" without switching to it
Switch to branch "cool-feature", add some text to a file, stage the file and commit it: 

```shell
$ git branch morefeatures
$ git checkout cool-feature 
Switched to branch 'cool-feature'
$ git commit -m "second-file.txt"
$ echo "add text" >> morefiles.txt 
$ git add morefiles.txt 
$ git commit -m "Some text"
[cool-feature 469542b] Some text
 1 file changed, 1 insertion(+)
 create mode 100644 morefiles.txt
```

---

<!-- .slide: data-background="#ffffff" -->

<!-- .slide: style="font-size: 30px;" -->

Switch to branch "morefeatures". Modify the same file, stage the file and commit it. Then try and switch back to the "cool-features" branch: 

```shell
$ git checkout morefeatures 
Switched to branch 'morefeatures'
$ echo "Adding yet some more text" >> morefiles.txt
$ git add morefiles.txt 
$ git checkout cool-feature 
error: Your local changes to the following files would be overwritten by checkout:
	morefiles.txt
Please commit your changes or stash them before you switch branches.
Aborting
```
Now Git complains and do not allow the switch. 

---


<!-- .slide: data-background="#ffffff" -->

## Handling uncommitted changes

<!-- .slide: style="font-size: 36px;" -->

So, what can we do if there is a conflict?

* Commit the changes before switching branch
* Stash the uncommitted changes
* Discard the uncommitted changes
* Checkout with Merge

---

<!-- .slide: data-background="#ffffff" -->

## Stashing

<!-- ## Handling uncommitted changes - stashing -->

<!-- .slide: style="font-size: 32px;" -->

The command "stash" can be described as a **drawer** where you store uncommitted changes temporarily. 

After stashing your uncommitted changes you can continue **working on other things** in a different branch.

The uncommitted changes that are stored in the stash **can be taken out and applied to any branch, including the original branch.**

---

<!-- .slide: data-background="#ffffff" -->

### Stashing, example (no type-along this time)

<!-- .slide: style="font-size: 32px;" -->

First do a `git status` in the branch where you may have uncommitted changes: 

```shell
$ git status
On branch morefeatures
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

	modified:   file.txt
	new file:   morefiles.txt
```

You can see the dirty status. 

---

<!-- .slide: data-background="#ffffff" -->

<!-- .slide: style="font-size: 32px;" -->

To fix it, let us use `git stash`:

```shell
$ git stash
Saved working directory and index state WIP on morefeatures: 4922606 Some text
```

Checking again with `git status`: 

```shell
$ git status
On branch morefeatures
nothing to commit, working tree clean
```

You can now switch branches and work on something else. 


---

<!-- .slide: data-background="#ffffff" -->

## Working with stashes (repetition)

You can have several stashes stored. To see them, use 

```
$ git stash list
```

Example: 

```
$ git stash list
stash@{0}: WIP on morefeatures: 4922606 Some text
stash@{1}: WIP on morefeatures: 4922606 Some text
stash@{2}: WIP on morefeatures: 4922606 Some text
```

---

<!-- .slide: data-background="#ffffff" -->

### Working with stashes - continued (repetition)

When you have done what you needed before committing the stashed changes you can reapply a stash (select branch first), using 

```
$ git stash apply
```

which will apply the most recent stash. If you want to apply a different stash, you can name it.

Example: 

```
$ git stash apply stash@{0}
```

---

<!-- .slide: data-background="#ffffff" -->

## Discarding uncommitted changes 

<!-- .slide: style="font-size: 32px;" -->

If you do not want to stash your changes, but just **get rid** of them, you can use `git clean`.

WARNING: This command will remove all non-tracked files in your current directory!

You can safely test which files will be removed by running: 

```shell
$ git clean --dry-run
```


---

<!-- .slide: data-background="#ffffff" -->

## Handling uncommitted changes - merging

<!-- .slide: style="font-size: 30px;" -->

- There is a checkout with merge option. Add the flag `--merge` (or `-m`): 
```shell
$ git checkout --merge <branch>
```
- This will perform a **three-way merge between your working tree and the new branch, with the current branch as the base.**

- After the merge, you will be on the new  branch and the merged result will be in your working tree. 
 
- NOTE: As with any merge, **conflicts may result** and you will then have to resolve those. 


---

<!-- .slide: data-background="#ffffff" -->

## Merging and merge conflicts

<!-- .slide: style="font-size: 32px;" -->

- Merge conflicts will happen now and then when you are working with more than one branch and try to merge them. 
- In many cases, Git is actually able to do a merge without problems. However, merge conflicts can happen.
- If Git cannot safely merge something automatically, you will get a message like this:
```shell
error: Entry '<fileName>' would be overwritten by merge. 
Cannot merge. (Changes in staging area)
```

- NOTE: Always check that you are on the right branch before merging! You check the branch with `git branch`.


---

<!-- .slide: data-background="#ffffff" -->

<!-- .slide: style="font-size: 32px;" -->

Git can automatically try to merge when you give the command: 

```shell
$ git merge <branch-to-merge-into-present-branch>
```

while standing on the branch you want to merge to. 

---

<!-- .slide: data-background="#ffffff" -->

### Merge strategies
<!-- .slide: style="font-size: 24px;" -->

The most commonly used 

* Fast Forward Merge 
  * the commit history is one straight line. 
  * You create a branch, you make some commits there, but no changes to the 'master'. You then just merge onto the 'master'. This just moves the pointer for the 'master' branch forward in a straight line. 
* Recursive Merge (until 2.32)
  * make a branch and make some commits there, but also make new commits that are made on another branch, like the ‘master‘. 
  * Then, when you want to merge, git will recurse over the branch and create a new merge commit. The merge commit will continue to have two parents. 
* ORT (from git-2.33)
  * acronym for "Ostensibly Recursive’s Twin"
  * replacement for the previous default algorithm, recursive.
  * This is the default merge strategy when pulling or merging one branch. 
  * Results in fewer merge conflicts without causing mismerges 

---

<!-- .slide: data-background="#ffffff" -->

### Merge conflicts, example

<!-- .slide: style="font-size: 30px;" -->

Let's create a merge conflict:

```shell
$ mkdir merge-test
$ cd merge-test/
$ git init
$ echo "Initial content" > myfile.txt
$ git add myfile.txt
$ git commit -m "first commit"

$ git checkout -b feature_1
$ echo "Feature 1 is a good implementation" >> myfile.txt
$ git commit -a -m "start work on feature 1"

$ git checkout master
$ echo "Working on a really cool feature" >> myfile.txt
$ git commit -a -m "start work on a cool feature" 
```

---

<!-- .slide: data-background="#ffffff" -->
<!-- .slide: style="font-size: 30px;" -->


We now have two branches, **master** and **feature_1**:

```shell
$ git log --all --graph --decorate --oneline
* d8e6809 (HEAD -> master) start work on a cool feature
| * 87934eb (feature_1) start work on feature 1
|/  
* ce7e46c first commit
```

What are the contents of **myfile.txt** in the two branches?
```shell
$ git diff master feature_1 -- myfile.txt
diff --git a/myfile.txt b/myfile.txt
index b14ae98..5390ea7 100644
--- a/myfile.txt
+++ b/myfile.txt
@@ -1,2 +1,2 @@
 Initial content
-Working on a really cool feature
+Feature 1 is a good implementation
```
Or use the **git show <ref>:<path>** command:
```
$ git show master:myfile.txt
Initial content
Working on a really cool feature
$ git show feature_1:myfile.txt
Initial content
Feature 1 is a good implementation
```


---

<!-- .slide: data-background="#ffffff" -->

<!-- .slide: style="font-size: 30px;" -->

Let's try to merge the **feature_1** branch on to the **master** branch:
    
```shell
$ $ git merge feature_1
Auto-merging myfile.txt
CONFLICT (content): Merge conflict in myfile.txt
Automatic merge failed; fix conflicts and then commit the result.
```

The merge failed due to a conflict. In this case, the conflict arises because there are changes in the same line on both branches.

---

<!-- .slide: data-background="#ffffff" -->

<!-- .slide: style="font-size: 28px;" -->

We can get some more information with the **git status** command: 

```shell
$ git status
On branch master
You have unmerged paths.
  (fix conflicts and run "git commit")
  (use "git merge --abort" to abort the merge)

Unmerged paths:
  (use "git add <file>..." to mark resolution)
	both modified:   myfile.txt

no changes added to commit (use "git add" and/or "git commit -a")
```

Let's check the file that lead to the conflict, note the "conflict dividers":
```shell
$ cat myfile.txt 
Initial content
<<<<<<< HEAD
Working on a really cool feature
=======
Feature 1 is a good implementation
>>>>>>> feature_1

```
One can abort the merge with **git merge --abort**.
Or one may try to solve the conflict..

---

<!-- .slide: data-background="#ffffff" -->

## Resolving merge conflicts 

<!-- .slide: style="font-size: 28px;" -->

- The most direct way to resolve the conflict is to edit the file yourself and stage it. 
- When this has been done, you can attempt the merge again with:
```shell
$ git merge --continue
```


    

Helpful commands:
- identify conflicting files: `git status`

- list the conflicting commits among the branches: `git log --merge`

- find differences between the commits involved in the merge: `git diff` 

- reset conflicted files to a known good state: `git reset` 


If you made a mistake when you resolved a conflict and have completed the merge before realizing, you can roll back to the commit before the merge was done with the command `git reset --hard`. 


---

<!-- .slide: data-background="#ffffff" -->

## Workflow - merge goes well

<!-- .slide: style="font-size: 32px;" -->

- Work on files
- Stage files
- Commit files
- Then do
```shell
$ git merge <branch>
``` 

Success!

---

<!-- .slide: data-background="#ffffff" -->

## Workflow - merge goes badly 

<!-- .slide: style="font-size: 30px;" -->

- Work on files
- Stage files
- Commit files
- Then do
```shell
$ git merge <branch>
```
- CONFLICT!
- Fix problems
- Stage files
- Attempt the merge again:
```shell
$ git merge --continue
```
Success!

---

<!-- .slide: data-background="#ffffff" -->

## Rebasing

<!-- .slide: style="font-size: 32px;" -->

- Rebasing is the process of moving or combining a sequence of commits to a new base commit. 
- It solves the same problem as git merge. The commands are both used to integrate changes from one branch into another branch, however the way they do it is very different.
- When you do a rebase, all the changes will be compressed together in a single "patch" which is then "applied" - rebasing creates new commits on the other branch for each commit in the original branch. 

---

<!-- .slide: data-background="#ffffff" -->

### Rebasing - illustration 

<!-- .slide: style="font-size: 28px;" -->

Branch 'bugfix' was branched from 'master' 
```graphviz
digraph {
  rankdir=LR
  "commit2" -> "commit1"
  "commit3" -> "commit2"
  "commit4" -> "commit3"
  "commitX" -> "commit2"
  "master" -> "commit4" [style=dashed]
  "bugfix" -> "commitY" [style=dashed]
  "commitY" -> "commitX"
  master [shape=plaintext]
  "bugfix" [shape=plaintext]
  "HEAD" -> "bugfix" [style=dashed]
  HEAD [shape=plaintext]

}
```


Rebasing 'bugfix' onto the 'master' branch
```graphviz
digraph {
  rankdir=LR
  splines="line"
  "commit2" -> "commit1"
  "commit3" -> "commit2"
  "master" -> "commitY'" [style=dashed]
  "commit4" -> "commit3"
  "commitX'" -> "commit4"
  "commitY'" -> "commitX'"
  master [shape=plaintext]
  "HEAD" -> "master" [style=dashed]
  HEAD [shape=plaintext]

}
```

---

<!-- .slide: data-background="#ffffff" -->

### Rebasing - continued

<!-- .slide: style="font-size: 30px;" -->

Assume a master branch and the branch "cool-features" and that you want to rebase the branch "cool-features" onto the master branch: 

```shell
$ git checkout cool-features
$ git rebase master
```

This works by

* going to the common ancestor of the two branches
* getting the diff introduced by each commit of the branch you are on
* saving those diffs to temporary files
* resetting the current branch to the same commit as the branch you are rebasing onto
* apply each change in turn

---

<!-- .slide: data-background="#ffffff" -->

## Cherry-picking

<!-- .slide: style="font-size: 30px;" -->

Basically, cherry-picking in Git means that you choose a commit from one branch that you apply to another. 

Find the hash for the commit you want to apply, using `git log`.

Then make sure you are on the right branch that you want to apply the commit to: 

```shell
$ git checkout <branch>
```
Now you execute the cherry-picking: 
```shell
$ git cherry-pick <hash>
```

---

<!-- .slide: data-background="#ffffff" -->

### Cherry-picking — illustration

<!-- .slide: style="font-size: 28px;" -->

Let's assume we have:

```graphviz
digraph {
  rankdir=LR
  "commitY" -> "commitX"
  "commitZ" -> "commitY"
  "master" -> "commit3" [style=dashed]
  "feature" -> "commitZ" [style=dashed]
  "HEAD" -> "master" [style=dashed]

  "commit2" -> "commit1"
  "commitX" -> "commit2"
  "commit3" -> "commit2"
  
  master [shape=plaintext]
  feature [shape=plaintext]
  HEAD [shape=plaintext]
 
}
```

    
Applying the commit Y to master  with `git cherry-pick <hash>` will result in a new commit Y´.

```graphviz
digraph {
  rankdir=LR
  "commitY" -> "commitX"
  "commitZ" -> "commitY"
  "master" -> "commitY'" [style=dashed]
  "feature" -> "commitZ" [style=dashed]
  "HEAD" -> "master" [style=dashed]

  "commit2" -> "commit1"
  "commitX" -> "commit2"
  "commit3" -> "commit2"
  "commitY'" -> "commit3"
  
  master [shape=plaintext]
  feature [shape=plaintext]
  HEAD [shape=plaintext]

}
```

---

<!-- .slide: data-background="#ffffff" -->

## Take aways
<!-- .slide: style="font-size: 24px;" -->

- create or parse branch - `git branch`
- switch branch - `git checkout` or `git switch`
- merge branches - `git merge` 
- rebase branch  - `rebase` - like merge but end result is just one branch


**Conflict?**
- `commit` or `stash` or discard (`clean`) the changes before switching branch or do a ``checkout --merge`` .

**Workflow merge**
- Work on files 
- Stage and commit files 
- Then do: `git merge <branch>`

Conflict?
  - Fix problems 
  - Stage modifications 
  - Then do: `git merge --continue`


---

<!-- .slide: data-background="#ffffff" -->

## Exercises
<!-- .slide: style="font-size: 32px;" -->

Each of the exercises has a README.md file with explanations and descriptions of what to do. You can find all of them in the subdirectory 5.branches. You should do them in the below order: 
 
1. Fast-forward Merge (OK): This exercise will show an example where git can do a fast-forward merge. The exercise is in the subdirectory "1.merge-ok" 

2. Recursive/ORT Merge (OK): In this exercise you will see an example where git can automatically merge two branches. This time git will use the recursive merge. The exercise can be found in the subdirectory "2.merge-ok-recursive" 

---

<!-- .slide: data-background="#ffffff" -->

### Exercises

<!-- .slide: style="font-size: 32px;" -->
 
3. Merge (BAD): This exercise gives an example of a merge that cannot be done automatically with the merge command. The exercise can be found in the subdirectory "3.merge-bad" 

4. Rebasing (OK): In this exercise you will try the command rebase and see that it succeeds. The exercise can be found in the subdirectory "4.rebase-ok"  

5. Rebasing (BAD): This exercise again gives an example of rebasing two branches, but in this case the rebase fails. The exercise can be found in the subdirectory "5.rebase-bad" 

---
