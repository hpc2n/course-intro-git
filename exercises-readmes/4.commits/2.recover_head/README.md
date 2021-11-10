# Recovering the HEAD

The goal of this exercise is to learn to identify a "detached HEAD" situation
and recover from it. Enter the `repository/` directory and perform the following
steps:

 1. Enter the `repository/` directory and check whether the HEAD is detached. 
 
 2. If the HEAD is detached, return the `HEAD` back to the tip of the branch. 
 
 3. Confirm that that the `HEAD` indeed points to the tip of the branch`

Hints:

 - git checkout <ref>
 - rev-parse
 - cat .git/something
