---
title: 'Lecture B: Using Rackham for the Git course'
tags: [Lecture, ' Birgitte', ' day 1']

---

---
title: "Lecture B: Using Rackham for the Git course"
tags: Lecture, Birgitte, day 1
description: "Git installation, use of Rackham, etc"
---

Introduction to Git --- Fall 2024
# Lecture B: Using Rackham for the Git course

<!-- .slide: data-background="#ffffff" -->

<!-- Lecture material made by Birgitte Brydsö for the version of the course that was given in fall 2020. Lecture was first given by Birgitte Brydsö in fall 2020. 
Minor modifications done for the fall 2021 and 2022 versions of the course. For the 2023 version of the course the machine was changed from Kebnekaise to Rackham. In 2024, Rackham will also be used. -->

![TOC](https://www.hpc2n.umu.se/sites/default/files/umu-logo-left-se.png =200x)  ![](https://www.hpc2n.umu.se/sites/default/files/hpc2n-logo-text5.png =200x)  ![](https://www.hpc2n.umu.se/sites/default/files/conferences-courses/2023/Uppsala_Universitet-logo-2E2D20E6B3-seeklogo.com.png =100x) ![](https://www.hpc2n.umu.se/sites/default/files/conferences-courses/2023/naiss-narrow.jpg =200x)

<small>Slides: https://hackmd.io/@git-fall-2024/LB-rackham</small>

---

## Connecting to Rackham

<!-- .slide: style="font-size: 28px;" -->

For this course we recommend using ThinLinc, but if you have your own installation of another SSH client that you prefer, you are welcome to use that. We will be using the command line only. 

* Download the client from https://www.cendio.com/thinlinc/download and install it.
* Start the client. Enter the name of the server: rackham-gui.uppmax.uu.se and then enter your own username.
* Go to "Options" -> "Security". Check that authentication method is set to password.
* Go to "Options" -> "Screen" and uncheck "Full screen mode".
* Enter your UPPMAX password. Click "Connect".

ThinLinc can also be used from a browser: https://rackham-gui.uppmax.uu.se

If you prefer a different SSH client (terminal, etc.), you connect with ssh -Y <user>@rackham.uppmax.uu.se

---

## Connecting to Rackham - continued

<!-- .slide: style="font-size: 30px;" -->

**NOTE** If you are not connecting from within the domain of a Swedish university, **2FA may be needed**.
    
* You cannot do this through ThinLinc
* It can be handled by
    * logging in with a regular SSH-client (PuTTy or similar)
    * doing the 2FA and then logging out again
    * there is then a grace period of some minutes for you to login to ThinLinc. 
* More info here: https://www.uu.se/en/centre/uppmax/get-started/2-factor   

---

## Setting up Git

<!-- .slide: style="font-size: 28px;" -->

Git is already installed on Rackham, but you need to set your name and email globals *unless you have already done this at some earlier time*. 

* Open a terminal. In ThinLinc: Go to the menu at the top. Click “Applications” → “System Tools” → “MATE Terminal”.
* Set your global name (change "Your Name"): 
  `$ git config --global user.name "Your Name"`
* Set your global email (change the example): 
  `$ git config --global user.email "name@example.com"` 

You may also want to set your editor. We recommend nano, but other options are vim and emacs (or notepad on Windows). 

* `$ git config --global core.editor nano`

---

## Testing your configuration 

<!-- .slide: style="font-size: 32px;" -->

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

## Testing your configuration - continued

<!-- .slide: style="font-size: 32px;" -->

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

<!-- .slide: style="font-size: 20px;" -->

For the individual hands-on part of the course, we have created some course materials which you will download from either the course website, the course GitHub, or the "important information" page. 

* Course website: https://www.hpc2n.umu.se/events/courses/2024/fall/git
* Course GitHub: https://github.com/hpc2n/course-intro-git
  - Click the green button labeled "Code" for links to clone or download the materials. 
  - Either do **1. CLONE** or **2. DOWNLOAD**, not both! 
    - CLONE: Change to the directory where you wish to have the course material and clone with 'git clone' and the url: 
      - git clone https://github.com/hpc2n/course-intro-git.git
      - You get the directory: `course-intro-git`
    - DOWNLOAD Zipfile: Please go to the terminal window where you have downloaded and set up Git. Change the directory to wherever you wish to have the course material. 
      - Download the Zipfile and move it there. Can be done directly from the terminal with `wget https://github.com/hpc2n/course-intro-git/archive/refs/heads/main.zip`)
      - Unpack with `unzip main.zip`. 
      - You will get a directory called `course-intro-git-main`.  
    
    

