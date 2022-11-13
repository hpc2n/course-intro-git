---
title: "Lecture B: Using Kebnekaise for the Git course"
tags: Lecture, Birgitte, day 1
description: "Git installation, use of Kebnekaise, etc"
---

Introduction to Git --- Fall 2022
# Lecture B: Using Kebnekaise for the Git course

<!-- .slide: data-background="#ffffff" -->

<!-- Lecture material made by Birgitte Brydsö for the version of the course that was given in fall 2020. Lecture was first given by Birgitte Brydsö in fall 2020. 
Minor modifications done for the fall 2021 and 2022 versions of the course. -->

![TOC](https://www.hpc2n.umu.se/sites/default/files/umu-logo-left-se.png =250x)  ![](https://www.hpc2n.umu.se/sites/default/files/hpc2n-logo-text5.png =250x)  ![](https://www.hpc2n.umu.se/sites/default/files/images/SNIC_logo_autocrop.png =250x)

<small>Slides: https://hackmd.io/@git-fall-2022/LB-kebnekaise#/</small>

---

## Connecting to Kebnekaise

<!-- .slide: style="font-size: 30px;" -->

For this course we recommend using ThinLinc, but if you have your own installation of another SSH client that you prefer, you are welcome to use that. We will be using the command line only. 

* Download the client from https://www.cendio.com/thinlinc/download and install it.
* Start the client. Enter the name of the server: kebnekaise-tl.hpc2n.umu.se and then enter your own username.
* Go to "Options" -> "Security". Check that authentication method is set to password.
* Go to "Options" -> "Screen" and uncheck "Full screen mode".
* Enter your HPC2N password. Click "Connect".

More information here: https://www.hpc2n.umu.se/documentation/guides/thinlinc

---

## Setting up Git

<!-- .slide: style="font-size: 32px;" -->

Git is already installed on Kebnekaise, but you need to set your name and email globals *unless you have already done this at some earlier time*. 

* Open a terminal. In ThinLinc: Go to the menu at the top. Click “Applications” → “System Tools” → “MATE Terminal”.
* Set your global name: `$ git config --global user.name "Your Name"`
* Set your global email: `$ git config --global user.email "yourname@example.com"` 

You may also want to set your editor. We recommend vim, but other options are nano and emacs. 

* `$ git config --global core.editor vim`

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

<!-- .slide: style="font-size: 32px;" -->

For the individual hands-on part of the course, we have created some course materials which you will download from either the course website, the course GitHub, or the "important information" page. 

* Course website: https://www.hpc2n.umu.se/events/courses/2022/introduction-to-git
* Course GitHub: https://github.com/hpc2n/course-intro-git
  - Click the green button labeled "Code" to get links to clone or download the materials. 
* Download the material, then please go to the terminal window where you have downloaded and set up Git.
* Change the directory to wherever you wish to have the course material.
* Copy/transfer the tarball there (or download there directly with `wget <url-to-tarball>`)
* Unpack with `tar zxvf <tarball>`

