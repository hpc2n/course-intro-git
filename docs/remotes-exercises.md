# Exercises - Working with remotes 

In order to do these exercises, you need to download the exercises zip file (if you already did so for the previous exercise, you do not need to do so again, of course).

You can do that either by cloning the repository or by just getting the zip file with `wget`.

- Do ONE of the following:
    - **git clone**
        1. `git clone https://github.com/hpc2n/course-intro-git.git`
        2. `cd course-intro-git`
        3. `unzip git_materials.zip`
        4. `cd git_materials`
        5. `cd 6.remotes`
    - **Fetch with wget**
        1. `wget https://github.com/hpc2n/course-intro-git/raw/refs/heads/main/git_materials.zip`
        2. `unzip git_materials.zip`
        3. `cd git_materials`
        4. `cd 6.remotes`

You are now in a directory with 2 subdirectories, one for each exercise.

## Adding remotes

Make sure you are in the subdirectory `git_materials/6.remotes/1.adding-remotes`. 

1. Fork the following repository `https://github.com/pojeda/pull-request-course.git`<br>
2. Clone the forked repository and check the available remotes<br>
3. Add the upstream repository with the name "upstream"<br>
4. Using your cloned version of the forked repository, make some modification to the "README.md" file and commit them locally. Then, push the changes to the remote.<br>
Finally, make a "pull request" from your GitHub account.


## Merge conflicts and rebasing 

Make sure you are in the subdirectory `git_materials/6.remotes/2.merge-rebase`. 

!!! note 

    This exercise demonstrates how to solve a merge conflict using rebasing.

    **Note:** for the present example you don't need to add a remote. It has been added for this example already.

Tasks:

1. Enter the `repository` directory and check the current status.
<br>
2. Check that the file `file.txt` has been modified since the last commit
using the *diff* command
<br>
3. Try commiting the changes and push them to the remote
<br>
4. Why do the push was unsuccesful?
<br>
**hint:** the remote contains changes that are missing from your local
remote. 
<br>
5. Pull the changes from the remote
<br>
6. When the text editor opens save the commit message. This means that
Git is able to merge the remote and your local changes.
<br>
7. Take a look at the commits' tree graph:
<br>
```
git log --all --decorate --oneline --graph
```
and save it into a text file for further investigations.
<br>
8. You could simply continue to work normally from here but the merge commit you just created is not actually necessary in this situation. Try falling back to the previous commit:
<br>
```
$ git reset --hard HEAD~
```
<br>
9. Now, pull again but tell Git to rebase your branch:
<br>
```
$ git pull --rebase
```
<br>
10. Take a look at the graph once again with:
<br>
```
git log --all --decorate --oneline --graph
```
<br>
and compare it with the one you saved into a text file. 
You can now see that the merge commit was not necessary.
<br>
11. Finally, you can now push the changes to the remote.
<br>

