# Exercises - Branches, merges, and conflicts 

In order to do these exercises, you need to download the exercises zip file (if you already did so for the previous exercise, you do not need to do so again, of course). 

You can do that either by cloning the repository or by just getting the zip file with `wget`.

- Do ONE of the following:
    - **git clone**
        1. ``git clone https://github.com/hpc2n/course-intro-git.git``
        2. ``cd course-intro-git``
        3. ``unzip git_materials.zip``
        4. ``cd git_materials``
        5. ``cd 5.branches`` 
    - **Fetch with wget**
        1. ``wget https://github.com/hpc2n/course-intro-git/raw/refs/heads/main/git_materials.zip`` 
        2. ``unzip git_materials.zip``
        3. ``cd git_materials``
        4. ``cd 4.branches``

You are now in a directory with 5 subdirectories, one for each exercise.

## 1. Merging two local branches

!!! note 

    The purpose of this exercise is to test the command `git merge` and see that the merge goes well in this case. 

    **Situation:** The ingredient list in branch "master" has an error in the ingredients which is fixed in the branch "fixed-recipe".

Start by making sure you are in the directory `git_materials/5.branches/1.merge-ok/recipes`. 

1. First do `git status` to look at the status. You can also run `git log` so you can compare before and after merging. 
2. Now try to merge the two branches. You will see that it merges with a "fast-forward" merge. <br>
   NOTE: Remember to check that you are on the right branch! Use `git branch` to check. <br>
   Merging the branch "fixed-recipe" to the "master" branch: 
   ```
   git merge fixed-recipe
   ```
   <br>
3. See that the merge goes well, and that git reports using "fast-forward" merge. <br>
4. Do `git log` and `git status` after the merge and compare what you got before.<br>
5. Think about why git could merge the two braches automatically and why it used "fast-forward" merge. 

## 2. Merging two local branches, recursive 

!!! note 

    In this exercise you will again try the command `git merge` and it should again go well. However, this time git will do a recursive merge, or in newer version an "ort" merge.

    **Situation:** The ingredient list in branch "master" has an error in the ingredients which is fixed in the branch "fixed-recipes". After that fix, a small change was made to the recipe in the "master" branch. 

Start by making sure you are in the directory `git_materials/5.branches/2.merge-ok-recursive/recipes`. 

1. First do `git status` to look at the status. Also run `git log` and see the commits that  have been made and to which branches. <br>
2. Now try to merge the two branches. You will see that the merge happens with "recursive" merge. <br>
   NOTE: Remember to check you are on the right branch before you try to merge!    <br>
   Merge the branch "fixed-recipe" to the "master" branch using the `git merge`command. 
   <br>
3. Notice that the merge goes well and that git reports using "recursive" merge. <br>
4. Do `git log`and `git status` after the merge and compare with what you got before.<br> 
5. Why did git use "recursive" merge? 

## 3. Merging two local branches resulting in a merge conflict 

!!! note 

    This exercise will again feature the command `git merge`, but this time the merge will fail and git will give a merge conflict. 

    **Situation:** In the branch "metric" we change the recipe to use the metric system for measurements. Then we change back to the "master" branch and **add some coffee** to that version of the recipe.

Start by making sure you are in the directory `git_materials/5.branches/3.merge-bad/recipes`. 

1. Do a `git status`first and note the result. Run `git log`. You could also look at the output from the longer command: 
   <br>   
   ```
   $ git log --oneline --abbrev-commit --all --graph
   ```
   or with the alias command `git graph`
   <br>
   NOTE: Remember to change to the subdirectory "recipes" first!
   <br>
2. Now try to merge the two branches with the `git merge` command and see that a conflict happens. 
   <br>
   NOTE: Check with `git branch` to find out if you are on the right branch before trying to merge.
   <br>
   You will get an error similar to this: 
   <br>
   ```
   $ git merge metric
   Auto-merging cakerecipe.txt
   CONFLICT (content): Merge conflict in cakerecipe.txt
   Automatic merge failed; fix conflicts and then commit the result.
   ```
   <br>
3. Use `git log` (including with the above mentioned flags) and `git status` to see where the problems are and see if you can fix the conflict and then reattempt the merge.

## 4. Rebase two local branches

!!! note 

    In this exercise you will try to use the command `git rebase`. You will see that it succeeds. 

    **Situation:** The ingredient list in branch "master" has an error in the ingredients which is fixed in the branch "fixed-recipe". Then we decide to make a small change to the recipe, and we do it in the "master" branch. 

Start by making sure you are in the directory `git_materials/5.branches/4.rebase-ok/recipes`. 

1. First do a `git status` and a `git log` and look at the results. Also look at the output at the longer command (git graph): 
   <br>
   ```
   $ git log --oneline --abbrev-commit --all --graph
   ```
   <br>
   And save the result somewhere for later comparison. 
   <br>
2. Now try to rebase the "master" with the new branch, "fixed-recipe". You will see that the rebase succeeds.  
   <br>
   NOTE: Remember to check with `git branch` that you are on the right branch before you try to rebase! 
   <br>
3. You should now validate the operation with `git log` and `git status`.
   <br>
   Also run `git graph` or `git log` with the following flags:  
   <br>
   ```
   $ git log --oneline --abbrev-commit --all --graph
   ```

## 5. Rebase two local branches resulting in a conflict

!!! note

    This exercise will again let you rebase two branches, using the command `git rebase`. In this case the rebase will fail. 

    **Situation:** In the branch "metric" we change the recipe to use the metric system for measurements. Then we switch back to the "master" branch and **add some coffee** to that version of the recipe.

Start by making sure you are in the directory `git_materials/5.branches/5.rebase-bad/recipes`. 

1. Check status and history with `git status` and `git graph` or `git log` first, including with the following flags to `git log`: 

   ```
   $ git log --oneline --abbrev-commit --all --graph
   ```
2. Try to rebase the "master" branch to the "metric" branch using the `git rebase` command and see that a conflict happens. 

   NOTE: Remember to check with `git branch` to find out if you are on the right branch before trying to rebase. 

   You will get an error more or less similar to this: 

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
<br>
3. Use `git log` (with the above flags) or `git graph`and `git status` to see where the problems are. See if you can fix the conflict and then reattempt the rebase.

