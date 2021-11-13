# Rebase two local branches

In this exercise you will try to use the command `git rebase`. You will see that it succeeds. 

Situation: The ingredient list in branch "master" has an error in the ingredients which is fixed in the branch "fixed-recipe". Then we decide to make a small change to the recipe, and we do it in the "master" branch. 

You should make sure you are in the sub-directory "recipes" when you give the git commands. 

1. First do a `git status` and a `git log` and look at the results. Also look at the output at the longer command: 

   ```
   $ git log --oneline --abbrev-commit --all --graph
   ```

   And save the result somewhere for later comparison. 

2. Now try to rebase the "master" with the new branch, "fixed-recipe". You will see that the rebase succeeds.  

   NOTE: Remember to check with `git branch` that you are on the right branch before you try to rebase! 

3. You should now validate the operation with `git log` and `git status`.

   Also run `git log` with the following flags:  

   ```
   $ git log --oneline --abbrev-commit --all --graph
   ```

