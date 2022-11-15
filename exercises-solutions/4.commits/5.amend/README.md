# Amending previous commit - with solutions

The goal of this exercise is to learn to amend the latest commit. Enter the
`repository/` directory and perform the following steps:

 1. The ingredient list in the `repository/recipe.txt` file is missing an
    ingredient. Add two eggs to the ingredient list.

 2. Stage the changes and amend the previous commit
    (`Add remaining ingredients and directions`).

 3. Validate the operation. The log (`git log`) should contain three commits and
    the most recent commit (`Add remaining ingredients and directions`) should
    contain the new added ingredient (`git show <commit>`).

**Solution**

 1. Investigate the repository as a very first step:

```shell
$ git log --oneline --all --graph
* c14e6da (HEAD -> master) Add remaining ingredients and directions
* 3aee0ad Add some ingredients
* 8806db1 This is going to be a cake recipe
$ git status
On branch master
nothing to commit, working tree clean
```

Editing `recipe.txt` in order to order to add 2 eggs.

 2. Stage the modification with `git add recipe.txt`.

```shell
$ git commit --amend 
[master 447f2a0] Add remaining ingredients and directions
 Date: Sun Nov 13 21:15:03 2022 +0100
 1 file changed, 18 insertions(+)
```

```shell
$ git log --oneline --all --graph
* 447f2a0 (HEAD -> master) Add remaining ingredients and directions
* 3aee0ad Add some ingredients
* 8806db1 This is going to be a cake recipe
```

```shell
$ git show HEAD```

