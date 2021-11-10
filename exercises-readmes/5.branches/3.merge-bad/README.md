# Merging two local branches resulting in a merge conflict 

This exercise will again feature the command `git merge`, but this time the merge will fail and git will give a merge conflict. 

Situation: In the branch "metric" we change the recipe to use the metric system for measurements. Then we change back to the "master" branch and **add some coffee** to that version of the recipe.

You should make sure you are in the sub-directory "recipes" when you give the git commands. 

1. Do a `git status`first and note the result. Run `git log`. You could also look at the output from the longer command: 
   
   ```
   $ git log --oneline --abbrev-commit --all --graph
   ```

   NOTE: Remember to change to the subdirectory "recipes" first!


2. Now try to merge the two branches with the `git merge` command and see that a conflict happens. 

   NOTE: Check with `git branch` to find out if you are on the right branch before trying to merge.

   You will get an error similar to this: 

   ```
   $ git merge metric
   Auto-merging cakerecipe.txt
   CONFLICT (content): Merge conflict in cakerecipe.txt
   Automatic merge failed; fix conflicts and then commit the result.
   ```

3. Use `git log` (including with the above mentioned flags) and `git status` to see where the problems are and see if you can fix the conflict and then reattempt the merge.

