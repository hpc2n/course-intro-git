# Stashing uncommitted changes - with solutions

The goal of this exercise is to learn to checkout a different commit and stash
uncommited changes, if necessary. Enter the `repository/` directory and perform
the following steps:

 1. Identify the first commit (`This is going to be a cake recipe`).
 
 2. Try to checkout the commit in order to identify the initial title of the
    recipe. If necessary, stash the changes. What was the initial title of the
    recipe?

 3. Restore the `HEAD` and pop the changes from the stash.
 
 4. Confirm that the changes were applied correctly and that the stash is empty.


**Solution**

 1. One may use `git log` to print the commit history:

```shell
$ git log --oneline
94e9a51 (HEAD -> master) Add directions
41ac71c Add ingredients
63b34a4 Better name for the cake
d290aa4 This is going to be a cake recipe
```

 2. There are modified changed in the working directory:

```shell
$ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
	modified:   recipe.txt

no changes added to commit (use "git add" and/or "git commit -a")
```

Save the changes in the working directory to the stash:

```shell
$ git stash
Saved working directory and index state WIP on master: 94e9a51 Add directions
```

Checkout to the first commit:

```shell
$ git checkout d290aa4
Note: switching to 'd290aa4'.

You are in 'detached HEAD' state. You can look around, make experimental
changes and commit them, and you can discard any commits you make in this
state without impacting any branches by switching back to a branch.

If you want to create a new branch to retain commits you create, you may
do so (now or later) by using -c with the switch command. Example:

  git switch -c <new-branch-name>

Or undo this operation with:

  git switch -

Turn off this advice by setting config variable advice.detachedHead to false

HEAD is now at d290aa4 This is going to be a cake recipe
```

Investigating the files:

```shell
$ ls 
recipe.txt
$ cat recipe.txt 
# My fancy cake
```

The original title of the recipe was "My fancy cake".

 3. Checkout to the tip of the branch: `git checkout master` or `git checkout main`, depending on your operating system.

```shell
$ git checkout master
Previous HEAD position was d290aa4 This is going to be a cake recipe
Switched to branch 'master'
```
List the stash and pop the changes:

```shell
$ git stash list
stash@{0}: WIP on master: 94e9a51 Add directions
$ git stash pop 0
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
	modified:   recipe.txt

no changes added to commit (use "git add" and/or "git commit -a")
Dropped refs/stash@{0} (3fdb287a100dda3296bec8c00f24f951286c8105)
```

 4. Confirm that the stash is empty and look into `recipe.txt`:

```shell
$ git stash list
$ cat recipe.txt 
# Maraschino Devil's Food Cake

## Ingredients

 - 2 cup sifted cake flour
 - 1 teaspoon soda
 - 1 1/3 cup sugar
 - 1/2 cup snowdrift
 - 1/2 cup buttermilk
 - 1/4 cup Maraschino cherry juice
 - 2 eggs
 - 2 squares unsweetened chocolate, melted and cooled

## Directions

 1. All ingredients mixed in same bowl.
 2. Mixing time three minutes.
 3. Sift together in large bowl flour, soda, and sugar.
 4. Add snowdrift, buttermilk and cherry juice.
 5. Mix enough to dampen flow; beat 2 minutes-if by hand, count beating time
    only; with electric mixer use low speed, beating 2 minutes.
 6. Add eggs and chocolate.
 7. Beat 1 minute for snowdrift, smooth batter, then fold in 1/2 cup chopped
    cherries dusted with flour.
 8. Bake in two greased a-inch layer pans lined with paper at 325f about 35
    minutes.
 9. Frost with fondant icing.

## Other ideas and hints

 - Adding some instant coffee might give the case some extra kick.
```

