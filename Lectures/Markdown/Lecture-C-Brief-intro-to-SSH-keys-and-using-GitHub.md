---
title: 'Lecture C: Brief intro to SSH-keys and using GitHub'
tags: [Lecture, ' Birgitte', ' day 4']

---

---
title: "Lecture C: Brief intro to SSH-keys and using GitHub"
tags: Lecture, Birgitte, day 4
description: "Git installation etc"
---

Introduction to Git --- Fall 2024
## Lecture C: Brief intro to SSH-keys and using GitHub

<!-- .slide: data-background="#ffffff" -->

<!-- Lecture material made by Birgitte Brydsö for the version of the course that was given in fall 2020. Lecture was first given by Birgitte Brydsö in fall 2020. 
Minor modifications done for the fall 2021, 2022, 2023, and 2024 versions of the course. -->

![TOC](https://www.hpc2n.umu.se/sites/default/files/umu-logo-left-se.png =200x)  ![](https://www.hpc2n.umu.se/sites/default/files/hpc2n-logo-text5.png =200x)  ![](https://www.hpc2n.umu.se/sites/default/files/conferences-courses/2023/Uppsala_Universitet-logo-2E2D20E6B3-seeklogo.com.png =100x) ![](https://www.hpc2n.umu.se/sites/default/files/conferences-courses/2023/naiss-narrow.jpg =200x)

<small>Slides: https://hackmd.io/@git-fall-2024/LC-github</small>

---

## GitHub

<!-- .slide: style="font-size: 32px;" -->

We are going to use GitHub for the part of the hands-on where you will be working together in groups, as well as part of the "Working with remotes" section.

Please go to 
* https://github.com/

and sign up for an account if you do not already have one. 

You will need to setup 2FA also. 

---

## Create a new SSH key for GitHub - Linux and macOS

<!-- .slide: style="font-size: 28px;" -->

This part will be repeated tomorrow before the section "Teamwork", but you should create and add your SSH key to GitHub now if you are doing the hands-ons for the "Working with remotes" section.

1. Open a terminal. In the command below, "GitHub" is a label added to the key for clarity. You can add any text you want: 
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

---

## Create a new SSH key for GitHub - Linux and macOS, continued

<!-- .slide: style="font-size: 28px;" -->

4. Add the key to the ssh-agent. Here we assume the default name for the newer systems - change to what your key was called (if you used the option for legacy systems, it would as default be called `id_rsa`): 
```
$ eval "$(ssh-agent -s)"

$ ssh-add ~/.ssh/id_ed25519
```
5. Switch to the `.ssh` folder, open the file `id_ed25519.pub` (`id_rsa.pub` for legacy systems) and copy the entire contents. Do NOT add any newlines or whitespace! 

---

## Create a new SSH key for GitHub - Windows

<!-- .slide: style="font-size: 28px;" -->

This part will be quickly repeated tomorrow before the section "Teamwork", but you should create and add your SSH key to GitHub now if you are doing any of the hands-ons for the "Working with remotes" section.

1. Open Git Bash. In the command below, "GitHub" is a label added to the key for clarity. You can add any you want: 
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

---

## Create a new SSH key for GitHub - Windows, continued

<!-- .slide: style="font-size: 28px;" -->

4. Add the key to the ssh-agent. Here we assume the default name for the newer systems (on the legacy systems it would be `id_rsa` instead) - change to what your key was called: 
```
$ eval "$(ssh-agent -s)"

$ ssh-add ~/.ssh/id_ed25519
```
5. Switch to the `.ssh` folder, open the file `id_ed25519.pub` (`id_rsa.pub` on legacy systems) and copy it. Do NOT add any newlines or whitespace! 

---

<!-- .slide: style="font-size: 28px;" -->

## Adding the SSH key to GitHub

1. On GitHub, click your avatar in the top right corner and pick "Settings".
2. Choose "SSH and GPG keys"
3. Click the green button labeled "New SSH key"
4. Add a descriptive label for the key in the "Title" field. In the key field you paste the content of the key (~/.ssh/id_rsa.ed25519.pub or ~/.ssh/id_rsa.pub)
![](https://i.imgur.com/DzOFZTd.png =500x)
5. Click "Add SSH key"
6. Confirm your GitHub password if you are prompted for it. 

---

<!-- .slide: style="font-size: 28px;" -->

## Testing the SSH keys

1. Open a terminal / the Git bash 
2. `$ ssh -T git@github.com`
3. It will look similar to this: 
```
$ ssh -T git@github.com
The authenticity of host 'github.com (140.82.121.3)' can't be established.
ECDSA key fingerprint is SHA256:p2QAMXNIC1TJYWeIOttrVc98/R1BUFWu3/LiyKgUfQM.
ECDSA key fingerprint is MD5:7b:99:81:1e:4c:91:a5:0d:5a:2e:2e:80:13:3f:24:ca.
Are you sure you want to continue connecting (yes/no)? yes
Warning: Permanently added 'github.com,140.82.121.3' (ECDSA) to the list of known hosts.
Hi bbrydsoe! You've successfully authenticated, but GitHub does not provide shell access.
```
4. Verify that the resulting message contains your username. 

<!-- ## GitHub CLI

GitHub also has a command line interface that you can use if you want to. 

It is available for Windows, macOS, and Linux. 

You can use it if you prefer to do your workflow through a terminal, and you can call the GitHub API to script various actions as well as set a custom alias for any command.

More information and download here: https://github.blog/2020-09-17-github-cli-1-0-is-now-available/ 

--- -->


