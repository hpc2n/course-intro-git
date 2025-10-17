# Exercises - Traversing the commit tree 

In order to do these exercises, you need to download the exercises zip file. You can do that either by cloning the repository or by just getting the zip file with `wget`.

- Do ONE of the following: 
    - **git clone** 
        1. ``git clone https://github.com/hpc2n/course-intro-git.git``
        2. ``cd course-intro-git``
        3. ``unzip git_materials.zip``
        4. ``cd git_materials``
        5. ``cd 4.commits`` 
    - **Fetch with wget**
        1. ``wget https://github.com/hpc2n/course-intro-git/raw/refs/heads/main/git_materials.zip``
        2. ``unzip git_materials.zip``
        3. ``cd git_materials``
        4. ``cd 4.commits``

You are now in a directory with 7 subdirectories, one for each exercise. 

## 1. Investigating the commit history

!!! note 

    The goal of this exercise is to learn to use the `git log` command. 

Found under `git_materials/4.commits/1.log` there is a directory named `repository`. Enter it and perform the following steps: 

1. Investigate the history. How many commit does the `main` branch contain?
2. Can you make the output of the command cleaner?
3. Are there any other branches? How many? What are they called?
4. Try to filter the output so that only commits that contain the word "abandon" in the commit message are shown.
5. Does the reference log contain anything interesting? Can you see where the `HEAD` was 6 steps ago?

!!! hint "Hints for this exercise"

    - oneline
    - graph
    - reflog

## 2. Recovering the HEAD 

!!! note 

    The goal of this exercise is to learn to identify a "detached HEAD" situation and recover from it. 

Enter the `repository/` directory under `git_materials/4.commits/2.recover_head` and perform the following steps:

1. Enter the `repository/` directory and check whether the HEAD is detached. 
2. If the HEAD is detached, return the `HEAD` back to the tip of the branch. 
3. Confirm that that the `HEAD` indeed points to the tip of the branch`

!!! tip "Hints for this exercise"

    - git checkout <ref>
    - rev-parse
    - cat .git/something

