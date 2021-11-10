# Proper commit workflow

This exercise is meant to demonstrate the proper workflow for making multiple
commits from a **single set of edits**. The overall goal is to make sure that
each commit produces a valid revision. This type of workflow is beneficial when
working with source code since each revision should both compile and function
correctly. The workflow is not that beneficial with the the example below but
it is used as an example only.

Enter the `repository/` directory and perform the following steps:

 1. You can confirm (`git diff HEAD`) that the `repository/recipe.txt` file
    contains uncommitted changes. That is, the recipe have been converted to
    metric system.

 2. You can also confirm (`git diff --cached`) that some of these changes have
    been already staged. 
    
    As you can probably guess, the **first commit** we are creating is going to
    convert the measurements to metric.
    
    The changes that are related to the pan size and the oven temperature (8th
    step the the directions) are going to be committed **separately**.

 3. Store the the unstaged changes to the stash:
 
    ```
    $ git stash --keep-index
    ```
    
    The `--keep-index` options tells Git to keep the staged changes. Otherwise
    Git would stash them.

 4. Now, investigate the content of the `repository/recipe.txt` file. You can
    see that the 7th step in the directions contains an unconverted measurement.
    This means that whoever created this exercise forgot to stage this line.
    This would correspond to a situation where the source code does not compile
    or does not function correctly.

 5. Pop the unstaged changes from the stash:
 
    ```
    $ git stash pop
    ```
    
 6. Stage the 7th step in the directions and stash the unstaged changes while
    keeping the index. 
    
    Remember to do partial staging (Lecture 3: Basic commands).
    
    Verify the `repository/recipe.txt` file.

 7. Commit changes.
 
 8. Pop the unstaged changes, and stage and commit changes that are related to
    the pan size and the oven temperature. 
    
    This is going to be the **second commit**.

Confirm that the two commits you created indeed contain the desired changes.
