# Merging two local branches resulting in a merge conflict - model solutions 

This exercise will again feature the command `git merge`, but this time the merge will fail and git will give a merge conflict. 

Situation: In the branch "metric" we change the recipe to use the metric system for measurements. Then we change back to the "master" branch and **add some coffee** to that version of the recipe.

You should make sure you are in the sub-directory "recipes" when you give the git commands. 

1. Do a `git status`first and note the result. Run `git log`. You could also look at the output from the longer command: 
   
   ```
   $ git log --oneline --abbrev-commit --all --graph
   ```

   NOTE: Remember to change to the subdirectory "recipes" first!

**Solution**

```shell
bbrydsoe@enterprise-a:~/course-intro-git/git_materials/5.branches/3.merge-bad/recipes$ git status
On branch master
nothing to commit, working tree clean
bbrydsoe@enterprise-a:~/course-intro-git/git_materials/5.branches/3.merge-bad/recipes$ git log --graph --oneline --abbrev-commit --all
* 1d6565c (HEAD -> master) Add 2 tsp of coffee powder.
| * f76e998 (metric) Change from imperial units to metric units.
|/  
* 03fbf09 Add ingredients and directions
* f9cc1ee This is going to be a cake recipe
```

2. Now try to merge the two branches with the `git merge` command and see that a conflict happens. 

   NOTE: Check with `git branch` to find out if you are on the right branch before trying to merge.

   You will get an error similar to this: 

   ```
   $ git merge metric
   Auto-merging cakerecipe.txt
   CONFLICT (content): Merge conflict in cakerecipe.txt
   Automatic merge failed; fix conflicts and then commit the result.
   ```

**Solution**

```shell
bbrydsoe@enterprise-a:~/course-intro-git/git_materials/5.branches/3.merge-bad/recipes$ git branch
* master
  metric
bbrydsoe@enterprise-a:~/course-intro-git/git_materials/5.branches/3.merge-bad/recipes$ git merge metric
Auto-merging cakerecipe.txt
CONFLICT (content): Merge conflict in cakerecipe.txt
Automatic merge failed; fix conflicts and then commit the result.
```

3. Use `git log` (including with the above mentioned flags) and `git status` to see where the problems are and see if you can fix the conflict and then reattempt the merge.

**Solution**

```shell
bbrydsoe@enterprise-a:~/course-intro-git/git_materials/5.branches/3.merge-bad/recipes$ git status
On branch master
You have unmerged paths.
  (fix conflicts and run "git commit")
  (use "git merge --abort" to abort the merge)

Unmerged paths:
  (use "git add <file>..." to mark resolution)
	both modified:   cakerecipe.txt

no changes added to commit (use "git add" and/or "git commit -a")
bbrydsoe@enterprise-a:~/course-intro-git/git_materials/5.branches/3.merge-bad/recipes$ git log --graph --oneline --abbrev-commit --all
* 1d6565c (HEAD -> master) Add 2 tsp of coffee powder.
| * f76e998 (metric) Change from imperial units to metric units.
|/  
* 03fbf09 Add ingredients and directions
* f9cc1ee This is going to be a cake recipe
```

The file 'cakerecipe.txt' is modified on both branches. You can solve this conflict in a number of ways: 
1) You could do "git merge --abort" to abort the merge and then perhaps undo the changes on one of the branches. 
2) You could manually fix the conflict. This is the option we are going to go with here. 

To fix the conflict, there are a few options (2, 3, 4 all basically reverts to you having to do the changes manually): 
1) Use 'git mergetool' to launch a graphical mergetool. This will help you go through the steps of the merge. you will need to configure mergetool before using it. 
2) Look at the diffs. The command git diff will show a three-way diff. The changes from the versions will be highlighted. Fix the conflicts in the file(s). 
3) Look at the diffs from each branch. The command git log --merge -p <path> will first give diffs for the HEAD of the branch you are on, then for the HEAD of the branch you are merging. 
4) Open the conflicting file and look at the problems directly. If it is just a small number of conflicts, this is the easiest. 

Here we will do option 4) so open the file 'cakerecipe.txt' in your editor of choice. Find the problematic areas: 

```shell
# Maraschino Devil's Food Cake

## Ingredients

 - 250 g sifted cake flour
 - 1 teaspoon soda
 - 2 eggs
<<<<<<< HEAD
 - 2 tsp instant coffee powder
 - 1 1/3 cup sugar
 - 1/2 cup snowdrift
 - 1/2 cup buttermilk
 - 1/4 cup Maraschino cherry juice
 - 1/2 cup chopped Marachino cherries
=======
 - 275 g sugar
 - 125 g snowdrift or butter
 - 120 ml buttermilk
 - 60 ml Maraschino cherry juice
 - 1 dl chopped Marachino cherries
>>>>>>> metric
 - 2 squares unsweetened chocolate, melted and cooled

## Directions

 1. All ingredients mixed in same bowl.
 2. Mixing time three minutes.
 3. Sift together in large bowl flour, soda, and sugar.
 4. Add snowdrift, buttermilk and cherry juice.
 5. Mix enough to dampen flow; beat 2 minutes-if by hand, count beating time
    only; with electric mixer use low speed, beating 2 minutes.
 6. Add eggs and chocolate.
<<<<<<< HEAD
 7. Mix in the instant coffee powder.
 8. Beat 1 minute for snowdrift, smooth batter, then fold in 1/2 cup chopped
    cherries dusted with flour.
 9. Bake in two greased 9-inch layer pans lined with paper at 325f about 35 minutes.
10. Frost with fondant icing.
=======
 7. Beat 1 minute for snowdrift, smooth batter, then fold in 1 dl chopped
    cherries dusted with flour.
 8. Bake in two greased 23cm layer pans lined with paper at 175C about 35
    minutes.
 9. Frost with fondant icing.
>>>>>>> metric
```

As you can see, they are clearly marked in the file. The stuff listed after '<<<<<<< HEAD' is how it looks on the 'master' branch (where you currently are), then come a divider '=======' and then follows how it looks on the branch 'metric'. There are two sections of the file which have been changed, and the changes are not compatible. You will have to manually pick one or the other (or a combination), as Git does not have a way of knowing which one you would prefer. 

When you have removed the stuff you do not want, also remove the dividers (equality-signs and angle brackets, etc.) 

When you have edited the file to your liking, again stage and commit: 

```shell
bbrydsoe@enterprise-a:~/course-intro-git/git_materials/5.branches/3.merge-bad/recipes$ git add cakerecipe.txt 
bbrydsoe@enterprise-a:~/course-intro-git/git_materials/5.branches/3.merge-bad/recipes$ git commit -m "Fixed conflicts, I think"
[master 562b10c] Fixed conflicts, I think
```

Now all is well: 

```shell
bbrydsoe@enterprise-a:~/course-intro-git/git_materials/5.branches/3.merge-bad/recipes$ git merge metric
Already up-to-date.
bbrydsoe@enterprise-a:~/course-intro-git/git_materials/5.branches/3.merge-bad/recipes$ git status
On branch master
nothing to commit, working tree clean
bbrydsoe@enterprise-a:~/course-intro-git/git_materials/5.branches/3.merge-bad/recipes$ git branch
* master
  metric
bbrydsoe@enterprise-a:~/course-intro-git/git_materials/5.branches/3.merge-bad/recipes$ git log --graph --oneline --abbrev-commit --all
*   562b10c (HEAD -> master) Fixed conflicts, I think
|\  
| * f76e998 (metric) Change from imperial units to metric units.
* | 1d6565c Add 2 tsp of coffee powder.
|/  
* 03fbf09 Add ingredients and directions
* f9cc1ee This is going to be a cake recipe
```

