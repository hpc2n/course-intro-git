---
title: "Lecture 3: Basic concepts"
tags: Lecture, Birgitte, day 2
description: "What are the basic concepts of Git?"
---

<!-- Lecture material made by Mirko Myllykoski for the version of the course that was given in fall 2020. Lecture was first given by Mirko Myllykoski in fall 2020. Various small changes done by Birgitte Brydsö for the fall 2023 and fall 2024 versions of the course.-->

<!-- Slides: https://hackmd.io/@git-fall-2024/L3-concepts -->

# Lecture 3: Basic concepts 

---

## Remark

- You are **not** intended to memorize any commands or low-level details. 
- The goal is to learn the *basic concepts*: 
    - hash sums, blobs, trees, commits, references, branches, ...
- Understanding these concepts helps to understand what the commands actually do!

---

## What is Git?

- Git is a **distributed** VCS: 
    - Does not rely on a server-client model.
    - Instead, everyone has a full copy of the entire project (repository).
        - Complete history, metadata, etc.
    - People can work completely independently. 
    - An (optional) server is used only to distribute changes. 

---

### Why use Git?

- It is popular.
    - Many project already use it, people know how to use it, people can tell you how to use it, ...
- Relies on hash sums: 
    - Built-in data corruption detection.
    - Built-in security.
- Distributed.
- Fast, simple and flexible.
- Free and open-source.

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

```mermaid
graph TD
  A(["repository/"]) 
  B([".git/"])
  A --> B
  B --> C(["branches/"])
  B --> D(["hooks/"])
  B --> E(["info/ "])
  B --> F(["objects/"])
  B --> G(["refs/"])
  B --> H(["config"])
  B --> I(["description"])
  B --> J(["HEAD"])
  F --> K(["info/"])
  F --> L(["pack/"])
  G --> M(["heads/"])
  G --> N(["tags/"])
  
```

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

Let's add some content:

```shell
$ echo "This file is very interesting" > file.txt
$ git add file.txt
$ git commit -m "This is the first commit"
[master (root-commit) 23b3ed5] This is the first commit
 1 file changed, 1 insertion(+)
 create mode 100644 file.txt
$ find
```

```mermaid
graph TD 
  A(["repository/"])
  B(["file.txt"]) 
  style B color:#FF0000
  C([".git/"])
  D(["logs/"]) 
  style D color:#FF0000
  E(["COMMIT_EDITMSG"])
  style E color:#FF0000
  F(["index"])
  style F color:#FF0000
  G(["branches/"])
  H(["hooks/"])
  I(["objects/"])
  J(["refs/"])
  K(["config"])
  L(["description"])
  M(["HEAD"])
  N(["info/ "])
  O(["23"])
  style O color:#FF0000
  P(["1a"])
  style P color:#FF0000
  Q(["09"])
  style Q color:#FF0000
  R(["info/ "])
  S(["pack/"])
  T(["heads/"])
  U(["tags/"]) 
  V(["b3ed5b16..."])
  style V color:#FF0000
  W(["098a06bf..."])
  style W color:#FF0000
  X(["c78e6e97..."])
  style X color:#FF0000
  Y(["master"])
  style Y color:#FF0000
 
  A --> B
  A --> C
  C --> D
  C --> E
  C --> F
  C --> G
  C --> H
  C --> I
  C --> J
  C --> K
  C --> L 
  C --> M
  C --> N
  I --> O
  I --> P
  I --> Q
  I --> R
  I --> S
  J --> T
  J --> U
  O --> V
  P --> W
  Q --> X
  T --> Y
```

---

### Working tree

- Everything inside `repository/` is a part of the *working tree* (or the *workspace*).
    - `.git/` is not included.
    - At the moment, the working tree contains just one file, `file.txt`.
    - Working tree is just a regular directory.
- The `git add` and `git commit` commands tell Git to care about `file.txt`.
    - More on that later...

---

### Objects

- Git stores files etc as **objects**:
    - Objects are stored under `.git/objects/`.
- Git uses *content-based addressing*.
    - A *hash sum* is computed from the **content** of the object.
    - The hash "uniquely" identifies the object.
    - Two objects with identical contents have the same hash and are stored only once.

---

- We can compute the hash manually:

```shell
$ git hash-object file.txt
09c78e6e971ce9e3d69e75bcb3ffd5de05b0d59a
```

- We can find the corresponding object:

```shell
$ find
...
./.git/objects/09/c78e6e971ce9e3d69e75bcb3ffd5de05b0d59a
...
```

- We can confirm that two files with identical contents have the same hash:

```shell
$ cp file.txt file2.txt 
$ git hash-object file.txt file2.txt
09c78e6e971ce9e3d69e75bcb3ffd5de05b0d59a
09c78e6e971ce9e3d69e75bcb3ffd5de05b0d59a
```

---

- Note that we do not have to use the entire hash:

```shell
git cat-file -p 09c78e6e
This file is very interesting
```

- We only need to use as many characters as is required to uniquely identify the object.
    - 7-8 is enough in most cases.
    - 12 in larger projects.
- If more characters is required, an error message is printed.

---

- Objects cannot (and should not) be accessed directly:

```shell
$ hexdump -C ./.git/objects/09/c78e6e97*
00000000  78 01 4b ca c9 4f 52 30  ....  |x.K..OR06`...,VH|
00000010  cb cc 49 55 00 d2 65 a9  ....  |..IU..e.E...y%.E|
00000020  a9 c5 25 99 79 e9 5c 00  ....  |..%.y.\..I.3|
0000002c
```

- However, we can observe the type and the content of an object:

```shell
$ git cat-file -t 09c78e6e
blob
$ git cat-file -p 09c78e6e
This file is very interesting
```

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

- We can restore the file from the object:

```shell
$ git restore file.txt
$ cat file.txt 
This file is very interesting
```

---

Let's take a second look at the repository:

```mermaid
graph TD
  A(["repository/"])
  B(["file.txt"])
  C([".git/"])
  D(["logs/"])
  E(["COMMIT_EDITMSG"])
  F(["index"])
  G(["branches/"])
  H(["hooks/"])
  I(["objects/"])
  J(["refs/"])
  K(["config"])
  L(["description"])
  M(["HEAD"])
  N(["info/ "])
  O(["23"])
  P(["1a"])
  Q(["09"])
  R(["info/ "])
  S(["pack/"])
  T(["heads/"])
  U(["tags/"])
  V(["b3ed5b16..."])
  style V color:#FF0000
  W(["098a06bf..."])
  style W color:#FF0000
  X(["c78e6e97..."])
  Y(["master"])

  A --> B
  A --> C
  C --> D
  C --> E
  C --> F
  C --> G
  C --> H
  C --> I
  C --> J
  C --> K
  C --> L
  C --> M
  C --> N
  I --> O
  I --> P
  I --> Q
  I --> R
  I --> S
  J --> T
  J --> U
  O --> V
  P --> W
  Q --> X
  T --> Y
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

- We can see that the type of the object is **tree**:
    - A tree stores pointers to
        - files (blobs) and 
        - other trees,
    - Trees are used to represent directory structures.

---

In this case, the tree has one level and one blob:

```mermaid
graph TD
  first_blob["blob 09c78e6e...<br>This file is very interesting"]

  tree(["tree 1a098a06b...<br>blob 09c78e6e.... file.txt"]) --> first_blob
```

---

Let's take a third look at the repository:

```mermaid
graph TD
  A(["repository/"])
  B(["file.txt"])
  C([".git/"])
  D(["logs/"])
  E(["COMMIT_EDITMSG"])
  F(["index"])
  G(["branches/"])
  H(["hooks/"])
  I(["objects/"])
  J(["refs/"])
  K(["config"])
  L(["description"])
  M(["HEAD"])
  N(["info/ "])
  O(["23"])
  P(["1a"])
  Q(["09"])
  R(["info/ "])
  S(["pack/"])
  T(["heads/"])
  U(["tags/"])
  V(["b3ed5b16..."])
  style V color:#FF0000
  W(["098a06bf..."])
  X(["c78e6e97..."])
  Y(["master"])

  A --> B
  A --> C
  C --> D
  C --> E
  C --> F
  C --> G
  C --> H
  C --> I
  C --> J
  C --> K
  C --> L
  C --> M
  C --> N
  I --> O
  I --> P
  I --> Q
  I --> R
  I --> S
  J --> T
  J --> U
  O --> V
  P --> W
  Q --> X
  T --> Y
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

- The type of the object is **commit**. It contains 
    - a pointer to a tree, 
    - an author and a committer (+time), and 
    - a commit message 

---

A commit stores the state of the project in a given point of time.

---

In this case, the commit points to a tree that has one level and one blob:

```mermaid
graph TD
  first_blob["blob 09c78e6e...<br>This file is very interesting"]
  file["file.txt<br>This file is very interesting"]

  commit(["commit 23b3ed5b1...<br>tree 1a098a06b<br>Mirko Myll...<br>This is the first commit"]) --> tree(["tree 1a098a06b...<br>blob 09c78e6e.... file.txt"]) --> first_blob
  
  metadata(["metadata"]) --> repo(["repository/"]) --> file
```

---

In a more general case, the associated tree can contain **several** levels and **multiple** blobs:

```mermaid
graph TD
  file1["file1.txt"]
  file2["file2.txt"]
  file3["file3.txt"]
  file4["file4.txt"]

  blob1["blob 1"]
  blob2["blob 2"]
  blob3["blob 3"]
  blob4["blob 4"]

  commit1(["commit 1"]) --> tree1(["tree 1"])
  tree1 --> blob1
  tree1 --> blob2
  tree1 --> tree2(["tree 2"])
  tree2 --> blob3
  tree2 --> blob4
  
  metadata(["metadata"]) --> repo(["repository/"])
  repo --> file1
  repo --> file2
  repo --> dir(["directory/"])
  dir --> file3
  dir --> file4
```

---

## Working with Git

---

Let's see what else we can find...

```mermaid
graph TD
  A(["repository/"])
  B(["file.txt"])
  C([".git/"])
  D(["logs/"])
  E(["COMMIT_EDITMSG"])
  F(["index"])
  G(["branches/"])
  H(["hooks/"])
  I(["objects/"])
  J(["refs/"])
  style J color:#FF0000
  K(["config"])
  L(["description"])
  M(["HEAD"])
  style M color:#FF0000
  N(["info/ "])
  O(["23"])
  P(["1a"])
  Q(["09"])
  R(["info/ "])
  S(["pack/"])
  T(["heads/"])
  style T color:#FF0000
  U(["tags/"])
  V(["b3ed5b16..."])
  W(["098a06bf..."])
  X(["c78e6e97..."])
  Y(["master"])
  style Y color:#FF0000

  A --> B
  A --> C
  C --> D
  C --> E
  C --> F
  C --> G
  C --> H
  C --> I
  C --> J
  C --> K
  C --> L
  C --> M
  C --> N
  I --> O
  I --> P
  I --> Q
  I --> R
  I --> S
  J --> T
  J --> U
  O --> V
  P --> W
  Q --> X
  T --> Y
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

```mermaid
graph LR
  
  head["HEAD"]
  style head fill:#ffffff,stroke:#ffffff
  master["master"]
  style master fill:#ffffff, stroke:#ffffff
  
  first_blob["blob 09c78e6e...<br>This file is very interesting"]
  
  head --> master --> commit(["commit<br>23b3ed5b1..."]) --> tree(["tree<br>1a098a06b..."]) --> first_blob
```

---

- `HEAD` and `master` are **references**.
    - A reference points to commits and another reference.
- `HEAD` determines "most recent" commit.
    - Many commands **act on the current `HEAD`**. 
    - More on this later
- `master` is the current branch (more later). 

---

- You can create a reference yourself: 

```shell
$ git tag first
$ find
```

```mermaid
graph TD
  A(["repository/"])
  B(["file.txt"])
  C([".git/"])
  D(["logs/"])
  E(["COMMIT_EDITMSG"])
  F(["index"])
  G(["branches/"])
  H(["hooks/"])
  I(["objects/"])
  J(["refs/"])
  style J color:#FF0000
  K(["config"])
  L(["description"])
  M(["HEAD"])
  N(["info/ "])
  O(["23"])
  P(["1a"])
  Q(["09"])
  R(["info/ "])
  S(["pack/"])
  T(["heads/"])
  U(["tags/"])
  style U color:#FF0000
  V(["b3ed5b16..."])
  W(["098a06bf..."])
  X(["c78e6e97..."])
  Y(["master"])
  Z(["first"])
  style Z color:#FF0000

  A --> B
  A --> C
  C --> D
  C --> E
  C --> F
  C --> G
  C --> H
  C --> I
  C --> J
  C --> K
  C --> L
  C --> M
  C --> N
  I --> O
  I --> P
  I --> Q
  I --> R
  I --> S
  J --> T
  J --> U
  O --> V
  P --> W
  Q --> X
  T --> Y
  U --> Z
```

```shell
$ git rev-parse first
23b3ed5b16095bb84b18d06734fdd614c8982841
```

```mermaid
graph LR
  
  first["first"]
  style first fill:#ffffff,stroke:#ffffff
  
  first_blob["blob 09c78e6e...<br>This file is very interesting"]
  
  first --> commit(["commit<br>23b3ed5b1..."]) --> tree(["tree<br>1a098a06b..."]) --> first_blob
```

---

### Index (staging area)

Let's repeat some of the earlier steps:

```shell
$ echo "More content" >> file.txt
$ git add file.txt
$ find
```

```mermaid
graph TD
  A(["repository/"])
  B(["file.txt"])
  style B color:#FF0000
  C([".git/"])
  D(["logs/"])
  E(["COMMIT_EDITMSG"])
  F(["index"])
  G(["branches/"])
  H(["hooks/"])
  I(["objects/"])
  J(["refs/"])
  K(["config"])
  L(["description"])
  M(["HEAD"])
  N(["info/ "])
  O(["23"])
  P(["1a"])
  Q(["09"])
  QR(["3b"])
  style QR color:#FF0000
  R(["info/ "])
  S(["pack/"])
  T(["heads/"])
  U(["tags/"])
  V(["b3ed5b16..."])
  W(["098a06bf..."])
  X(["c78e6e97..."])
  XY(["23ff0c41..."])
  style XY color:#FF0000
  Y(["master"])
  Z(["first"])

  A --> B
  A --> C
  C --> D
  C --> E
  C --> F
  C --> G
  C --> H
  C --> I
  C --> J
  C --> K
  C --> L
  C --> M
  C --> N
  I --> O
  I --> P
  I --> Q
  I --> QR
  I --> R
  I --> S
  J --> T
  J --> U
  O --> V
  P --> W
  Q --> X
  QR --> XY
  T --> Y
  U --> Z
```

```shell
$ git cat-file -p 3b23ff0c
This file is very interesting
More content
```

---

- The `git add` command creates a blob that correspond to the update `file.txt` file.
    - No other object are created yet.
- The command also adds the file to the **index**.
- The index will become the **next commit**.
    - Contains a representation of the tree object.

---

The index is a binary file:

```mermaid
graph TD
  A(["repository/"])
  B(["file.txt"])
  C([".git/"])
  D(["logs/"])
  E(["COMMIT_EDITMSG"])
  F(["index"])
  style F color:#FF0000
  G(["branches/"])
  H(["hooks/"])
  I(["objects/"])
  J(["refs/"])
  K(["config"])
  L(["description"])
  M(["HEAD"])
  N(["info/ "])
  O(["23"])
  P(["1a"])
  Q(["09"])
  QR(["3b"])
  R(["info/ "])
  S(["pack/"])
  T(["heads/"])
  U(["tags/"])
  V(["b3ed5b16..."])
  W(["098a06bf..."])
  X(["c78e6e97..."])
  XY(["23ff0c41..."])
  Y(["master"])
  Z(["first"])

  A --> B
  A --> C
  C --> D
  C --> E
  C --> F
  C --> G
  C --> H
  C --> I
  C --> J
  C --> K
  C --> L
  C --> M
  C --> N
  I --> O
  I --> P
  I --> Q
  I --> QR
  I --> R
  I --> S
  J --> T
  J --> U
  O --> V
  P --> W
  Q --> X
  QR --> XY
  T --> Y
  U --> Z
```

---

We can now turn the index to the next commit:

```shell
$ git commit -m "This is the second commit"
[master d3c6c63] This is the second commit
 1 file changed, 1 insertion(+)
$ find
```

```mermaid
graph TD
  A(["repository/"])
  B(["file.txt"])
  C([".git/"])
  D(["logs/"])
  E(["COMMIT_EDITMSG"])
  F(["index"])
  G(["branches/"])
  H(["hooks/"])
  I(["objects/"])
  J(["refs/"])
  K(["config"])
  L(["description"])
  M(["HEAD"])
  N(["info/ "])
  O(["23"])
  P(["1a"])
  Q(["09"])
  QR(["3b"])
  QRR(["22/"])
  style QRR color:#FF0000
  QRRR(["d3/"])
  style QRRR color:#FF0000
  R(["info/ "])
  S(["pack/"])
  T(["heads/"])
  U(["tags/"])
  V(["b3ed5b16..."])
  W(["098a06bf..."])
  X(["c78e6e97..."])
  XY(["23ff0c41..."])
  XYY(["b5208beb..."])
  style XYY color:#FF0000
  XYYY(["c6c635fb..."])
  style XYYY color:#FF0000
  Y(["master"])
  Z(["first"])

  A --> B
  A --> C
  C --> D
  C --> E
  C --> F
  C --> G
  C --> H
  C --> I
  C --> J
  C --> K
  C --> L
  C --> M
  C --> N
  I --> O
  I --> P
  I --> Q
  I --> QR
  I --> QRR
  I --> QRRR
  I --> R
  I --> S
  J --> T
  J --> U
  O --> V
  P --> W
  Q --> X
  QR --> XY
  QRR --> XYY
  QRRR --> XYYY
  T --> Y
  U --> Z
```

---

 - Just as before, we have a tree object that describes the directory structure:

```shell
$ git cat-file -p 22b5208b
100644 blob 3b23ff0c411faf22c9253ed0....    file.txt
```

- And a commit, that describes the state of the repository:

```shell
$ git cat-file -p d3c6c635
tree 22b5208bebacfcf745691f799b08df492b2a7da9
parent 23b3ed5b16095bb84b18d06734fdd614c8982841
author Mirko Myllykoski <mirko...> 1601228824 +0200
committer Mirko Myllykoski <mirko....> 1601228824 +0200

This is the second commit
```

---

### Parent

- The major difference is that the commit contains a pointer to a **parent**:

```
parent 23b3ed5b16095bb84b18d06734fdd614c8982841
```

- The parent pointer points to the previous commit: 

```mermaid
graph LR
  secondcommit(["commit d3c6c635...<br>tree 22b5208b<br>parent 23b3ed5b1<br>Mirko Myll..<br>This is the second commit"]) --> firstcommit(["commit 23b3ed5b1...<br>tree 1a098a06b<br>Mirko Myll...<br>This is the first commit"]) --> tree2(["tree 1a098a06b...<br>blob 09c78e6e.... file.txt"]) 

  secondcommit --> tree1(["tree 22b5208b...<br>blob 3b23ff0c file.txt"])
  secondblob["blob 3b23ff0c<br>This file is very interesting<br>More content"]
  firstblob["blob 09c78e6e...<br>This file is very interesting"]
  
  tree2 --> firstblob
  tree1 --> secondblob
```

---

### Commit tree

- Usually, we have a complete tree of commits (**commit tree**):

```mermaid
graph LR
  commit1(["commit 1"]) --> tree1(["tree 1"])
  commit2(["commit 2"]) --> tree2(["tree 2"])
  commit2 --> commit1
  commit3(["commit 3"]) --> tree3(["tree 3"])
  commit3 --> commit2
  commit4(["commit 4"]) --> tree4(["tree 4"])
  commit4 --> commit3
```

- Each commit represents the state of the repository at a given point of time.

---

- Each commit is allowed to have **multiple** parents:

```mermaid
graph LR
  commit2(["commit 2"]) --> commit1(["commit 1"])
  commit4(["commit 4"]) --> commit3(["commit 3"])
  commit4 --> commit2
```

- These parents appear when two (or more) *branches* are **merged**.
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

```mermaid
graph LR
  
  head["HEAD"]
  style head fill:#ffffff,stroke:#ffffff
  master["master"]
  style master fill:#ffffff,stroke:#ffffff
  
  head --> master --> secondcommit(["commit d3c6c635...<br>tree 22b5208b<br>parent 23b3ed5b1<br>Mirko Myll..<br>This is the second commit"]) --> firstcommit(["commit 23b3ed5b1...<br>tree 1a098a06b<br>Mirko Myll...<br>This is the first commit"])
  
  subgraph clusterworkingtree["Working tree"]
    clusterfile["file.txt<br><br>This file is very interesting<br>More content"]
  end
```

- Remember, many Git commands act on the current `HEAD`.

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

```mermaid
graph LR
  
  head["HEAD"]
  style head fill:#ffffff,stroke:#ffffff
  master["master"]
  style master fill:#ffffff,stroke:#ffffff
  
  second_commit["commit d3c6c635...<br>tree 22b5208b<br>parent 23b3ed5b1<br>Mirko Myll..<br>This is the second commit"]

  first_commit["commit 23b3ed5b1...<br>tree 1a098a06b<br>Mirko Myll...<br>This is the first commit"]
  
  second_commit --> first_commit
  
  head --> first_commit 
  master --> second_commit
  
  subgraph cluster_working_tree["Working tree"]
    cluster_file["file.txt<br><br>This file is very interesting"]
  end
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

- Let's investigate the newly created commit:

```shell
$ git cat-file -p a118ae8c
tree 5fcc4f83fedf5a94cd773704bdb1ab2cdcadc6fd
parent 23b3ed5b16095bb84b18d06734fdd614c8982841
author Mirko Myllykoski <mirko....> 1601286412 +0200
committer Mirko Myllykoski <mirko....> 1601286412 +0200

This is the third commit
```

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

---

<!-- .slide: style="font-size: 24px;" -->

 - Second, the commit tree now has **two** branches: 

```graphviz
digraph {
  rankdir=LR
  nodesep=0.2
  
  "HEAD" [fontsize=10 shape=plaintext]
  "master" [fontsize=10 shape=plaintext]
  
  third_commit [fontsize=10 label="commit a118ae8c...\nThis is the third commit"]
  second_commit [fontsize=10 label="commit d3c6c635...\nThis is the second commit"]
  first_commit [fontsize=10 label="commit 23b3ed5b1...\nThis is the first commit"]
  
  third_blob [fontsize=10 label="blob ea5f4b8e\nThis file is very interesting\nDifferent content" shape=box]
  second_blob [fontsize=10 label="blob 3b23ff0c\nThis file is very interesting\nMore content" shape=box]
  first_blob [fontsize=10 label="blob 09c78e6e...\nThis file is very interesting" shape=box]
  
  third_commit -> third_blob [style=dashed]
  second_commit -> second_blob [style=dashed]
  first_commit -> first_blob [style=dashed]
  
  third_commit -> first_commit
  second_commit -> first_commit
  
  "HEAD" -> third_commit 
  "master" -> second_commit
  
  subgraph cluster_working_tree {
    nodesep=0.2
    fontsize=10
    label="Working tree"
    subgraph cluster_file {
      fontsize=10
      label="file.txt"
        "This file is very interesting\nDifferent content
" [fontsize=10 shape=plain]
    }
  }
}
```

---

<!-- .slide: style="font-size: 24px;" -->

We can give the second branch a **name**:

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
  nodesep=0.2
  
  "HEAD" [fontsize=10 shape=plaintext]
  "master" [fontsize=10 shape=plaintext]
  "second_branch" [fontsize=10 shape=plaintext]
  
  third_commit [fontsize=10 label="commit a118ae8c...\nThis is the third commit"]
  second_commit [fontsize=10 label="commit d3c6c635...\nThis is the second commit"]
  first_commit [fontsize=10 label="commit 23b3ed5b1...\nThis is the first commit"]
  
  third_blob [fontsize=10 label="blob ea5f4b8e\nThis file is very interesting\nDifferent content" shape=box]
  second_blob [fontsize=10 label="blob 3b23ff0c\nThis file is very interesting\nMore content" shape=box]
  first_blob [fontsize=10 label="blob 09c78e6e...\nThis file is very interesting" shape=box]
  
  third_commit -> third_blob [style=dashed]
  second_commit -> second_blob [style=dashed]
  first_commit -> first_blob [style=dashed]
  
  third_commit -> first_commit
  second_commit -> first_commit
  
  "HEAD" -> third_commit
  "master" -> second_commit
  "second_branch" -> third_commit
  
  subgraph cluster_working_tree {
    fontsize=10
    label="Working tree"
    subgraph cluster_file {
      fontsize=10
      label="file.txt"
        "This file is very interesting\nDifferent content
" [fontsize=10 shape=plain]
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

<!-- .slide: style="font-size: 26px; text-align: left;" -->

Finally, the tree looks like follows:

```graphviz
digraph {
rankdir=LR
nodesep=0.03
    subgraph cluster_working_tree {
        label="Working tree"
        nodesep=0.1
        fontsize=9 width=0.03 height=0.02
        subgraph cluster_file {
           fontsize=9 width=0.03 height=0.02
           label="file.txt"
        "This file is very interesting\nMore content\nDifferent content" [fontsize=9 width=0.03 height=0.02 shape=plain]
    }
  }
  }
  ```

```graphviz
digraph {
  rankdir=LR
  nodesep=0.03
  
  "HEAD" [fontsize=8 width=0.03 height=0.02 shape=plaintext]
  "master" [fontsize=8 width=0.03 height=0.02 shape=plaintext]
  "second_branch" [fontsize=8 width=0.03 height=0.02 shape=plaintext]
  
  fourth_commit [fontsize=8 width=0.03 height=0.02 label="commit f0d72989...\nMerge branch 'second_branch'"]
  third_commit [fontsize=8 width=0.03 height=0.02 label="commit a118ae8c...\nThis is the third commit"]
  second_commit [fontsize=8 width=0.03 height=0.02 label="commit d3c6c635...\nThis is the second commit"]
  first_commit [fontsize=8 width=0.03 height=0.02 label="commit 23b3ed5b1...\nThis is the first commit"]
  
  fourth_blob [fontsize=8 width=0.03 height=0.02 label="blob e51364b9\nThis file is very interesting\nMore content\nDifferent content" shape=box]
  third_blob [fontsize=8 width=0.03 height=0.02 label="blob ea5f4b8e\nThis file is very interesting\nDifferent content" shape=box]
  second_blob [fontsize=8 width=0.03 height=0.02 label="blob 3b23ff0c\nThis file is very interesting\nMore content" shape=box]
  first_blob [fontsize=8 width=0.03 height=0.02 label="blob 09c78e6e...\nThis file is very interesting" shape=box]
  
  fourth_commit -> fourth_blob [fontsize=8 width=0.03 height=0.02 style=dashed]
  third_commit -> third_blob [fontsize=8 width=0.03 height=0.02 style=dashed]
  second_commit -> second_blob [fontsize=8 width=0.03 height=0.02 style=dashed]
  first_commit -> first_blob [fontsize=8 width=0.03 height=0.02 style=dashed]
  
  fourth_commit -> second_commit
  fourth_commit -> third_commit
  third_commit -> first_commit
  second_commit -> first_commit
  
  "HEAD" -> fourth_commit
  "master" -> fourth_commit
  "second_branch" -> third_commit
  
}
```

---

<!-- .slide: style="font-size: 24px; text-align: left;" -->

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
nodesep=0.03
    subgraph cluster_working_tree {
    label="Working tree"
    fontsize=8 width=0.03 height=0.02 
    subgraph cluster_file {
      label="file.txt"
      fontsize=8 width=0.03 height=0.02 
        "This file is very interesting" [fontsize=8 width=0.03 height=0.02 shape=plain]
    }
  }
  }
```

```graphviz
digraph {
  rankdir=LR
  nodesep=0.2
  
  "HEAD" [fontsize=8 width=0.03 height=0.02 shape=plaintext]
  "master" [fontsize=8 width=0.03 height=0.02 shape=plaintext]
  "second_branch" [fontsize=8 width=0.03 height=0.02 shape=plaintext]
  
  fourth_commit [fontsize=8 width=0.03 height=0.02 label="commit f0d72989...\nMerge branch 'second_branch'"]
  third_commit [fontsize=8 width=0.03 height=0.02 label="commit a118ae8c...\nThis is the third commit"]
  second_commit [fontsize=8 width=0.03 height=0.02 label="commit d3c6c635...\nThis is the second commit"]
  first_commit [fontsize=8 width=0.03 height=0.02 label="commit 23b3ed5b1...\nThis is the first commit"]
  
  fourth_blob [fontsize=8 width=0.03 height=0.02 label="blob e51364b9\nThis file is very interesting\nMore content\nDifferent content" shape=box]
  third_blob [fontsize=8 width=0.03 height=0.02 label="blob ea5f4b8e\nThis file is very interesting\nDifferent content" shape=box]
  second_blob [fontsize=8 width=0.03 height=0.02 label="blob 3b23ff0c\nThis file is very interesting\nMore content" shape=box]
  first_blob [fontsize=8 width=0.03 height=0.02 label="blob 09c78e6e...\nThis file is very interesting" shape=box]
  
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
  
}
```

---

The end.

An idea: Try to play with the different commands. See what happens to the `.git/` directory.

