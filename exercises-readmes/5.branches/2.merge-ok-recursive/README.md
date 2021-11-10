# Merging two local branches, recursive

In this exercise you will again try the command `git merge` and it should again go well. However, this time git will do a recursive merge. 

Situation: The ingredient list in branch "master" has an error in the ingredients which is fixed in the branch "fixed-recipes". After that fix, a small change was made to the recipe in the "master" branch.

You should make sure you are in the sub-directory "recipes" when you give the git commands. 

1. First do `git status` to look at the status. Also run `git log` and see the commits that  have been made and to which branches. 

2. Now try to merge the two branches. You will see that the merge happens with "recursive" merge. 

   NOTE: Remember to check you are on the right branch before you try to merge! 

   Merge the branch "fixed-recipe" to the "master" branch using the `git merge`command. 

3. Notice that the merge goes well and that git reports using "recursive" merge. 
4. Do `git log`and `git status` after the merge and compare with what you got before. 

5. Why did git use "recursive" merge? 
