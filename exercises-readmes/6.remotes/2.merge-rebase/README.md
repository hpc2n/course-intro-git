# Merge conflicts and rebasing

This exercise demonstrates how to solve a merge conflict using rebasing. 

Note: for the present example you don't need to add a remote. It has been
added for this example already.

Tasks:

1. Enter the `repository` directory and check the current status.

2. Check that the file `file.txt` has been modified since the last commit
using the *diff* command

3. Try commiting the changes and push them to the remote

4. Why do the push was unsuccesful?

hint: the remote contains changes that are missing from your local
remote. 

5. Pull the changes from the remote

6. When the text editor opens save the commit message. This means that
Git is able to merge the remote and your local changes.

7. Take a look at the commits' tree graph:

```
git log --all --decorate --oneline --graph
```
and save it into a text file for further investigations.

8. You could simply continue to work normally from here but the merge commit you
just created is not actually necessary in this situation. Try falling back to
the previous commit:

```
$ git reset --hard HEAD~
```

9. Now, pull again but tell Git to rebase your branch:

```
$ git pull --rebase
```

10. Take a look at the graph once again with:


```
git log --all --decorate --oneline --graph
```

and compare it with the one you saved into a text file. 
You can now see that the merge commit was not necessary.

11. Finally, you can now push the changes to the remote.
