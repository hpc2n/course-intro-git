# Merging two local branches - model solutions

The purpose of this exercise is to test the command `git merge` and see that the merge goes well in this case. 

Situation: The ingredient list in branch "master" has an error in the ingredients which is fixed in the branch "fixed-recipe".

You should make sure you are in the sub-directory "recipes". 

1. First do `git status` to look at the status. You can also run `git log` so you can compare before and after merging. 

**Solution**

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

**Solution**

Check which branch you are on. You will find that you are on branch 'fixed-recipe'. Switch to branch 'master' and then merge the 'fixed-recipe' branch to that. 

```shell
bbrydsoe@enterprise-a:~/course-intro-git/git_materials/5.branches/1.merge-ok/recipes$ git branch
* fixed-recipe
  master
bbrydsoe@enterprise-a:~/course-intro-git/git_materials/5.branches/1.merge-ok/recipes$ git checkout master
Switched to branch 'master'
bbrydsoe@enterprise-a:~/course-intro-git/git_materials/5.branches/1.merge-ok/recipes$ git merge fixed-recipe
Updating a92cf6f..2ab3c6e
Fast-forward
 cakerecipe.txt | 2 +-
 1 file changed, 1 insertion(+), 1 deletion(-)
```

3. See that the merge goes well, and that git reports using "fast-forward" merge. 

**Solution** 

Done above. 

4. Do `git log` and `git status` after the merge and compare what you got before.

**Solution** 

You are now on branch 'master' as you can see, and it has the changes. 

```shell
bbrydsoe@enterprise-a:~/course-intro-git/git_materials/5.branches/1.merge-ok/recipes$ git status
On branch master
nothing to commit, working tree clean
bbrydsoe@enterprise-a:~/course-intro-git/git_materials/5.branches/1.merge-ok/recipes$ git log --graph --oneline --decorate --all
* 2ab3c6e (HEAD -> master, fixed-recipe) Fix error in recipe - 1 egg should be 2 eggs
* a92cf6f Add ingredients and directions
* f9cc1ee This is going to be a cake recipe
```

5. Think about why git could merge the two braches automatically and why it used "fast-forward" merge. 

**Solution** 

The change was only made on the 'fixed-recipe' branch, so there was no risk of conflict. 

Remember: 
Fast Forward Merge - the commit history is one straight line. You create a branch, you make some commits there, but no changes to the ‘master’. You then just merge onto the ‘master’. This just moves the pointer for the ‘master’ branch forward in a straight line. 

