---
title: "Using Alvis for the Git course"
tags: Lecture, Birgitte, day 1
description: "Git installation, use of Alvis, etc"
---

<!-- Lecture material made by Birgitte Brydsö for the version of the course that was given in fall 2020. Lecture was first given by Birgitte Brydsö in fall 2020. 
Minor modifications done for the fall 2021 and 2022 versions of the course. For the 2023 version of the course the machine was changed from Kebnekaise to Rackham. In 2024, Rackham will also be used. 
For the 2024 version of the course, the machine was changed from Rackham to Tetralith, though the material for using Triolith remains, as Lecture B. -->

<!-- For the 2025 version of the course, material has been made for how to connect to Alvis as well. --> 

<!-- Slides: https://hackmd.io/@git-fall-2024/tetralith#/ --> 

---

# Connecting to Alvis

## OpenOnDemand

For this course we recommend using OpenOnDemand, but if you have your own installation of another SSH client that you prefer, you are welcome to use that. We will be using the command line only, so an SSH client like PuTTY would also work. 

## Logging in 

### OpenOnDemand

- Put ``https://alvis.c3se.chalmers.se`` in browser address bar
- Login through SUPR, with your SUPR credentials.

- Put ``<your-c3se-username>`` and ``<your-c3se-password>`` in the login box

### Other SSH client 

If you prefer a different SSH client (terminal, etc.), you connect with either of 

- ``ssh -Y <user>@alvis1.c3se.chalmers.se`` 
- ``ssh -Y <user>@alvis2.c3se.chalmers.se``

- Put ``<your-c3se-username>`` where it says ``<user>`` and then the ``<user-c3se-password>`` when it asks for it. 

!!! warning "Note"

    Alvis is accessible via SUNET networks (i.e. most Swedish university networks). 

    If you are not on one of those networks you need to use a VPN - preferrably your own Swedish university VPN. If this is not possible, contact ``support@chalmers.se`` and ask to be added to the Chalmers's eduVPN.

---

## Setting up Git

Git is already installed on Alvis, but you need to set your name and email globals *unless you have already done this at some earlier time*. 

* Open a terminal. 
    - If you are using OpenOnDemand portal: 
        - Go to the portal and authenticate through SUPR
        - In the menu at the top. Click “My Interactive Apps” → “Desktop Login” (since you do not need to start a job on a compute node to just run Git. 
        - Pick either of the login nodes
        - Pick "Alvis remote desktop" and enter your ``<alvis username>`` and ``<alvis password>``
        - When the desktop starts, in the top menu, choose "Applications" → “System” → "Xfce Terminal".
* Set your global name (change "Your Name", do not include the prompt `$`): 
  `$ git config --global user.name "Your Name"`
* Set your global email (change the example, do not include the prompt): 
  `$ git config --global user.email "name@example.com"` 

You may also want to set your editor. We recommend nano, but other options are vim and emacs (or notepad on Windows). 

* `$ git config --global core.editor nano`

---

## Testing your configuration 

Create an example folder and cd into that, then create a file test.txt: 

```bash
$ mkdir <mydir> 
$ cd <mydir>
$ touch test.txt
```

Now initialize a repository and add the new file:

```bash
$ git init
$ git add test.txt
```

Now *commit* the change. The editor which you configured earlier should open. Add an example commit message:

```bash
$ git commit test.txt 
```

---

Now let us look at the log:

```bash
$ git log
```

When you do `git log`, you should see something like: 

```bash
commit ff8b6f699d98c72d5cffc64d65a1c618b976b45a (HEAD -> master)
Author: Birgitte Brydsö <bbrydsoe@cs.umu.se>
Date:   Thu Sep 17 13:53:59 2020 +0200

    Test of git
```

but with name, email and commit message different.

If that is the case, your Git should be configured correctly. 

---

## Download the course materials

For the individual hands-on part of the course, we have created some course materials which you will download from either the course website, the course GitHub, or the "important information" page. 

* Course website: <a href="https://www.hpc2n.umu.se/events/courses/2025/git" target="_blank">https://www.hpc2n.umu.se/events/courses/2025/git</a>
* Course GitHub: <a href="https://github.com/hpc2n/course-intro-git" target="_blank">https://github.com/hpc2n/course-intro-git</a>
    - Click the green button labeled "Code" for links to clone or download the materials. 
    - Either do **1. CLONE** or **2. DOWNLOAD**, not both! 
        - CLONE: Change to the directory where you wish to have the course material and clone with 'git clone' and the url: 
            - ``git clone https://github.com/hpc2n/course-intro-git.git``
            - You get the directory: `course-intro-git`
        - DOWNLOAD Zipfile: Please go to the terminal window where you have downloaded and set up Git. Change the directory to wherever you wish to have the course material. 
            - Download the Zipfile and move it there. Can be done directly from the terminal with `wget https://github.com/hpc2n/course-intro-git/archive/refs/heads/main.zip`)
            - Unpack with `unzip main.zip`. 
            - You will get a directory called `course-intro-git-main`. 

---

## GitHub and SSH keys

* You need to create an account on GitHub for the course
* You also need to create SSH keys on Alvis and install these on GitHub.
* We will go through this in a general way which should work regardless of system you are using
    * We will go through it before the Teamwork session. The material for creating and setting up SSH keys are here: <a href="https://hpc2n.github.io/course-intro-git/setup/#create__a__new__ssh__key__for__github" target="_blank">https://hpc2n.github.io/course-intro-git/setup/#create__a__new__ssh__key__for__github</a>


