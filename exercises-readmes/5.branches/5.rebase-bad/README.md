# Rebase two local branches resulting in a conflict 

This exercise will again let you rebase two branches, using the command `git rebase`. In this case the rebase will fail. 

Situation: In the branch "metric" we change the recipe to use the metric system for measurements. Then we switch back to the "master" branch and **add some coffee** to that version of the recipe.

You should make sure you are in the sub-directory "recipes" when you give the git commands. 

1. Check status and history with `git status` and `git log` first, including with the following flags to `git log`: 

   ```
   $ git log --oneline --abbrev-commit --all --graph
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

3. Use `git log` (with the above flags) and `git status` to see where the problems are. See if you can fix the conflict and then reattempt the rebase.


