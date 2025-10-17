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

