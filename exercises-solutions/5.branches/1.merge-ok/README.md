# Merging two local branches - model solutions

The purpose of this exercise is to test the command `git merge` and see that the merge goes well in this case. 

Situation: The ingredient list in branch "master" has an error in the ingredients which is fixed in the branch "fixed-recipe".

You should make sure you are in the sub-directory "recipes". 

1. First do `git status` to look at the status. You can also run `git log` so you can compare before and after merging. 

```shell
bbrydsoe@enterprise-a:~/course-intro-git/git_materials/5.branches/1.merge-ok/recipes$ git status
On branch fixed-recipe
nothing to commit, working tree clean
bbrydsoe@enterprise-a:~/course-intro-git/git_materials/5.branches/1.merge-ok/recipes$ git log --graph --oneline --decorate --all
* 2ab3c6e (HEAD -> fixed-recipe) Fix error in recipe - 1 egg should be 2 eggs
* a92cf6f (master) Add ingredients and directions
* f9cc1ee This is going to be a cake recipe
```

2. Now try to merge the two branches. You will see that it merges with a "fast-forward" merge. 

   NOTE: Remember to check that you are on the right branch! Use `git branch` to check. 

   Merging the branch "fixed-recipe" to the "master" branch: 

   ```
   git merge fixed-recipe
   ```

3. See that the merge goes well, and that git reports using "fast-forward" merge. 

4. Do `git log` and `git status` after the merge and compare what you got before.

5. Think about why git could merge the two braches automatically and why it used "fast-forward" merge. 

