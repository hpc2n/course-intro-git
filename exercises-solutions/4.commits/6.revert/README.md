# Revert the latest commit - with solutions

The goal of this exercise is to learn to revert the latest commit. Enter the
`repository/` directory and perform the following steps:

 1. Revert the latest commit.
 
 2. Confirm that the commit tree indeed contains the revert commit. Confirm
    that the `recipe.txt` file no longer contains the section "Other ideas
    and hints".


**Solution**

 1. Investigate the repository:

```shell
$ git log --oneline --graph --all
* 2690c4f (HEAD -> master) Add other ideas and hints
* 9552f3f Add directions
* 9b751b9 Add ingredients
* ddfe74e Better name for the cake
* d290aa4 This is going to be a cake recipe
$
$ git status
On branch master
nothing to commit, working tree clean
$
$ git revert HEAD
[master 52054bb] Revert "Add other ideas and hints"
 1 file changed, 4 deletions(-)
```

 2. Confirm the revert
```shell
$ git log --oneline --graph --all
* 52054bb (HEAD -> master) Revert "Add other ideas and hints"
* 2690c4f Add other ideas and hints
* 9552f3f Add directions
* 9b751b9 Add ingredients
* ddfe74e Better name for the cake
* d290aa4 This is going to be a cake recipe
$
$ git diff HEAD HEAD~~
$
$ git show HEAD
commit 52054bbb4fd9a173ce5cbc9f33b22a8c2dd69b87 (HEAD -> master)
Author: John Doe <john.doe@email.com>
Date:   Tue Nov 15 20:02:49 2022 +0100

    Revert "Add other ideas and hints"
    
    This reverts commit 2690c4f6183c187b75588c5d5cfd485fe88fcb2c.

diff --git a/recipe.txt b/recipe.txt
index 261773d..9c65dc5 100644
--- a/recipe.txt
+++ b/recipe.txt
@@ -28,7 +28,3 @@
  8. Bake in two greased a-inch layer pans lined with paper at 325f about 35
     minutes.
  9. Frost with fondant icing.
-
-## Other ideas and hints
-
- - Adding some instant coffee might give the case some extra kick.
```

