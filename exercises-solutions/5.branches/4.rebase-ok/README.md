# Rebase two local branches - model solutions 

In this exercise you will try to use the command `git rebase`. You will see that it succeeds. 

Situation: The ingredient list in branch "master" has an error in the ingredients which is fixed in the branch "fixed-recipe". Then we decide to make a small change to the recipe, and we do it in the "master" branch. 

You should make sure you are in the sub-directory "recipes" when you give the git commands. 

1. First do a `git status` and a `git log` and look at the results. Also look at the output at the longer command: 

   ```
   $ git log --oneline --abbrev-commit --all --graph
   ```

   And save the result somewhere for later comparison. 

**Solution**

```shell
bbrydsoe@enterprise-a:~/course-intro-git/git_materials/5.branches/4.rebase-ok/recipes$ git status
On branch master
nothing to commit, working tree clean
bbrydsoe@enterprise-a:~/course-intro-git/git_materials/5.branches/4.rebase-ok/recipes$ git log --oneline --abbrev-commit --all --graph
* 2ab3c6e (fixed-recipe) Fix error in recipe - 1 egg should be 2 eggs
| * 7d1b744 (HEAD -> master) Suggested a replacement for snowdrift
|/  
* a92cf6f Add ingredients and directions
* f9cc1ee This is going to be a cake recipe
```

2. Now try to rebase the "master" with the new branch, "fixed-recipe". You will see that the rebase succeeds.  

   NOTE: Remember to check with `git branch` that you are on the right branch before you try to rebase! 

**Solution**

First check that you are on the correct branch ('fixed-recipe'). It turns out you are on the 'master' branch, so you should switch to 'fixed-recipe'. When you have done that, do the rebase: 

```shell
bbrydsoe@enterprise-a:~/course-intro-git/git_materials/5.branches/4.rebase-ok/recipes$ git branch
  fixed-recipe
* master
bbrydsoe@enterprise-a:~/course-intro-git/git_materials/5.branches/4.rebase-ok/recipes$ git checkout fixed-recipe 
Switched to branch 'fixed-recipe'
bbrydsoe@enterprise-a:~/course-intro-git/git_materials/5.branches/4.rebase-ok/recipes$ git rebase master
First, rewinding head to replay your work on top of it...
Applying: Fix error in recipe - 1 egg should be 2 eggs
Using index info to reconstruct a base tree...
M	cakerecipe.txt
Falling back to patching base and 3-way merge...
Auto-merging cakerecipe.txt
No changes -- Patch already applied.
```

3. You should now validate the operation with `git log` and `git status`.

   Also run `git log` with the following flags:  

   ```
   $ git log --oneline --abbrev-commit --all --graph
   ```

**Solution**

```shell
bbrydsoe@enterprise-a:~/course-intro-git/git_materials/5.branches/4.rebase-ok/recipes$ git status
On branch fixed-recipe
nothing to commit, working tree clean
bbrydsoe@enterprise-a:~/course-intro-git/git_materials/5.branches/4.rebase-ok/recipes$ git log --oneline --abbrev-commit --all --graph
* 7d1b744 (HEAD -> fixed-recipe, master) Suggested a replacement for snowdrift
* a92cf6f Add ingredients and directions
* f9cc1ee This is going to be a cake recipe
``` 

Comparing with what you got under 1) you can see that the rebasing was successfull. 

