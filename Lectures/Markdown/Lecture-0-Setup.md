---
title: "Lecture 0: Setup"
tags: Lecture, Birgitte, day 1
description: "Git installation etc"
---

Introduction to Git --- Fall 2022
# Lecture 0: Setup

<!-- .slide: data-background="#ffffff" -->

<!-- Lecture material made by Birgitte Brydsö for the version of the course that was given in fall 2020. Lecture was first given by Birgitte Brydsö in fall 2020. 
Minor modifications done for the fall 2021 and 2022 versions of the course. -->

![TOC](https://www.hpc2n.umu.se/sites/default/files/umu-logo-left-se.png =250x)  ![](https://www.hpc2n.umu.se/sites/default/files/hpc2n-logo-text5.png =250x)  ![](https://www.hpc2n.umu.se/sites/default/files/images/SNIC_logo_autocrop.png =250x)

<small>Slides: https://hackmd.io/@git-fall-2022/L0-setup#/</small>

---

## Installing and setting up Git

<!-- .slide: style="font-size: 30px;" -->

We will use Git from the command line in this course. This is how you will use it on HPC2N's systems, and this way it will also be easier to understand what is going on while you are learning to use Git. 

Graphical tools exists for Git, see below list for a few. All entries on the list are free and unless otherwise mentioned for Windows, macOS, and Linux: 

* git-scm (https://git-scm.com) comes with a basic GUI 
* Git Kraken (https://www.gitkraken.com/)
* Github Desktop (https://desktop.github.com/) Windows and macOS only
* Sourcetree (https://www.sourcetreeapp.com/) Windows and macOS only
* TortoiseGit (https://tortoisegit.org/) Windows only

---

### Installing and setting up Git - continued

<!-- .slide: style="font-size: 38px;" -->

* Install Git, if you have not already
* Create a repository with `git init`
* Set your name and email with `git config` (local, global, system)
* Test by creating a file
* Then adding the file with `git add`
* Then commiting the file with `git commit`

When this is done, you will clone the course materials.

NOTE: if you have a problem and want to use Kebnekaise for this part (and have an account there), we have documentation for you. 

---

### Git install - Windows

<!-- .slide: style="font-size: 32px;" -->

* Go to the Git-scm website (https://git-scm.com/downloads) and click "Windows" to download the Windows version. It will automatically start download of the .exe file.
* The downloaded file can be installed by double-clicking and choosing "Run". 
* Click "Yes" to let it be installed and then "Next" to accept the GNU GPL. 
* The default options you are presented with should work, and we recommend using those. 
* NOTE: when it comes to choosing the default editor, we recommend using Vim, unless you have a preferred editor.

---

### Git install - macOS

<!-- .slide: style="font-size: 34px;" -->

If you have installed XCode (or its Command Line Tools), Git may already be installed. To find out, open a terminal and enter `git --version`.

If Git is not installed, you have several installation options. Apple maintains their own fork of Git, but it is usually a few versions behind, so we do not recommend installing that. 

* SourceForge: https://sourceforge.net/projects/git-osx-installer/files/
* Git-scm.com: https://git-scm.com/downloads
* If you have Homebrew: `brew install git`

---

### Git install - Linux

<!-- .slide: style="font-size: 38px;" -->

Installing Git on Linux depends on which distro you are running. 

* `sudo apt-get install git` (Ubuntu, Debian)
* `sudo dnf install git` (RHEL, CentOS)
* https://git-scm.com/download/linux (other)

---

## Configure git

<!-- .slide: style="font-size: 38px;" -->

First check that you have git installed:
```bash
$ git --version
```
Now configure git with

* `git config (local, global, system)`

You should at least set your global name and email (just once):

```bash
$ git config --global user.name "Your Name"
$ git config --global user.email "yourname@example.com" 
```

---

## Configure git - continued

<!-- .slide: style="font-size: 34px;" -->

Setting the editor (once) is also a good idea: 

```bash
$ git config --global core.editor <editor>
```

Choices for editor could be: 
* nano
* vim
* emacs

---

## Test your Git installation

<!-- .slide: style="font-size: 32px;" -->

Create an example folder and change to that, then create a file test.txt. On Linux you would do this: 

```bash
$ mkdir <mydir> 
$ cd <mydir>
$ touch test.txt
```

Now initialize a repository and stage the new file:

```bash
$ git init
Initialized empty Git repository in /home/bbrydsoe/test-git/.git/
$ git add test.txt
```

Now *commit* the change. The editor which you configured earlier should open. Add an example commit message:

```bash
$ git commit test.txt 
[master (root-commit) ff8b6f6] Test of git
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 test.txt
```

---

## Test your Git installation - continued

<!-- .slide: style="font-size: 32px;" -->

Now let us look at the log:

```bash
$ git log
commit ff8b6f699d98c72d5cffc64d65a1c618b976b45a (HEAD -> master)
Author: Birgitte Brydsö <bbrydsoe@cs.umu.se>
Date:   Thu Sep 17 13:53:59 2020 +0200

    Test of git
```

When you do `git log`, you should see something like the above, but with name, email, and commit message different. If that is the case, your Git should be configured correctly. 

---

## Download the course materials

<!-- .slide: style="font-size: 32px;" -->

For the individual hands-on part of the course, we have created some course materials which you will download from the course GitHub: https://github.com/hpc2n/course-intro-git (normally you click the green "Code" button to get the link to clone or download)

* Please go to the terminal window where you have downloaded and set up Git.
* Change the directory to wherever you wish to have the course material.
* *Do one of*: 
  - 1. Download the zipfile (directly with wget or elsewhere then transfer) and unzip
  - 2. `git clone https://github.com/hpc2n/course-intro-git.git`

---

## Web based Git repositories

<!-- .slide: style="font-size: 32px;" -->

There are several web based Git repository. Some of the more popular ones are: 

* GitHub (https://github.com/)
* GitLab (https://www.gitlab.com)
* Bitbucket (https://bitbucket.org)
* SourceForge (https://sourceforge.net/)

We are going to use GitHub for the part of the hands-on where you will be working together in groups. 

Please go to 
* https://github.com/

and sign up for an account. 

---

## Create a new SSH key for GitHub - Linux and macOS

<!-- .slide: style="font-size: 32px;" -->

This part will be done during the exercises on day 5, but you can create and add your SSH key to GitHub now if you want to. 

1. Open a terminal. In the command below, "GitHub" is a label added to the key for clarity. You can add any you want: 
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
4. Add the key to the ssh-agent. Here we assume the default name for the legacy systems - change to what your key was called: 
```
$ eval "$(ssh-agent -s)"

$ ssh-add ~/.ssh/id_rsa
```
5. Switch to the `.ssh` folder, open the file `id_rsa.pub` and copy it. Do NOT add any newlines or whitespace! 

---

## Create a new SSH key for GitHub - Windows

<!-- .slide: style="font-size: 32px;" -->

This part will be done during the exercises on day 5, but you can create and add your SSH key to GitHub now if you want to. 

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
4. Add the key to the ssh-agent. Here we assume the default name for the legacy systems - change to what your key was called: 
```
$ eval "$(ssh-agent -s)"

$ ssh-add ~/.ssh/id_rsa
```
5. Switch to the `.ssh` folder, open the file `id_rsa.pub` and copy it. Do NOT add any newlines or whitespace! 

---

<!-- .slide: style="font-size: 28px;" -->

## Adding the SSH key to GitHub

1. On GitHub, click your avatar in the top right corner and pick "Settings".
2. Choose "SSH and GPG keys"
3. Click "Add new SSH key"
4. Add a descriptive label for the key in the "Title" field. In the key field you paste the content of the key (~/.ssh/id_rsa.pub)
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
The authenticity of host 'github.com (140.82.121.4)' can't be established.
RSA key fingerprint is SHA256:nThbg6kXUpJWGl7E1IGOCspRomTxdCARLviKw6E5SY8.
Are you sure you want to continue connecting (yes/no)? yes
Warning: Permanently added 'github.com,140.82.121.4' (RSA) to the list of known hosts.
Enter passphrase for key '/home/bbrydsoe/.ssh/id_rsa': 
Hi bbrydsoe! You've successfully authenticated, but GitHub does not provide shell access.
```
4. Verify that the resulting message contains your username. 

<!-- ## GitHub CLI

GitHub also has a command line interface that you can use if you want to. 

It is available for Windows, macOS, and Linux. 

You can use it if you prefer to do your workflow through a terminal, and you can call the GitHub API to script various actions as well as set a custom alias for any command.

More information and download here: https://github.blog/2020-09-17-github-cli-1-0-is-now-available/ 

--- -->

--- 

## Editor, Linux

<!-- .slide: style="font-size: 30px;" -->

Vim
* You may need to install it first. (`sudo apt-get install vim`)
* Start with `vim <filename>` to open a file for editing. The file will be created if it does not exist before. 
* Type `i` to enter 'insert' mode to be able to write in the editor. 
* Use `ESC` to go to 'command' mode and then `:wq` to save and exit the editor.
* When you are in 'command' mode, typing `dd` will delete the whole line your cursor is on. 

Nano
* Start with `nano <filename>` to open a file for editing. The file will be created if it does not exist before.
* Ctrl-x will exit the editor, asking first if you want to save the file. 
