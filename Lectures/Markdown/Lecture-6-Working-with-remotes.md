---
title: 'Lecture 6: Working with remotes'
tags: [Lecture, ' Pedro', ' Day 4']

---

---
title: "Lecture 6: Working with remotes"
tags: Lecture, Pedro, Day 4
description: "TODO"
---

Introduction to Git --- Fall 2024
# Lecture 6: Working with remotes

<!-- .slide: data-background="#ffffff" -->

<!-- Lecture material made by Pedro Ojeda-May for the version of the course that was given in fall 2020. Lecture was first given by Pedro Ojeda-May in fall 2020.-->

![TOC](https://www.hpc2n.umu.se/sites/default/files/umu-logo-left-se.png =200x)  ![](https://www.hpc2n.umu.se/sites/default/files/logo-hpc2n-git-course.png =90x)  ![](https://www.hpc2n.umu.se/sites/default/files/conferences-courses/2023/Uppsala_Universitet-logo-2E2D20E6B3-seeklogo.com.png =100x) ![](https://www.hpc2n.umu.se/sites/default/files/conferences-courses/2023/naiss-narrow.jpg =200x)

<small>Slides: https://hackmd.io/@git-fall-2023/L6-remotes#/</small>

---

<!-- .slide: data-background="#ffffff" -->
<style type="text/css">
  .reveal p {
    text-align: left;
  }
  .reveal ul {
    display: block;
  }
  .reveal ol {
    display: block;
  }
</style>
## Concepts
A remote repository is a version of the project which can be hosted in your local machine, some network, or over the internet (Pro Git, 2nd. Ed., Scott Chacon and Ben Straub) where you and your collaborators can push or pull code modifications. 

In addition to this, a remote is a way to backup your repository.


---

<!-- .slide: data-background="#ffffff" -->
![](https://i.imgur.com/z2FesR1.jpg)


---

<!-- .slide: data-background="#ffffff" -->
<!-- .slide: style="font-size: 30px;" -->
## Updated scheme for file stages

![](https://www.hpc2n.umu.se/sites/default/files/git-folders2.png =700x)

---

<!-- .slide: data-background="#ffffff" -->
## Concepts cont.
The command 

```java
$ git remote -v
origin  git@bitbucket.org:arm2011/gitcourse.git (fetch)
origin  git@bitbucket.org:arm2011/gitcourse.git (push)
```


displays the remotes that are already set up where you can *fetch* and *pull* changes. In this case there is only a single remoted called **origin**.

---

<!-- .slide: data-background="#ffffff" -->

```java
$ git graph
* 2e56d0a (HEAD -> main, origin/main, origin/HEAD) text of exercise git diff usage
* 22a7316 Adding yet more lectures
* 0ddb791 Adding some more of the lectures
* 3ff9f8f Adding some of the lectures
```

---

<!-- .slide: data-background="#ffffff" -->
<!-- .slide: style="font-size: 30px;" -->
## Adding remotes

A remote repository can be added manually with the command

```java
$ git remote add remote_name location

$ git remote add remote_name git@github.com:aliceuser2020/my-first-project.git

$ git remote -v
remote_name	git@github.com:aliceuser2020/my-first-project.git (fetch)
remote_name	git@github.com:aliceuser2020/my-first-project.git (push)
```

where the location of the remote can be an URL or the path if that is in your local machine.


---

<!-- .slide: data-background="#ffffff" -->
Protocols:
- local ->  git clone /opt/git/project.git
- SSH   ->  git clone ssh://user@server:project.git
- HTTP  ->  git clone http://example.com/gitproject.git
- Git


---

<!-- .slide: data-background="#ffffff" -->

Why do we need more than one remote?


```graphviz
digraph {
  rankdir=TD
  S [style=invis]
  "Bob repo" [shape=diamond]
  "Alice fork" [fixedsize=circle]
  "Alice fork" -> "Alice local"
  "Bob repo" -> "Alice fork"
  "Alice local" -> "Bob repo" [style=dashed]
  orig [label="origin" shape=plaintext fontcolor=red]
  orig -> "Alice fork" [style=dashed color=red]
  ups [label="upstream" shape=plaintext fontcolor=red]
  ups -> "Bob repo" [style=dashed color=red]
}
```

---


<!-- .slide: data-background="#ffffff" -->
<!-- .slide: style="font-size: 28px;" -->

```java
$ git remote add upstream git@github.com:bob/my-first-project.git

$ git remote -v
origin	git@github.com:aliceuser2020/my-first-project.git (fetch)
origin	git@github.com:aliceuser2020/my-first-project.git (push)
upstream	git@github.com:bobuser2020/my-first-project.git (fetch)
upstream	git@github.com:bobuser2020/my-first-project.git (push)
```


---

<!-- .slide: data-background="#ffffff" -->
<!-- .slide: style="font-size: 30px;" -->

```java
$git graph
* 2e56d0a (HEAD -> main, upstream/main, origin/main, origin/HEAD) text of exercise git diff usage
* 22a7316 Adding yet more lectures
* 0ddb791 Adding some more of the lectures
* 3ff9f8f Adding some of the lectures
```

---

<!-- .slide: data-background="#ffffff" -->
## Working with remotes
One can push or fetch/pull to or from remotes:

```shell
$ git push  remote_name branch_name
$ git fetch remote_name branch_name
$ git pull  remote_name branch_name 
```

---

<!-- .slide: data-background="#ffffff" -->
In case you obtained the repository by cloning an existing one you will have the **origin** remote. You can do push/fetch/pull for this remote with

```shell
$ git push  origin master      
$ git fetch origin master
$ git pull  origin master
```

---

<!-- .slide: data-background="#ffffff" -->
or 

```shell
$ git push
$ git fetch
$ git pull
```

because the remote *origin* and the *master* branch are configured for pushing and pulling by default upon cloning.

---

<!-- .slide: data-background="#ffffff" -->
The command: 
```shell
$ git pull
```
brings all the changes (branches) that are in the remote and tries to merge them with the current branch of the local repo. The default behavior of *git pull* (*fetch* part) is in the *$GIT_DIR/config* file:
```shell
[remote "origin"]
  fetch = +refs/heads/*:refs/remotes/origin/*
```

---

<!-- .slide: data-background="#ffffff" -->
In fact, *git pull* is a combination of two commands:
```shell
$ git fetch remote_name branch_name
$ git merge remote_name/branch_name
```

If you want to fetch all branches and merge the current one:

```shell
$ git fetch 
$ git merge
```

---

<!-- .slide: data-background="#ffffff" -->
## Advanced
The command
```shell
$ git push 
```
will send the changes in the current branch to the remote by default.

---

<!-- .slide: data-background="#ffffff" -->

The default behavior can be seen with:
```shell
$ git config --get push.default
```
This can be changed by applying:
```shell
git config --global push.default matching(default), current, ...
```

---

<!-- .slide: data-background="#ffffff" -->
If you have a brand-new branch called **new**, you can push it the first time with the command:

```shell
git push -u origin new
```

which is equivalent to

```shell
git push origin new
git branch --set-upstream new origin/new
```

---

<!-- .slide: data-background="#ffffff" -->
then, you will be able to push/pull the changes in the branch by simply typing **git push/pull**

---

<!-- .slide: data-background="#ffffff" -->
<!-- .slide: style="font-size: 30px;" -->
### Displaying remote information

```console
$ git remote show origin
* remote origin
  Fetch URL: git@bitbucket.org:arm2011/gitcourse.git
  Push  URL: git@bitbucket.org:arm2011/gitcourse.git
  HEAD branch: master
  Remote branches:
    experiment     tracked
    feature        tracked
    less-salt      tracked
    master         tracked
    nested-feature tracked
  Local branches configured for 'git pull':
    feature        merges with remote feature
    master         merges with remote master
    nested-feature merges with remote nested-feature
  Local refs configured for 'git push':
    feature        pushes to feature        (fast-forwardable)
    master         pushes to master         (up to date)
    nested-feature pushes to nested-feature (up to date)
```

---

<!-- .slide: data-background="#ffffff" -->
### Renaming remotes

```shell
$ git remote rename initial_name new_name
```

### Deleting remotes

```shell
$ git remote remove remote_name 
```


---

<!-- .slide: data-background="#ffffff" -->
## Bare repositories

![](https://www.hpc2n.umu.se/sites/default/files/git-folders-bare.png)



A bare repository is a repository with no working directory.

---

<!-- .slide: data-background="#ffffff" -->
### Creating a bare repository

```shell
$ mkdir bare.git && cd bare.git
$ git init --bare
```

### Cloning a bare repository cont.

```shell
$ git clone --bare location
```

---

<!-- .slide: data-background="#ffffff" -->
## Using GitHub

![](https://i.imgur.com/kj3WDWT.jpg)


---

<!-- .slide: data-background="#ffffff" -->

Upon login into your GitHub account you will see the following option to create a new repository

![](https://i.imgur.com/E8lMrMi.jpg)

---

<!-- .slide: data-background="#ffffff" -->
<!-- .slide: style="font-size: 28px;" -->

Here, you can choose the type of repository that is appropriate to your needs (public/private), if you want to add *README* and *.gitignore* files and also the type of license for your project,

![](https://i.imgur.com/un2NdHE.jpg =700x)

---

<!-- .slide: data-background="#ffffff" -->

GitHub will suggest some steps that you can take for your brand-new repository:

![](https://i.imgur.com/9egKoEv.jpg)

---

<!-- .slide: data-background="#ffffff" -->

![](https://i.imgur.com/qlUQxq3.jpg)


---

<!-- .slide: data-background="#ffffff" -->
## Setting ssh-keys

1. ssh-keygen -t rsa -b 4096 -C "pedro@gemail.com"
2. eval $(ssh-agent -s)
3. ssh-add ~/.ssh/id_rsa
4. clip < ~/.ssh/id_rsa.pub (it copies the ssh key that has got generated)


---

<!-- .slide: data-background="#ffffff" -->

5. Go to your remote repository on github.com and then **Settings** -> **SSH and GPG keys** ->new SSH key -> write a title and paste the copied SSH key and save it
6. check if the key was properly set on github/bitbucket 

```
$ ssh -T git@bitbucket.org
$ ssh -T git@github.com
```


---

<!-- .slide: data-background="#ffffff" -->

![](https://i.imgur.com/j1PivRS.jpg)

---

<!-- .slide: data-background="#ffffff" -->
## Network visualization
![](https://i.imgur.com/q9f0ZFH.jpg)


---

<!-- .slide: data-background="#ffffff" -->
## Working with other's repos
In the following scenario, a developer, Bob, has its repo on GitHub. Another developer, Alice, finds it useful. Alice can clone it but she cannot push changes unless Bob allows it:
```graphviz
digraph {
  rankdir=LR
  S [style=invis]
  "Bob repo" [shape=rectangle]
  "Alice cloned" [fixedsize=circle]
  "Bob repo" -> "Alice cloned" [label="cloning"]
  "Alice cloned" -> "Bob repo" [label="cannot commit" fontcolor=red style=dashed color=red]
}
```

---

<!-- .slide: data-background="#ffffff" -->
A better approach is to *fork* Bob's repository: 
```graphviz
digraph {
  rankdir=LR
  S [style=invis]
  "Bob repo" [label="Bob's repo (upstream)" shape=rectangle]
  "Alice fork" [label="Alice's repo (origin)" fixedsize=circle]
  "Alice local" [label="Alice local copy (PC/laptop)" color=darkgreen fontcolor=darkgreen]
  "Alice fork" -> "Alice local" [label="cloning"]
  "Alice local" -> "Alice fork" [label="can commit"]
  "Alice local" -> "Bob repo" [label="cannot commit" fontcolor=red color=red style=dashed]
  "Bob repo" -> "Alice fork" [label="forking"]
  "Alice local" -> "Bob repo" [label="can request pulls" fontcolor=blue color=blue style=dashed]
}
```
In this way, Alice can push changes to her repository and eventually make Bob aware of them as well.

---

<!-- .slide: data-background="#ffffff" -->
## Forking a repository
To fork a repository, Alice go to the URL of the target repository and use the option *Fork* in Bob's repository: 
![forking](https://hackmd.io/_uploads/HJiZrUNm1l.jpg)

---

<!-- .slide: data-background="#ffffff" -->
## Forking a repository
Then, Alice will see the forked repository on her user space:
![forked](https://hackmd.io/_uploads/ry85IUVXyl.jpg)

---

<!-- .slide: data-background="#ffffff" -->
After doing some changes, Alice push them to her forked repository but she wants Bob become aware of them (1 commit in this case, click on this commit)
![pr1](https://hackmd.io/_uploads/S1c02UEXJe.png)

---

<!-- .slide: data-background="#ffffff" -->
## Pull request
A **pull request** will be suggested: 
![pr2](https://hackmd.io/_uploads/HJeBTLEQke.png)

---

<!-- .slide: data-background="#ffffff" -->
You can then create a the PR:
![pr3](https://hackmd.io/_uploads/rkhj6IEm1l.png)


---

<!-- .slide: data-background="#ffffff" -->
Another way to create PR is with "Pull request" option:
![](https://i.imgur.com/9SGeaEk.jpg)

---

<!-- .slide: data-background="#ffffff" -->
<!-- .slide: style="font-size: 30px;" -->

Then, Bob receives an email with the pull request information about Alice modifications. On the GitHub site he sees the request:
![](https://i.imgur.com/JZ73bMu.jpg =700x)

---

<!-- .slide: data-background="#ffffff" -->
Because Bob find the changes from Alice useful and there are no conflicts he can merge them, 
![](https://i.imgur.com/5yiTuCC.jpg)

---

<!-- .slide: data-background="#ffffff" -->
## Issues
If you find some issues in the files/code you can open an "Issue" on GitHub
![](https://i.imgur.com/mJ9NfvF.jpg)

---

<!-- .slide: data-background="#ffffff" -->
![](https://i.imgur.com/1M4f1Nr.jpg)

---

<!-- .slide: data-background="#ffffff" -->
You may also assign people to the issues that are more related to that topic. 

In future commits you may refer to this issue by using the issue number, <span style="color:blue">#2</span> in this case. This will allow you to track the evolution of the issue on GitHub.

---

<!-- .slide: data-background="#ffffff" -->
## Best practices

- Communicate with your colleagues.
- Some commands such as **git rebase** change the history. It wouldn't be a good idea to use them on public branches. 
- Don't accept pull requests right away.



