# Merging two local branches, recursive - model solutions

In this exercise you will again try the command `git merge` and it should again go well. However, this time git will do a recursive merge. 

Situation: The ingredient list in branch "master" has an error in the ingredients which is fixed in the branch "fixed-recipes". After that fix, a small change was made to the recipe in the "master" branch.

You should make sure you are in the sub-directory "recipes" when you give the git commands. 

1. First do `git status` to look at the status. Also run `git log` and see the commits that  have been made and to which branches. 

**Solution** 

```shell
bbrydsoe@enterprise-a:~/course-intro-git/git_materials/5.branches/2.merge-ok-recursive/recipes$ git status
On branch master
nothing to commit, working tree clean
bbrydsoe@enterprise-a:~/course-intro-git/git_materials/5.branches/2.merge-ok-recursive/recipes$ git log --graph --oneline --decorate --all
* 2ab3c6e (fixed-recipe) Fix error in recipe - 1 egg should be 2 eggs
| * 7d1b744 (HEAD -> master) Suggested a replacement for snowdrift
|/  
* a92cf6f Add ingredients and directions
* f9cc1ee This is going to be a cake recipe
```

2. Now try to merge the two branches. You will see that the merge happens with "recursive" merge. 

   NOTE: Remember to check you are on the right branch before you try to merge! 

   Merge the branch "fixed-recipe" to the "master" branch using the `git merge`command. 

**Solution**

Check what branch you are on:
```shell
bbrydsoe@enterprise-a:~/course-intro-git/git_materials/5.branches/2.merge-ok-recursive/recipes$ git branch
  fixed-recipe
* master
```

We are on branch 'master' so we go ahead and do the merge: 

```shell
bbrydsoe@enterprise-a:~/course-intro-git/git_materials/5.branches/2.merge-ok-recursive/recipes$ git merge fixed-recipe
```

Instead of doing the merge, it opens up an editor with this content: 

```shell
Merge branch 'fixed-recipe'
# Please enter a commit message to explain why this merge is necessary,
# especially if it merges an updated upstream into a topic branch.
#
# Lines starting with '#' will be ignored, and an empty message aborts
# the commit.
~
~                                                                                                            
~
```

If you want (you should), add something to the above message, then save and quit the editor (if it opened in vim as above, then open for editing by pushing the 'i' key, write what you want to write, then press the 'ESC' key to go to command-mode, then write ':wq' and press enter to save and quit).                    

You then get the following output on the screen: 
```shell
Auto-merging cakerecipe.txt
Merge made by the 'recursive' strategy.
```

So all went well. 

3. Notice that the merge goes well and that git reports using "recursive" merge. 

**Solution**

Done above. 

4. Do `git log`and `git status` after the merge and compare with what you got before. 

**Solution**

```shell
bbrydsoe@enterprise-a:~/course-intro-git/git_materials/5.branches/2.merge-ok-recursive/recipes$ git status
On branch master
nothing to commit, working tree clean
bbrydsoe@enterprise-a:~/course-intro-git/git_materials/5.branches/2.merge-ok-recursive/recipes$ git log --graph --oneline --decorate --all
*   5ec01dc (HEAD -> master) Merge branch 'fixed-recipe' Fixes to the recipe
|\  
| * 2ab3c6e (fixed-recipe) Fix error in recipe - 1 egg should be 2 eggs
* | 7d1b744 Suggested a replacement for snowdrift
|/  
* a92cf6f Add ingredients and directions
* f9cc1ee This is going to be a cake recipe
``` 

5. Why did git use "recursive" merge? 

**Solution**

There were changes on both branches, so it could not just do a fast-forward merge. 

Remember:
Recursive Merge - make a branch and make some commits there, but also make new commits made on the ‘master‘. Then, when you want to merge, git will recurse over the branch and create a new merge commit. The merge commit will continue to have two parents. 

