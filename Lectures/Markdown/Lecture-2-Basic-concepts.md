---
title: "Lecture 2: Basic concepts"
tags: Lecture, Diana, day 1
description: "What are the basic concepts of Git?"
---

Introduction to Git --- Fall 2021
# Lecture 2: Basic concepts

<!-- .slide: data-background="#ffffff" -->

<!-- Lecture material made by Mirko Myllykoski for the version of the course that was given in fall 2020. Lecture was first given by Mirko Myllykoski in fall 2020.-->

![](https://www.hpc2n.umu.se/sites/default/files/umu-logo-left-se.png =250x)  ![](https://www.hpc2n.umu.se/sites/default/files/hpc2n-logo-text5.png =250x)  ![](https://www.hpc2n.umu.se/sites/default/files/images/SNIC_logo_autocrop.png =250x)

<small>Slides: https://hackmd.io/@hpc2n-git-2021/L2-concepts#/</small>

---

## Remark

<!-- .slide: class="fragment" -->

 - You are **not** intended to memorize any commands or low-level details. <!-- .element: class="fragment" -->
 - The goal is to learn the *basic concepts*: <!-- .element: class="fragment" -->
     - hash sums, blobs, trees, commits, references, branches, ...
 - Understanding these concepts helps to understand what the commands actually do! <!-- .element: class="fragment" -->

---

## What is Git?

 - Git is a **distributed** VCS: <!-- .element: class="fragment" -->
     - Does not rely on a server-client model.<!-- .element: class="fragment" -->
     - Instead, everyone has a full copy the entire project (repository). <!-- .element: class="fragment" -->
         - Complete history, metadata, etc. <!-- .element: class="fragment" -->
     - People can work completely independently. <!-- .element: class="fragment" -->
     - An (optional) server is used to only to distribute changes. <!-- .element: class="fragment" -->

---

### Why use Git?

 - It is popular. <!-- .element: class="fragment" -->
     - Many project already use it, people know how to use it, people can tell you how to use it, ... <!-- .element: class="fragment" -->
 - Relies on hash sums: <!-- .element: class="fragment" -->
     - Built-in data corruption detection. <!-- .element: class="fragment" -->
     - Built security. <!-- .element: class="fragment" -->
 - Distributed. <!-- .element: class="fragment" -->
 - Fast, simple and flexible. <!-- .element: class="fragment" -->
 - Free and open-source. <!-- .element: class="fragment" -->

---

## How does Git store the history?

---

### What is inside a repository?

```shell
$ mkdir repository && cd repository
$ git init
Initialized empty Git repository in .../repository/.git/
$ find
```

```graphviz
digraph {
  "repository/" -> ".git/"
  ".git/" -> "branches/"
  ".git/" -> "hooks/"
  ".git/" -> "info/ "
  ".git/" -> "objects/"
  ".git/" -> "refs/"
  ".git/" -> "config"
  ".git/" -> "description"
  ".git/" -> "HEAD"
  "objects/" -> "info/"
  "objects/" -> "pack/"
  "refs/" -> "heads/"
  "refs/" -> "tags/"
}
```

 <!-- .element: class="fragment" -->

---

Most directories are empty and the files are not that interesting:

```shell
$ cat .git/config 
[core]
        repositoryformatversion = 0
        filemode = true
        bare = false
        logallrefupdates = true
$ cat .git/HEAD 
ref: refs/heads/master
$ cat .git/description 
Unnamed repository; edit this file 'description' to name the
repository.
```

---

Lets add some content:

```shell
$ echo "This file is very interesting" > file.txt
$ git add file.txt
$ git commit -m "This is the first commit"
[master (root-commit) 23b3ed5] This is the first commit
 1 file changed, 1 insertion(+)
 create mode 100644 file.txt
$ find
```

```graphviz
digraph {
  "file.txt" [fontcolor=red]
  "logs/" [fontcolor=red]
  "master" [fontcolor=red]
  "COMMIT_EDITMSG" [fontcolor=red]
  "index" [fontcolor=red]
  "23" [fontcolor=red]
  "b3ed5b16..." [fontcolor=red]
  "1a" [fontcolor=red]
  "098a06bf..." [fontcolor=red]
  "09" [fontcolor=red]
  "c78e6e97..." [fontcolor=red]

  "repository/" -> ".git/"
  "repository/" -> "file.txt"
  ".git/" -> "branches/"
  ".git/" -> "hooks/"
  ".git/" -> "info/ "
  ".git/" -> "logs/"
  ".git/" -> "objects/"
  ".git/" -> "refs/"
  ".git/" -> "COMMIT_EDITMSG"
  ".git/" -> "config"
  ".git/" -> "description"
  ".git/" -> "HEAD"
  ".git/" -> "index"
  "objects/" -> "23" -> "b3ed5b16..."
  "objects/" -> "1a" -> "098a06bf..."
  "objects/" -> "09" -> "c78e6e97..."
  "objects/" -> "info/"
  "objects/" -> "pack/"
  "refs/" -> "heads/" -> "master"
  "refs/" -> "tags/"
}
```

 <!-- .element: class="fragment" -->

---

### Working tree

 - Everything inside `repository/` is a part of the *working tree* (or the *workspace*).
     - `.git/` is not included. <!-- .element: class="fragment" -->
     - At the moment, the working tree contains just one file, `file.txt`. <!-- .element: class="fragment" -->
     - Working tree is just a regular directory. <!-- .element: class="fragment" -->
 - The `git add` and `git commit` commands tell Git to care about `file.txt`. <!-- .element: class="fragment" -->
     - More on that later...

---

### Objects

 - Git stores files etc as **objects**:
     - Objects are stored under `.git/objects/`. <!-- .element: class="fragment" -->
 - Git uses *content-based addressing*. <!-- .element: class="fragment" -->
     - A *hash sum* is computed from the **content** of the object. <!-- .element: class="fragment" -->
     - The hash "uniquely" identifies the object. <!-- .element: class="fragment" -->
     - Two objects with identical contents have the same hash and are stored only once. <!-- .element: class="fragment" -->

---

 - We can compute the hash manually:

```shell
$ git hash-object file.txt
09c78e6e971ce9e3d69e75bcb3ffd5de05b0d59a
```

 - We can find the corresponding object: <!-- .element: class="fragment" data-fragment-index="2" -->

```shell
$ find
...
./.git/objects/09/c78e6e971ce9e3d69e75bcb3ffd5de05b0d59a
...
```

 <!-- .element: class="fragment" data-fragment-index="2" -->

 - We can confirm that two files with identical contents have the same hash: <!-- .element: class="fragment" data-fragment-index="3" -->

```shell
$ cp file.txt file2.txt 
$ git hash-object file.txt file2.txt
09c78e6e971ce9e3d69e75bcb3ffd5de05b0d59a
09c78e6e971ce9e3d69e75bcb3ffd5de05b0d59a
```

 <!-- .element: class="fragment" data-fragment-index="3" -->

---

 - Note that we do not have to use the entire hash:

```shell
git cat-file -p 09c78e6e
This file is very interesting
```

 - We only need to use as many characters as is required to uniquely identify the object. <!-- .element: class="fragment" -->
     - 7-8 is enough in most cases.
     - 12 in larger projects.
 - If more characters is required, an error message is printed. <!-- .element: class="fragment" -->

---

 - Objects cannot not (and should not) be accessed directly:

```shell
$ hexdump -C ./.git/objects/09/c78e6e97*
00000000  78 01 4b ca c9 4f 52 30  ....  |x.K..OR06`...,VH|
00000010  cb cc 49 55 00 d2 65 a9  ....  |..IU..e.E...y%.E|
00000020  a9 c5 25 99 79 e9 5c 00  ....  |..%.y.\..I.3|
0000002c
```

 - However, we can observe the type and the content of an object: <!-- .element: class="fragment" data-fragment-index="1" -->

```shell
$ git cat-file -t 09c78e6e
blob
$ git cat-file -p 09c78e6e
This file is very interesting
```

 <!-- .element: class="fragment" data-fragment-index="1" -->

---

 - It is also important to realize that the object stays even when the file is removed:

```shell
$ rm file.txt
$ find
....
./.git/objects/09/c78e6e971ce9e3d69e75bcb3ffd5de05b0d59a
....
$ git cat-file -p 09c78e6e971ce9e3d69e75bcb3ffd5de05b0d59a
This file is very interesting
```

 - We can restore the file from the object: <!-- .element: class="fragment" data-fragment-index="1" -->

```shell
$ git restore file.txt
$ cat file.txt 
This file is very interesting
```

 <!-- .element: class="fragment" data-fragment-index="1" -->

---

Let's take a second look at the repository:

```graphviz
digraph {
  "file.txt"
  "logs/"
  "master"
  "COMMIT_EDITMSG"
  "index"
  "23"
  "b3ed5b16..." [fontcolor=red]
  "1a"
  "098a06bf..." [fontcolor=red]
  "09"
  "c78e6e97..."

  "repository/" -> ".git/"
  "repository/" -> "file.txt"
  ".git/" -> "branches/"
  ".git/" -> "hooks/"
  ".git/" -> "info/ "
  ".git/" -> "logs/"
  ".git/" -> "objects/"
  ".git/" -> "refs/"
  ".git/" -> "COMMIT_EDITMSG"
  ".git/" -> "config"
  ".git/" -> "description"
  ".git/" -> "HEAD"
  ".git/" -> "index"
  "objects/" -> "23" -> "b3ed5b16..."
  "objects/" -> "1a" -> "098a06bf..."
  "objects/" -> "09" -> "c78e6e97..."
  "objects/" -> "info/"
  "objects/" -> "pack/"
  "refs/" -> "heads/" -> "master"
  "refs/" -> "tags/"
}
```

*What are these two other objects?*

---

### Trees

 - Let's investigate one of the remaining objects:

```shell
$ git cat-file -t 1a098a06
tree
$ git cat-file -p 1a098a06
100644 blob 09c78e6e971ce9e3d69e75b....    file.txt
```

 - We can see that the type of the object is **tree**: <!-- .element: class="fragment" -->
     - A tree stores pointers to <!-- .element: class="fragment" -->
         - files (blobs) and 
         - other trees,
     - Trees are used to represent directory structures. <!-- .element: class="fragment" -->

---

In this case, the tree has one level and one blob:

```graphviz
digraph {
  first_blob [label="blob 09c78e6e...\nThis file is very interesting" shape=box]

  "tree 1a098a06b...\nblob 09c78e6e.... file.txt" -> first_blob
}
```

---

Let's take a third look at the repository:

```graphviz
digraph {
  "file.txt"
  "logs/"
  "master"
  "COMMIT_EDITMSG"
  "index"
  "23"
  "b3ed5b16..." [fontcolor=red]
  "1a"
  "098a06bf..."
  "09"
  "c78e6e97..."

  "repository/" -> ".git/"
  "repository/" -> "file.txt"
  ".git/" -> "branches/"
  ".git/" -> "hooks/"
  ".git/" -> "info/ "
  ".git/" -> "logs/"
  ".git/" -> "objects/"
  ".git/" -> "refs/"
  ".git/" -> "COMMIT_EDITMSG"
  ".git/" -> "config"
  ".git/" -> "description"
  ".git/" -> "HEAD"
  ".git/" -> "index"
  "objects/" -> "23" -> "b3ed5b16..."
  "objects/" -> "1a" -> "098a06bf..."
  "objects/" -> "09" -> "c78e6e97..."
  "objects/" -> "info/"
  "objects/" -> "pack/"
  "refs/" -> "heads/" -> "master"
  "refs/" -> "tags/"
}
```

*Just one object remains...*

---

### Commits

 - Let's investigate the last object:

```shell
$ git cat-file -t 23b3ed5b
commit
$ git cat-file -p 23b3ed5b
tree 1a098a06bf0bcae9695238d9d5cb96345c00cacf
author Mirko Myllykoski <....@gmail.com> 1600867851 +0200
committer Mirko Myllykoski <....@gmail.com> 1600867851 +0200

This is the first commit
```

 - The type of the object is **commit**. <!-- .element: class="fragment" --> It contains <!-- .element: class="fragment" -->
     - a pointer to a tree, <!-- .element: class="fragment" -->
     - an author and a committer (+time), and <!-- .element: class="fragment" -->
     - a commit message <!-- .element: class="fragment" -->

---

A commit stores the state of the project in a given point of time.

---

In this case, the commit points to a tree that has one level and one blob:

```graphviz
digraph {
  first_blob [label="blob 09c78e6e...\nThis file is very interesting" shape=box]
  file [label="file.txt\nThis file is very interesting" shape=box]

  "commit 23b3ed5b1...\ntree 1a098a06b\nMirko Myll...\nThis is the first commit" -> "tree 1a098a06b...\nblob 09c78e6e.... file.txt" -> first_blob
  
  "metadata" -> "repository/" -> file
}
```

---

In a more general case, the associated tree can contain **several** levels and **multiple** blobs:

```graphviz
digraph {
  file1 [label="file1.txt" shape=box]
  file2 [label="file2.txt" shape=box]
  file3 [label="file3.txt" shape=box]
  file4 [label="file4.txt" shape=box]

  blob1 [label="blob 1" shape=box]
  blob2 [label="blob 2" shape=box]
  blob3 [label="blob 3" shape=box]
  blob4 [label="blob 4" shape=box]

  "commit 1" -> "tree 1"
  "tree 1" -> blob1
  "tree 1" -> blob2
  "tree 1" -> "tree 2"
  "tree 2" -> blob3
  "tree 2" -> blob4
  
  "metadata" -> "repository/"
  "repository/" -> file1
  "repository/" -> file2
  "repository/" -> "directory/"
  "directory/" -> file3
  "directory/" -> file4
}
```

---

## Working with Git

---

Let's see what else we can find...

```graphviz
digraph {
  "file.txt"
  "logs/"
  "master"
  "COMMIT_EDITMSG"
  "index"
  "23"
  "b3ed5b16..."
  "1a"
  "098a06bf..."
  "09"
  "c78e6e97..."

  "repository/" -> ".git/"
  "repository/" -> "file.txt"
  ".git/" -> "branches/"
  ".git/" -> "hooks/"
  ".git/" -> "info/ "
  ".git/" -> "logs/"
  ".git/" -> "objects/"
  ".git/" -> "refs/"
  ".git/" -> "COMMIT_EDITMSG"
  ".git/" -> "config"
  ".git/" -> "description"
  ".git/" -> "HEAD"
  ".git/" -> "index"
  "objects/" -> "23" -> "b3ed5b16..."
  "objects/" -> "1a" -> "098a06bf..."
  "objects/" -> "09" -> "c78e6e97..."
  "objects/" -> "info/"
  "objects/" -> "pack/"
  "refs/" -> "heads/" -> "master"
  "refs/" -> "tags/"
  
  "HEAD" [fontcolor=red]
  "refs/" [fontcolor=red]
  "heads/" [fontcolor=red]
  "master" [fontcolor=red]
}
```

---

### HEAD and other references

 - `HEAD` points (indirectly) to `23b3ed5b1`:

```shell
$ cat ./.git/HEAD
ref: refs/heads/master
$ cat .git/refs/heads/master
23b3ed5b16095bb84b18d06734fdd614c8982841
```

```graphviz
digraph {
  rankdir=LR
  
  "HEAD" [shape=plaintext]
  "master" [shape=plaintext]
  
  first_blob [label="blob 09c78e6e...\nThis file is very interesting" shape=box]
  
  "HEAD" -> "master" -> "commit\n23b3ed5b1..." -> "tree\n1a098a06b..." -> first_blob
}
```

---

 - `HEAD` and `master` are **references**.
     - A reference points to commits and an other reference. <!-- .element: class="fragment" -->
 - `HEAD` determines "most recent" commit. <!-- .element: class="fragment" -->
     - Many commands **act on the current `HEAD`**. <!-- .element: class="fragment" --> 
     - More on this later <!-- .element: class="fragment" -->
 - `master` is the current branch (more later). <!-- .element: class="fragment" --> 

---

 - You can create a references yourself: 

```shell
$ git tag first
$ find
```

```graphviz
digraph {
  "file.txt"
  "logs/"
  "master"
  "COMMIT_EDITMSG"
  "index"
  "23"
  "b3ed5b16..."
  "1a"
  "098a06bf..."
  "09"
  "c78e6e97..."

  "repository/" -> ".git/"
  "repository/" -> "file.txt"
  ".git/" -> "branches/"
  ".git/" -> "hooks/"
  ".git/" -> "info/ "
  ".git/" -> "logs/"
  ".git/" -> "objects/"
  ".git/" -> "refs/"
  ".git/" -> "COMMIT_EDITMSG"
  ".git/" -> "config"
  ".git/" -> "description"
  ".git/" -> "HEAD"
  ".git/" -> "index"
  "objects/" -> "23" -> "b3ed5b16..."
  "objects/" -> "1a" -> "098a06bf..."
  "objects/" -> "09" -> "c78e6e97..."
  "objects/" -> "info/"
  "objects/" -> "pack/"
  "refs/" -> "heads/" -> "master"
  "refs/" -> "tags/"
  "tags/" -> first
  
  "refs/" [fontcolor=red]
  "tags/" [fontcolor=red]
  "first" [fontcolor=red]
}
```

 <!-- .element: class="fragment" data-fragment-index="2" --> 

```shell
$ git rev-parse first
23b3ed5b16095bb84b18d06734fdd614c8982841
```

 <!-- .element: class="fragment" data-fragment-index="3" -->

```graphviz
digraph {
  rankdir=LR
  
  "first" [shape=plaintext]
  
  first_blob [label="blob 09c78e6e...\nThis file is very interesting" shape=box]
  
  "first" -> "commit\n23b3ed5b1..." -> "tree\n1a098a06b..." -> first_blob
}
```

 <!-- .element: class="fragment" data-fragment-index="3" -->

---

### Index (staging area)

Let's repeat some of the earlier steps:

```shell
$ echo "More content" >> file.txt
$ git add file.txt
$ find
```

<!-- .element: class="fragment" -->

```graphviz
digraph {
  "file.txt" [fontcolor=red]
  "logs/"
  "master"
  "COMMIT_EDITMSG"
  "index"
  "23/"
  "b3ed5b16..."
  "1a/"
  "098a06bf..."
  "09/"
  "c78e6e97..."
  "3b/" [fontcolor=red]
  "23ff0c41..." [fontcolor=red]

  "repository/" -> ".git/"
  "repository/" -> "file.txt"
  ".git/" -> "branches/"
  ".git/" -> "hooks/"
  ".git/" -> "info/ "
  ".git/" -> "logs/"
  ".git/" -> "objects/"
  ".git/" -> "refs/"
  ".git/" -> "COMMIT_EDITMSG"
  ".git/" -> "config"
  ".git/" -> "description"
  ".git/" -> "HEAD"
  ".git/" -> "index"
  "objects/" -> "23/" -> "b3ed5b16..."
  "objects/" -> "1a/" -> "098a06bf..."
  "objects/" -> "09/" -> "c78e6e97..."
  "objects/" -> "3b/" -> "23ff0c41..."
  "objects/" -> "info/"
  "objects/" -> "pack/"
  "refs/" -> "heads/" -> "master"
  "refs/" -> "tags/"
  "tags/" -> first
}
```

<!-- .element: class="fragment" -->

```shell
$ git cat-file -p 3b23ff0c
This file is very interesting
More content
```

<!-- .element: class="fragment" -->

---

 - The `git add` command creates a blob that correspond to the update `file.txt` file.
     - No other object are created yet. <!-- .element: class="fragment" -->
 - The command also adds the file to the **index**. <!-- .element: class="fragment" -->
 - The index will become the **next commit**. <!-- .element: class="fragment" -->
     - Contains a representation of the tree object. <!-- .element: class="fragment" -->

---

The index is a binary file:

```graphviz
digraph {
  "file.txt"
  "logs/"
  "master"
  "COMMIT_EDITMSG"
  "index" [fontcolor=red]
  "23/"
  "b3ed5b16..."
  "1a/"
  "098a06bf..."
  "09/"
  "c78e6e97..."
  "3b/"
  "23ff0c41..." 

  "repository/" -> ".git/"
  "repository/" -> "file.txt"
  ".git/" -> "branches/"
  ".git/" -> "hooks/"
  ".git/" -> "info/ "
  ".git/" -> "logs/"
  ".git/" -> "objects/"
  ".git/" -> "refs/"
  ".git/" -> "COMMIT_EDITMSG"
  ".git/" -> "config"
  ".git/" -> "description"
  ".git/" -> "HEAD"
  ".git/" -> "index"
  "objects/" -> "23/" -> "b3ed5b16..."
  "objects/" -> "1a/" -> "098a06bf..."
  "objects/" -> "09/" -> "c78e6e97..."
  "objects/" -> "3b/" -> "23ff0c41..."
  "objects/" -> "info/"
  "objects/" -> "pack/"
  "refs/" -> "heads/" -> "master"
  "refs/" -> "tags/"
  "tags/" -> first
}
```

---

We can now turn the index to the next commit:

```shell
$ git commit -m "This is the second commit"
[master d3c6c63] This is the second commit
 1 file changed, 1 insertion(+)
$ find
```

```graphviz
digraph {
  "file.txt"
  "logs/"
  "master"
  "COMMIT_EDITMSG"
  "index"
  "23/"
  "b3ed5b16..."
  "1a/"
  "098a06bf..."
  "09/"
  "c78e6e97..."
  "3b/"
  "23ff0c41..."
  "22/" [fontcolor=red]
  "b5208beb..." [fontcolor=red]
  "d3/" [fontcolor=red]
  "c6c635fb..." [fontcolor=red]

  "repository/" -> ".git/"
  "repository/" -> "file.txt"
  ".git/" -> "branches/"
  ".git/" -> "hooks/"
  ".git/" -> "info/ "
  ".git/" -> "logs/"
  ".git/" -> "objects/"
  ".git/" -> "refs/"
  ".git/" -> "COMMIT_EDITMSG"
  ".git/" -> "config"
  ".git/" -> "description"
  ".git/" -> "HEAD"
  ".git/" -> "index"
  "objects/" -> "23/" -> "b3ed5b16..."
  "objects/" -> "1a/" -> "098a06bf..."
  "objects/" -> "09/" -> "c78e6e97..."
  "objects/" -> "3b/" -> "23ff0c41..."
  "objects/" -> "22/" -> "b5208beb..."
  "objects/" -> "d3/" -> "c6c635fb..."
  "objects/" -> "info/"
  "objects/" -> "pack/"
  "refs/" -> "heads/" -> "master"
  "refs/" -> "tags/"
  "tags/" -> first
}
```

 <!-- .element: class="fragment" -->

---

 - Just as before, we have a tree object that describes the directory structure:

```shell
$ git cat-file -p 22b5208b
100644 blob 3b23ff0c411faf22c9253ed0....    file.txt
```

 - And a commit, that describes the state of the repository: <!-- .element: class="fragment" data-fragment-index="1" -->

```shell
$ git cat-file -p d3c6c635
tree 22b5208bebacfcf745691f799b08df492b2a7da9
parent 23b3ed5b16095bb84b18d06734fdd614c8982841
author Mirko Myllykoski <mirko...> 1601228824 +0200
committer Mirko Myllykoski <mirko....> 1601228824 +0200

This is the second commit
```

 <!-- .element: class="fragment" data-fragment-index="1" -->

---

### Parent

 - The major difference is that the commit contains a pointer to a **parent**:

```
parent 23b3ed5b16095bb84b18d06734fdd614c8982841
```

 - The parent pointer points to the previous commit: <!-- .element: class="fragment" data-fragment-index="1" -->

```graphviz
digraph {
  rankdir=LR
  
  second_commit [label="commit d3c6c635...\ntree 22b5208b\nparent 23b3ed5b1\nMirko Myll..\nThis is the second commit"]
  first_commit [label="commit 23b3ed5b1...\ntree 1a098a06b\nMirko Myll...\nThis is the first commit"]
  
  second_blob [label="blob 3b23ff0c\nThis file is very interesting\nMore content" shape=box]
  first_blob [label="blob 09c78e6e...\nThis file is very interesting" shape=box]
  
  second_commit -> "tree 22b5208b...\nblob 3b23ff0c file.txt" -> second_blob

  first_commit -> "tree 1a098a06b...\nblob 09c78e6e.... file.txt" -> first_blob
  
  second_commit -> first_commit
}
```

 <!-- .element: class="fragment" data-fragment-index="1" -->

---

### Commit tree

 - Usually, we have a complete tree of commits (**commit tree**):

```graphviz
digraph {
  rankdir=LR
  "commit 1" -> "tree 1"
  "commit 2" -> "tree 2"
  "commit 2" -> "commit 1"
  "commit 3" -> "tree 3"
  "commit 3" -> "commit 2"
  "commit 4" -> "tree 4"
  "commit 4" -> "commit 3"
}
```

 - Each commit represents the state of the repository at a given point of time. <!-- .element: class="fragment" -->

---

 - Each commit is allowed to have **multiple** parents:

```graphviz
digraph {
  rankdir=LR
  "commit 2" -> "commit 1"
  "commit 4" -> "commit 3"
  "commit 4" -> "commit 2"
}
```

 - These parents appear when two (or more) *branches* are **merged**. <!-- .element: class="fragment" -->
     - More on this later...

---

### HEAD and other references (again)

 - Let's investigate `HEAD` and `master`:

```shell
$ cat .git/HEAD 
ref: refs/heads/master
$ cat .git/refs/heads/master
d3c6c635fb44c7084797d47050bff7961853c19b
```

```graphviz
digraph {
  rankdir=LR
  
  "HEAD" [shape=plaintext]
  "master" [shape=plaintext]
  
  second_commit [label="commit d3c6c635...\ntree 22b5208b\nparent 23b3ed5b1\nMirko Myll..\nThis is the second commit"]

  first_commit [label="commit 23b3ed5b1...\ntree 1a098a06b\nMirko Myll...\nThis is the first commit"]
  
  second_commit -> first_commit
  
  "HEAD" -> "master" -> second_commit
  
  subgraph cluster_working_tree {
    label="Working tree"
    subgraph cluster_file {
      label="file.txt"
        "This file is very interesting\nMore content
" [shape=plain]
    }
  }
}
```

 - Remember, many Git commands act on the current `HEAD`. <!-- .element: class="fragment" -->

---

 - We can change the `HEAD` to something else:

```shell
$ git checkout 23b3ed5b
....
HEAD is now at 23b3ed5 This is the first commit
$ cat .git/HEAD 
23b3ed5b16095bb84b18d06734fdd614c8982841
$ cat file.txt 
This file is very interesting
```

```graphviz
digraph {
  rankdir=LR
  
  "HEAD" [shape=plaintext]
  "master" [shape=plaintext]
  
  second_commit [label="commit d3c6c635...\ntree 22b5208b\nparent 23b3ed5b1\nMirko Myll..\nThis is the second commit"]

  first_commit [label="commit 23b3ed5b1...\ntree 1a098a06b\nMirko Myll...\nThis is the first commit"]
  
  second_commit -> first_commit
  
  "HEAD" -> first_commit 
  "master" -> second_commit
  
  subgraph cluster_working_tree {
    label="Working tree"
    subgraph cluster_file {
      label="file.txt"
        "This file is very interesting
" [shape=plain]
    }
  }
}
```

---

### Branches

 - We can modify the working tree and create a new commit:

```shell
$ echo "Different content" >> file.txt 
$ git commit -a -m "This is the third commit"
[detached HEAD a118ae8] This is the third commit
 1 file changed, 1 insertion(+)
```

 - Let's investigate the newly created commit: <!-- .element: class="fragment" data-fragment-index="1" -->

```shell
$ git cat-file -p a118ae8c
tree 5fcc4f83fedf5a94cd773704bdb1ab2cdcadc6fd
parent 23b3ed5b16095bb84b18d06734fdd614c8982841
author Mirko Myllykoski <mirko....> 1601286412 +0200
committer Mirko Myllykoski <mirko....> 1601286412 +0200

This is the third commit
```

 <!-- .element: class="fragment" data-fragment-index="1" -->

---

 - First, the `parent` points to the **first commit**:

```graphviz
digraph {
  rankdir=LR
  
  third_commit [label="commit a118ae8c...\nparent 23b3ed5b1...\nThis is the third commit"]
  first_commit [label="commit 23b3ed5b1...\nThis is the first commit"]
  
  third_commit -> first_commit
}
```

 - Second, the commit tree now has **two** branches: <!-- .element: class="fragment" data-fragment-index="1" -->

```graphviz
digraph {
  rankdir=LR
  
  "HEAD" [shape=plaintext]
  "master" [shape=plaintext]
  
  third_commit [label="commit a118ae8c...\nThis is the third commit"]
  second_commit [label="commit d3c6c635...\nThis is the second commit"]
  first_commit [label="commit 23b3ed5b1...\nThis is the first commit"]
  
  third_blob [label="blob ea5f4b8e\nThis file is very interesting\nDifferent content" shape=box]
  second_blob [label="blob 3b23ff0c\nThis file is very interesting\nMore content" shape=box]
  first_blob [label="blob 09c78e6e...\nThis file is very interesting" shape=box]
  
  third_commit -> third_blob [style=dashed]
  second_commit -> second_blob [style=dashed]
  first_commit -> first_blob [style=dashed]
  
  third_commit -> first_commit
  second_commit -> first_commit
  
  "HEAD" -> third_commit 
  "master" -> second_commit
  
  subgraph cluster_working_tree {
    label="Working tree"
    subgraph cluster_file {
      label="file.txt"
        "This file is very interesting\nDifferent content
" [shape=plain]
    }
  }
}
```

 <!-- .element: class="fragment" data-fragment-index="1" -->

---

We can give the second brach a **name**:

```shell
$ git checkout -b second_branch
Switched to a new branch 'second_branch'
$ cat .git/HEAD 
ref: refs/heads/second_branch
$ cat .git/refs/heads/second_branch
a118ae8cda10a8f0a966ab7b9158b4a6d3b48cfc
```

```graphviz
digraph {
  rankdir=LR
  
  "HEAD" [shape=plaintext]
  "master" [shape=plaintext]
  "second_branch" [shape=plaintext]
  
  third_commit [label="commit a118ae8c...\nThis is the third commit"]
  second_commit [label="commit d3c6c635...\nThis is the second commit"]
  first_commit [label="commit 23b3ed5b1...\nThis is the first commit"]
  
  third_blob [label="blob ea5f4b8e\nThis file is very interesting\nDifferent content" shape=box]
  second_blob [label="blob 3b23ff0c\nThis file is very interesting\nMore content" shape=box]
  first_blob [label="blob 09c78e6e...\nThis file is very interesting" shape=box]
  
  third_commit -> third_blob [style=dashed]
  second_commit -> second_blob [style=dashed]
  first_commit -> first_blob [style=dashed]
  
  third_commit -> first_commit
  second_commit -> first_commit
  
  "HEAD" -> third_commit
  "master" -> second_commit
  "second_branch" -> third_commit
  
  subgraph cluster_working_tree {
    label="Working tree"
    subgraph cluster_file {
      label="file.txt"
        "This file is very interesting\nDifferent content
" [shape=plain]
    }
  }
}
```

---

### Merging

We can **merge** the two branches together:

```shell
$ git checkout master
$ git merge --no-ff second_branch
Auto-merging file.txt
CONFLICT (content): Merge conflict in file.txt
Automatic merge failed; fix conflicts and then commit the
result.
$ vim file.txt
```

We fix some **conflicts** at this point...

```shell
$ git add file.txt
$ git merge --continue
[master f0d7298] Merge branch 'second_branch'
```

---

The created commit has **two** parents:

```shell
$ git cat-file -p f0d72989
tree f63f3a4c548f5065cee598bed4ae189bd2c099d8
parent d3c6c635fb44c7084797d47050bff7961853c19b
parent a118ae8cda10a8f0a966ab7b9158b4a6d3b48cfc
author Mirko Myllykoski <mirko....> 1601288485 +0200
committer Mirko Myllykoski <mirko....> 1601288485 +0200

Merge branch 'second_branch'
```

---

Finally, the tree looks like follows:

```graphviz
digraph {
  rankdir=LR
  
  "HEAD" [shape=plaintext]
  "master" [shape=plaintext]
  "second_branch" [shape=plaintext]
  
  fourth_commit [label="commit f0d72989...\nMerge branch 'second_branch'
"]
  third_commit [label="commit a118ae8c...\nThis is the third commit"]
  second_commit [label="commit d3c6c635...\nThis is the second commit"]
  first_commit [label="commit 23b3ed5b1...\nThis is the first commit"]
  
  fourth_blob [label="blob e51364b9\nThis file is very interesting\nMore content\nDifferent content" shape=box]
  third_blob [label="blob ea5f4b8e\nThis file is very interesting\nDifferent content" shape=box]
  second_blob [label="blob 3b23ff0c\nThis file is very interesting\nMore content" shape=box]
  first_blob [label="blob 09c78e6e...\nThis file is very interesting" shape=box]
  
  fourth_commit -> fourth_blob [style=dashed]
  third_commit -> third_blob [style=dashed]
  second_commit -> second_blob [style=dashed]
  first_commit -> first_blob [style=dashed]
  
  fourth_commit -> second_commit
  fourth_commit -> third_commit
  third_commit -> first_commit
  second_commit -> first_commit
  
  "HEAD" -> fourth_commit
  "master" -> fourth_commit
  "second_branch" -> third_commit
  
  subgraph cluster_working_tree {
    label="Working tree"
    subgraph cluster_file {
      label="file.txt"
        "This file is very interesting\nMore content\nDifferent content
" [shape=plain]
    }
  }
}
```

---

### Switching to a specific commit

We can always move back to any of the previous commits:

```shell
$ git checkout 23b3ed5b1
....
HEAD is now at 23b3ed5 This is the first commit
$ cat file.txt 
This file is very interesting
```

```graphviz
digraph {
  rankdir=LR
  
  "HEAD" [shape=plaintext]
  "master" [shape=plaintext]
  "second_branch" [shape=plaintext]
  
  fourth_commit [label="commit f0d72989...\nMerge branch 'second_branch'
"]
  third_commit [label="commit a118ae8c...\nThis is the third commit"]
  second_commit [label="commit d3c6c635...\nThis is the second commit"]
  first_commit [label="commit 23b3ed5b1...\nThis is the first commit"]
  
  fourth_blob [label="blob e51364b9\nThis file is very interesting\nMore content\nDifferent content" shape=box]
  third_blob [label="blob ea5f4b8e\nThis file is very interesting\nDifferent content" shape=box]
  second_blob [label="blob 3b23ff0c\nThis file is very interesting\nMore content" shape=box]
  first_blob [label="blob 09c78e6e...\nThis file is very interesting" shape=box]
  
  fourth_commit -> fourth_blob [style=dashed]
  third_commit -> third_blob [style=dashed]
  second_commit -> second_blob [style=dashed]
  first_commit -> first_blob [style=dashed]
  
  fourth_commit -> second_commit
  fourth_commit -> third_commit
  third_commit -> first_commit
  second_commit -> first_commit
  
  "HEAD" -> first_commit
  "master" -> fourth_commit
  "second_branch" -> third_commit
  
  subgraph cluster_working_tree {
    label="Working tree"
    subgraph cluster_file {
      label="file.txt"
        "This file is very interesting" [shape=plain]
    }
  }
}
```

---

The end.

And idea: Try to play with different commands. See what happens to the `.git/` directory.
