# Rebase two local branches resulting in a conflict - model solutions  

This exercise will again let you rebase two branches, using the command `git rebase`. In this case the rebase will fail. 

Situation: In the branch "metric" we change the recipe to use the metric system for measurements. Then we switch back to the "master" branch and **add some coffee** to that version of the recipe.

You should make sure you are in the sub-directory "recipes" when you give the git commands. 

1. Check status and history with `git status` and `git log` first, including with the following flags to `git log`: 

   ```
   $ git log --oneline --abbrev-commit --all --graph
   ```

**Solution**

```shell
bbrydsoe@enterprise-a:~/course-intro-git/git_materials/5.branches/5.rebase-bad/recipes$ git status
On branch master
nothing to commit, working tree clean
bbrydsoe@enterprise-a:~/course-intro-git/git_materials/5.branches/5.rebase-bad/recipes$ git log --oneline --abbrev-commit --all --graph
* 1d6565c (HEAD -> master) Add 2 tsp of coffee powder.
| * f76e998 (metric) Change from imperial units to metric units.
|/  
* 03fbf09 Add ingredients and directions
* f9cc1ee This is going to be a cake recipe
``` 

2. Try to rebase the "master" branch to the "metric" branch using the `git rebase` command and see that a conflict happens. 

   NOTE: Remember to check with `git branch` to find out if you are on the right branch before trying to rebase. 

   You will get an error similar to this: 

   ```
   $ git rebase master
   First, rewinding head to replay your work on top of it...
   Applying: Change from imperial units to metric units.
   Using index info to reconstruct a base tree...
   M    	cakerecipe.txt
   Falling back to patching base and 3-way merge...
   Auto-merging cakerecipe.txt
   CONFLICT (content): Merge conflict in cakerecipe.txt
   error: Failed to merge in the changes.
   Patch failed at 0001 Change from imperial units to metric units.
   Use 'git am --show-current-patch' to see the failed patch

   Resolve all conflicts manually, mark them as resolved with
   "git add/rm <conflicted_files>", then run "git rebase --continue".
   You can instead skip this commit: run "git rebase --skip".
   To abort and get back to the state before "git rebase", run "git rebase --abort".
   ```

**Solution** 

Let us check what branch we are on first. Finding that we are on the 'master' branch, we switch to the 'metric' branch, then do the rebase (or try to): 

```shell
bbrydsoe@enterprise-a:~/course-intro-git/git_materials/5.branches/5.rebase-bad/recipes$ git branch
* master
  metric
bbrydsoe@enterprise-a:~/course-intro-git/git_materials/5.branches/5.rebase-bad/recipes$ git checkout metric
Switched to branch 'metric'
bbrydsoe@enterprise-a:~/course-intro-git/git_materials/5.branches/5.rebase-bad/recipes$ git rebase master
First, rewinding head to replay your work on top of it...
Applying: Change from imperial units to metric units.
Using index info to reconstruct a base tree...
M	cakerecipe.txt
Falling back to patching base and 3-way merge...
Auto-merging cakerecipe.txt
CONFLICT (content): Merge conflict in cakerecipe.txt
error: Failed to merge in the changes.
Patch failed at 0001 Change from imperial units to metric units.
hint: Use 'git am --show-current-patch' to see the failed patch
Resolve all conflicts manually, mark them as resolved with
"git add/rm <conflicted_files>", then run "git rebase --continue".
You can instead skip this commit: run "git rebase --skip".
To abort and get back to the state before "git rebase", run "git rebase --abort".
```

CONFLICT!

Let us try the command 'git am --show-current-patch': 

![](https://github.com/hpc2n/course-intro-git/blob/main/exercises-solutions/5.branches/5.rebase-bad/git-rebase-fail.png)

This shows the conflicts. 

3. Use `git log` (with the above flags) and `git status` to see where the problems are. See if you can fix the conflict and then reattempt the rebase.

**Solution**

```shell
bbrydsoe@enterprise-a:~/course-intro-git/git_materials/5.branches/5.rebase-bad/recipes$ git status
rebase in progress; onto 1d6565c
You are currently rebasing branch 'metric' on '1d6565c'.
  (fix conflicts and then run "git rebase --continue")
  (use "git rebase --skip" to skip this patch)
  (use "git rebase --abort" to check out the original branch)

Unmerged paths:
  (use "git restore --staged <file>..." to unstage)
  (use "git add <file>..." to mark resolution)
	both modified:   cakerecipe.txt

no changes added to commit (use "git add" and/or "git commit -a")
bbrydsoe@enterprise-a:~/course-intro-git/git_materials/5.branches/5.rebase-bad/recipes$ git log --oneline --abbrev-commit --all --graph
* 1d6565c (HEAD, master) Add 2 tsp of coffee powder.
| * f76e998 (metric) Change from imperial units to metric units.
|/  
* 03fbf09 Add ingredients and directions
* f9cc1ee This is going to be a cake recipe
```

It is also worth noting that you are currently in the "detached head" mode: 

```shell
bbrydsoe@enterprise-a:~/course-intro-git/git_materials/5.branches/5.rebase-bad/recipes$ git branch
* (no branch, rebasing metric)
  master
  metric
```

You now have three options: 

1) Run 'git rebase --abort' to undo the rebase. You will then be in the state before 'git rebase' was called.
2) Run 'git rebase --skip' to skip the commit. This means you will not include ANY of the changes that was in the conflicting commit. This is VERY rarely the case. 
3) You can fix the conflict.

We will try to fix the conflict, by editing the offending file, cakerecipe.txt: 

1) Edit the file 'cakerecipe.txt', removing/changing until you keep the lines you want. 
2) Stage the file again with 'git add cakerecipe.txt'
3) You can now continue the rebase 

```shell
bbrydsoe@enterprise-a:~/course-intro-git/git_materials/5.branches/5.rebase-bad/recipes$ git rebase --continue
Applying: Change from imperial units to metric units.
``` 

Let us check that all is well: 

```shell
bbrydsoe@enterprise-a:~/course-intro-git/git_materials/5.branches/5.rebase-bad/recipes$ git status
On branch metric
nothing to commit, working tree clean
bbrydsoe@enterprise-a:~/course-intro-git/git_materials/5.branches/5.rebase-bad/recipes$ git log --oneline --abbrev-commit --all --graph
* a67a03a (HEAD -> metric) Change from imperial units to metric units.
* 1d6565c (master) Add 2 tsp of coffee powder.
* 03fbf09 Add ingredients and directions
* f9cc1ee This is going to be a cake recipe
```

Problem solved! 

There are other ways to solve a conflict during git rebase; you could choose to accept all the conflicting commits from one or the other branch, or you could try and auto-resolve the conflict (which could be dangerous, even if it seems to go through). 

You can read more about resolving conflicts during a git rebase here: https://codeinthehole.com/guides/resolving-conflicts-during-a-git-rebase/ 

