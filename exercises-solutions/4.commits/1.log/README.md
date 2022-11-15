# Investigating the commit history - with solutions

The goal of this exercise is to learn to use the `git log` command. Enter the
`repository/` directory and perform the following steps:

 1. Investigate the history. How many commit does the `main` branch contain?
 
 2. Can you make the output of the command cleaner?
 
 3. Are there any other branches? How many? What are they called?
 
 4. Try to filter the output so that only commits that contain the word
    "abandon" in the commit message are shown.

 5. Does the reference log contain anything interesting? Can you see where the 
    `HEAD` was 6 steps ago?

Hints:

 - oneline
 - graph
 - reflog

**Solution**

 1. List all commits on the current branch with `git log`. There are 5 commits on the `master`/`main` branch.

 2. `git log --oneline`

 3. `git log --oneline --all --graph` lists all branches. There are two other branches besides `master`/`main`: `new_direction` and `experiment`.

 4. `git log --grep="abandon"` lists all commits that have the word "abandon" in the commit message.

```shell
$ git log --grep="abandon"
commit 8b0bd060fbb2566f3f4b28dabd2034e0a44beb66
Author: John Doe <john.doe@email.com>
Date:   Sun Nov 13 21:15:03 2022 +0100

    I am not going to abandon this path yet
```

 5. You may use `git reflog` and counts 6 steps back from the current `HEAD`, `30734ce`.

 A more elegant solution is:

```shell
$ git rev-parse --short HEAD@{6}
f0675dc
```

 Thus, the `HEAD` was pointing to commit `f0675dc` 6 steps back.

