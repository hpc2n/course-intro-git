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

2. You will be asked for a file to save the key. Unless you have an existing SSH key, accept the default.

3. Enter a passphrase and repeat it.

4. Add the key to the ssh-agent. Here we assume the default name: 

```
$ eval "$(ssh-agent -s)"

$ ssh-add ~/.ssh/id_rsa
```

5. Switch to the `.ssh` folder, open the file `id_rsa.pub` and copy it. Do NOT add any newlines or whitespace! 



**Adding the SSH key to GitHub**

1. On GitHub, click your avatar in the top right corner and pick "Settings".

2. Choose "SSH and GPG keys"

3. Click "Add new SSH key"

4. Add a descriptive label for the key in the "Title" field. In the key field you paste the content of the key (~/.ssh/id_rsa.pub)

![](https://i.imgur.com/DzOFZTd.png)

5. Click "Add SSH key"

6. Confirm your GitHub password if you are prompted for it. 



**Testing the SSH keys**

1. Open a terminal (or Git Bash) 

2. `$ ssh -T git@github.com`

3. It will look similar to this: 

```
$ ssh -T git@github.com
The authenticity of host 'github.com (140.82.121.4)' can't be established.
RSA key fingerprint is SHA256:nThbg6kXUpJWGl7E1IGOCspRomTxdCARLviKw6E5SY8.
Are you sure you want to continue connecting (yes/no)? yes
Warning: Permanently added 'github.com,140.82.121.4' (RSA) to the list of known hosts.
Enter passphrase for key '/home/bbrydsoe/.ssh/id_rsa': 
Hi bbrydsoe! You've successfully authenticated, but GitHub does not provide shell access.
```

4. Verify that the resulting message contains your username. 

5. NOTE: Optionally, you could run `ssh-add` to add the key. Then you will only be asked for the passphrase once per session. This is relatively safe on Linux and macOS, but not on Windows where it usually saves the key passphrase permanently.


