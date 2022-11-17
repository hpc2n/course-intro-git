# 9. Merge conflicts

In this exercise everyone in the team will be working in the same branch, for instance the main branch (yes, it is not normally recommended to work in the main/master branch, but this could just as well be done in another branch, so we are just using main here). 

Merge conflicts generally happen when two (or more) teammembers edit the same file and the same line, or when one edits a file and another deletes it.

1. Create a new repository on GitHub. Add your team members as in the previous exercises. Everyone clones the repository (from the command line).

	Follow the instructions from the first exercise for how to create a repository and from the fourth exercise for how to add members. 

2. Create a couple files. Add, commit, and push.
   - If more than one creates files, remember to either pull your teammates work first, or do a `git pull --rebase` before pushing.

4. After doing this, everyone should again do a `git pull`

5. Now one or more make changes to the same file, in the same line. Add, commit, push.

6. Did you get a conflict? Use `git status`, `git branch`, and `git log` to see what has happened. Try to resolve the conflict.

7. Now again all will work on one file. One or more edit it and one deletes it (`git rm file`). What happens when you push your work? You should get a conflict. Try and resolve the conflict. Should the file be kept or deleted?

