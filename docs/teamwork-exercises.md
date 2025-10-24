# Exercises - Teamwork  

## 1. Setting up a repository on GitHub 

!!! note

    In this exercise you will create a repository on GitHub and work with that. 

    You will be working on the GitHub website (so you need to have signed up for an account). 

1. Create a repository (click on the + at the top right of the menu or picking "Start a new repository" on your "home screen")
<br>
2. Under "Quick setup", pick "creating a new file".
<br>
3. Name the file "README.md" (at the top, over the file editor).
<br>
4. Put some text in the file "README.md".
<br>
5. At the bottom, where it says "Commit new file" you should put a useful commit message. Then click "Commit new file"
<br>
6. Notice: the content of README.md appears at top level of the repo
<br>
7. Try creating another file in a subdirectory (create subdirectories by adding the name you want after the name of your repo, then adding a "/" and your filename).
<br>
8. Try adding a file that you have created on your computer and uploads (Add file -> Upload files)
<br>
9. Test out making edits to your files and committing them - all through the GitHub site.
<br>
10. If you put a file "README.md" in a subdirectory then it will be shown as a "description" for the directory
<br>
11. When you have made some commits, try click "commits" above the files in the repo and see a list of your commits.

## 2. Creating and using SSH-keys 

!!! warning 

    Only do this if you did not do that earlier in the week/before! 

!!! note 

    In this exercise you create SSH keys and upload to GitHub. Then test that it works.

    Everyone in the team should do this! 

**Create a new SSH key**

1. Open a terminal (Git Bash on Windows). In the command below, "GitHub" is a label added to the key for clarity. You can add any you want:
    a. Do this
    ```
    $ ssh-keygen -t ed25519 -C "GitHub"
    ```
    b. If you have an older system, this may work better
    ```
    $ ssh-keygen -t rsa -b 4096 -C "GitHub"
    ```
<br>
2. You will be asked for a file to save the key. Unless you have an existing SSH key, accept the default.
<br>
3. Enter a passphrase and repeat it.
<br>
4. Add the key to the ssh-agent. Here we assume the default name: 
<br>
```
$ eval "$(ssh-agent -s)"

$ ssh-add ~/.ssh/id_rsa
```
<br>
5. Switch to the `.ssh` folder, open the file `id_rsa.pub` and copy it. Do NOT add any newlines or whitespace! 
<br>


**Adding the SSH key to GitHub**

1. On GitHub, click your avatar in the top right corner and pick "Settings".
<br>
2. Choose "SSH and GPG keys"
<br>
3. Click "Add new SSH key"
<br>
4. Add a descriptive label for the key in the "Title" field. In the key field you paste the content of the key (~/.ssh/id_rsa.pub)
<br>
![Add new SSH key](../images/new-key.png)
<br>
5. Click "Add SSH key"
<br>
6. Confirm your GitHub password if you are prompted for it. 
<br>


**Testing the SSH keys**

1. Open a terminal (or Git Bash) 
<br>
2. `$ ssh -T git@github.com`
<br>
3. It will look similar to this: 
<br>
```
$ ssh -T git@github.com
The authenticity of host 'github.com (140.82.121.4)' can't be established.
RSA key fingerprint is SHA256:nThbg6kXUpJWGl7E1IGOCspRomTxdCARLviKw6E5SY8.
Are you sure you want to continue connecting (yes/no)? yes
Warning: Permanently added 'github.com,140.82.121.4' (RSA) to the list of known hosts.
Enter passphrase for key '/home/bbrydsoe/.ssh/id_rsa': 
Hi bbrydsoe! You've successfully authenticated, but GitHub does not provide shell access.
```
<br>
4. Verify that the resulting message contains your username. 
<br>
5. NOTE: Optionally, you could run `ssh-add` to add the key. Then you will only be asked for the passphrase once per session. This is relatively safe on Linux and macOS, but not on Windows where it usually saves the key passphrase permanently.

## 3. clone, push, pull

!!! note 

    We now have SSH keys set up. Time to test it from your own machine

1. Clone the repository, using the SSH address (click "CODE" on the GitHub repository and pick "SSH"). You will be asked for the key passphrase.
<br>
2. Enter the local repository. Do a `git pull` and see that it works. You will have to enter the key passphrase.
<br>
3. Create a file (or edit a file).
<br>
4. Add the file. Commit the file (`git add`, `git commit`)
<br>
5. Push the file. Again it will ask for the key passphrase. Success!
<br>
6. NOTE: Optionally, you could run `ssh-add` to add the key. Then you will only be asked for the passphrase once per session. This is relatively safe on Linux and macOS, but **not** on Windows where it usually saves the key passphrase permanently.
<br> 

## 4. Teamwork, push and pull 

!!! note 

    One of you should create a repository on GitHub and invite their team. 

    Remember, on the GitHub webpage the option to create a new repository is in the top right corner - click the "+". To add members: "Settings" -> "Manage access".

1. Each person should create a file in the repository (Add and commit the file)
<br>
2. On the command line, do a `git status`. Do a `git log --graph --oneline --decorate --all`
<br>
3. NOTE! To avoid errors, do `git pull` before you stage and commit your file and also the team members should use different names for their files. See the changes appear when you do a `git pull` after all have added their file(s).
<br>
4. You could also try to push a new change before pulling the changes your team members have made. Git will complain, but you should be able to solve this kind of simple problem with `git pull --rebase` before you re-do `git push`
<br>
5. Try create more files then add and commit. Do `git status` and `git log --graph --oneline --decorate --all` before and after each step. Push the files to the repository. Check the log and status again.
<br>
6. NOTE: You will be asked for the key passphrase each time you do a push
<br>

## 5. Teamwork, branches and merging

1. Each person creates a branch in the repo you created in the previous exercise. You can use `git branch yourbranchname` where you put any name you want for the new branch.
<br>
2. Switch to the new branch with `git checkout yourbranchname`
<br>
3. Create a uniquely named file. Put anything you want in it.
<br>
4. Do `git log` and `git status` to see any changes.
<br>
5. Stage and commit the file. Check again with `git log` and `git status`
<br>
6. Push your changes with `git push origin -u yourbranchname` (or with `git push -u origin HEAD` for a fast way when using the same name)
<br>
7. When everyone has done this, all do a `git pull`
<br>
8. Use `git status`, `git branch`, and `git log` to see what has happened.
<br>

## 6. Teamwork, branches and merging, pull requests 

1. (Members) Go to the repository you have worked in on the GitHub page. Submit a pull-request from your branch to the main branch
<br>
2. (Owner) The owner of the repository (the person who created it) can then accept them and click to merge them.
<br>
3. After doing so, everyone should again do a `git pull` (on the command line)
<br>
4. Use `git status`, `git branch --all`, and `git log --graph --oneline --decorate --all` to see what has happened.
<br>
**Note**: It is possible to make the main branch "protected" so it is not changed without a review from the owner. Try doing this (on GitHub).
<br> 

## 7. Teamwork and branches 

!!! note 

    Now you will be creating a new branch in the repo your group is sharing, but you will create in from the GitHub page 

1. Everyone in the group create a new branch in the repo - this time you could try doing it **from the GitHub page**
<br>
Now you are working on the command line
<br>
2. Check which remote branches exist with `git branch -r` 
<br>
3. Check which local branches you have with `git branch` 
<br>
4. Use `git status` to see which branch you are on.
<br>
5. Check with `git branch -a` to see all local and remote branches
<br>
6. Do a `git pull` from the command line to get a list of all branches. Switch to the branch you created on GitHub with `git checkout --track origin/mynewbranch`. Again do `git branch` to see which branch you are on.
<br>
7. Create a new file and put some content to it. Add and commit it. Check for changes (`git status`, `git log`). Push the changes.
<br>
8. Try and merge the branches from the command line. Remember to first pull any changes from your other group members. Also remember to switch to the branch you want to merge it to (main in this case).
<br>
9. Were you succesful? Why or why not? Is there are difference between what happens when the owner of the branch tries this and when everyone else does?
<br>
10. After doing this, everyone should again do a `git pull` (on the command line)
<br>
11. Use `git status`, `git branch`, and `git log` to see what has happened. If you want a "prettier" and sometimes easier to read view, use `git log --graph --oneline --decorate --all`
<br>

## 8. Deleting branches 

1. Everyone should now create two more branches in the repo. In each case, switch to the branch, create a file in it, and push the branch. (You could try this both on the command line and in the web repo on GitHub) 
<br>
2. Check which branches exist, remotely and locally (on the command line)
<br>
3. Try and delete a remote branch with `git push origin --delete myownbranch` (on the command line)
<br>
4. Try delete a local branch with `git branch -D <alsomyownbranch>` (on the command line)
<br>
5. On the command line, do a `git status`, `git log` and `git branch` to see what has happened
<br>
6. The branch you deleted locally is still on the repo. Get another copy of it (`git pull` and `git fetch`, possibly with suitable flags will get it back for you - this is again done on the command line)
<br> 

## 9. Merge conflicts 

!!! note 

    In this exercise everyone in the team will be working in the same branch, for instance the main branch.

    Merge conflicts generally happen when two (or more) teammembers edit the same file and the same line, or when one edits a file and another deletes it.

1. (One in the team do this) Create a new repository on GitHub. Add your team members as in the previous exercises. Everyone clones the repository (from the command line).
<br>
2. Create a couple files. Add, commit, and push.
    - If more than one person creates files, remember to either pull your teammates work first, or do a `git pull --rebase` before pushing.
<br>
3. After doing this, everyone should again do a `git pull`
<br>
4. Now one or more of the team members make changes to the same file, in the same line. Add, commit, push.
<br>
5. Did you get a conflict? Use `git status`, `git branch`, and `git log` to see what has happened. Try to resolve the conflict.
<br>
6. Now again all will work on one file. One or more will edit it and one deletes it (`git rm file`). What happens when you push your work? You should get a conflict. 
<br>
7. Try and resolve the conflict you got. Should the file be kept or deleted?
<br> 

