# 7. Teamwork and branches  

Now you will be creating a new branch in the repo your group is sharing, but you will create in from the GitHub page. 

1. Everyone in the group create a new branch in the repo - this time you could try doing it from the GitHub page. 

	You can do it two ways; either by pressing the "branches" (marked by me with a red line) and then picking the green "New branch" button on the right side, or by pressing "main" (marked by me with a blue line) and writing your new branch's name in the field and then clicking "Create branch: <branch-name> from main"

![](figures/github-main.png)

	Option 1: Creating from clicking "branches": 

![](figures/create-new-branch.png) 
![](figures/creating.png)
	
	Note that you could create a branch from one of the other branches instead of main, if you want to. 

	Option 2: Creating from clicking "main": 

![](figures/othercreate.png)

2. Check which remote branches exist with `git branch -r`

	This is done on the command line. Note that you need to do a pull before you will see the newly created branches: 
	
	Before a pull:

	```shell
	bbrydsoe@enterprise-a:~/mytestrepo$ git branch -r
	  origin/HEAD -> origin/main
	  origin/birgittesbranch
	  origin/extrabranch
	  origin/fancyfeatures
	  origin/main
	  origin/mynewbranch
	  origin/mytestbranch
	  origin/spocksbranch
	```

	After a pull: 

	```shell
	bbrydsoe@enterprise-a:~/mytestrepo$ git pull
	Enter passphrase for key '/home/bbrydsoe/.ssh/id_rsa': 
	From github.com:bbrydsoe/mytestrepo
	 * [new branch]      mybranch         -> origin/mybranch
	 * [new branch]      yetanotherbranch -> origin/yetanotherbranch
	Already up-to-date.
	```

	```shell
	bbrydsoe@enterprise-a:~/mytestrepo$ git branch -r
	  origin/HEAD -> origin/main
	  origin/birgittesbranch
	  origin/extrabranch
	  origin/fancyfeatures
	  origin/main
	  origin/mybranch
	  origin/mynewbranch
	  origin/mytestbranch
	  origin/spocksbranch
	  origin/yetanotherbranch
	```

3. Check which local branches you have with `git branch`

	```shell
	bbrydsoe@enterprise-a:~/mytestrepo$ git branch
	  birgittesbranch
	* fancyfeatures
	  main
	  mynewbranch
	  mytestbranch
	```

	So no changes here, as the branches were created remotely.  

4. Use `git status` to see which branch you are on. 

	```shell
	bbrydsoe@enterprise-a:~/mytestrepo$ git status
	On branch fancyfeatures
	Your branch is up-to-date with 'origin/fancyfeatures'.

	nothing to commit, working tree clean
	```

	Again, no changes. 

5. Check with `git branch -a` to see all local and remote branches

	```shell
	bbrydsoe@enterprise-a:~/mytestrepo$ git branch -a
	  birgittesbranch
	* fancyfeatures
	  main
	  mynewbranch
	  mytestbranch
	  remotes/origin/HEAD -> origin/main
	  remotes/origin/birgittesbranch
	  remotes/origin/extrabranch
	  remotes/origin/fancyfeatures
	  remotes/origin/main
	  remotes/origin/mybranch
	  remotes/origin/mynewbranch
	  remotes/origin/mytestbranch
	  remotes/origin/spocksbranch
	  remotes/origin/yetanotherbranch
	```

6. Do a `git pull` from the command line to get a list of all branches. Switch to the branch you created on GitHub with `git checkout --track origin/mynewbranch`. Again do `git branch` to see which branch you are on.

	We did a `git pull` a bit further up in the exercise, so nothing new: 

	```shell
	bbrydsoe@enterprise-a:~/mytestrepo$ git pull
	Enter passphrase for key '/home/bbrydsoe/.ssh/id_rsa': 
	Already up-to-date.
	```

I created a branch called "mybranch" on the GitHub page. Switching to that: 

	```shell
	bbrydsoe@enterprise-a:~/mytestrepo$ git checkout --track origin/mybranch
	Branch 'mybranch' set up to track remote branch 'mybranch' from 'origin'.
	Switched to a new branch 'mybranch'
	bbrydsoe@enterprise-a:~/mytestrepo$ 
	```

Using `git branch` to see the (local) branches and what branch I am on: 

	```shell
	bbrydsoe@enterprise-a:~/mytestrepo$ git branch
	  birgittesbranch
	  fancyfeatures
	  main
	* mybranch
	  mynewbranch
	  mytestbranch
	```

7. Create a new file and put some content to it. Add and commit it. Check for changes (`git status`, `git log`). Push the changes.

	```shell
	bbrydsoe@enterprise-a:~/mytestrepo$ touch candy.txt
	bbrydsoe@enterprise-a:~/mytestrepo$ echo 'I like licorice' > candy.txt 
	bbrydsoe@enterprise-a:~/mytestrepo$ git add candy.txt 
	bbrydsoe@enterprise-a:~/mytestrepo$ git commit -m "Adding a file with some info on what candy I like"
	[mybranch 19b6733] Adding a file with some info on what candy I like
	 1 file changed, 1 insertion(+)
	 create mode 100644 candy.txt
	```

	```shell
	bbrydsoe@enterprise-a:~/mytestrepo$ git status
	On branch mybranch
	Your branch is ahead of 'origin/mybranch' by 1 commit.
	  (use "git push" to publish your local commits)

	nothing to commit, working tree clean
	```

	The top of the log: 

	```shell
	commit 19b67339983385d460fd28ce4bc25f3978f69d53 (HEAD -> mybranch)
	Author: Birgitte Brydsö <bbrydsoe@cs.umu.se>
	Date:   Thu Nov 17 12:12:15 2022 +0100

	    Adding a file with some info on what candy I like
	```

	Pushing the changes: 

	```shell
	bbrydsoe@enterprise-a:~/mytestrepo$ git push
	Enter passphrase for key '/home/bbrydsoe/.ssh/id_rsa': 
	Enumerating objects: 4, done.
	Counting objects: 100% (4/4), done.
	Delta compression using up to 4 threads
	Compressing objects: 100% (2/2), done.
	Writing objects: 100% (3/3), 319 bytes | 319.00 KiB/s, done.
	Total 3 (delta 1), reused 0 (delta 0)
	remote: Resolving deltas: 100% (1/1), completed with 1 local object.
	To github.com:bbrydsoe/mytestrepo.git
	   fa76703..19b6733  mybranch -> mybranch
	```

	```shell
	bbrydsoe@enterprise-a:~/mytestrepo$ git status
	On branch mybranch
	Your branch is up-to-date with 'origin/mybranch'.

	nothing to commit, working tree clean
	```

8. Try and merge the branches from the command line. Remember to first pull any changes from your other group members. Also remember to switch to the branch you want to merge it to (main in this case).

	```shell
	bbrydsoe@enterprise-a:~/mytestrepo$ git pull
	Enter passphrase for key '/home/bbrydsoe/.ssh/id_rsa': 
	Already up-to-date.
	bbrydsoe@enterprise-a:~/mytestrepo$ git checkout main
	Switched to branch 'main'
	Your branch is behind 'origin/main' by 2 commits, and can be fast-forwarded.
	  (use "git pull" to update your local branch)
	bbrydsoe@enterprise-a:~/mytestrepo$ git pull
	Enter passphrase for key '/home/bbrydsoe/.ssh/id_rsa': 
	Updating 6be6d4a..fa76703
	Fast-forward
	 fancyfile.txt | 1 +
	 1 file changed, 1 insertion(+)
	 create mode 100644 fancyfile.txt
	bbrydsoe@enterprise-a:~/mytestrepo$ git merge mybranch
	Updating fa76703..19b6733
	Fast-forward
	 candy.txt | 1 +
	 1 file changed, 1 insertion(+)
	 create mode 100644 candy.txt
	```

	As you can see, there was a file on the main/master branch that I did not have in my branch "mybranch" because it was created after I made my branch. There were no problems, though, and git could easily remedy it. 

	Note that you will need to do a `git push` to make the "pull request" rfom the command line. 

	Another example: 

	```shell
	bbrydsoe@enterprise-a:~/mytestrepo$ git checkout yetanotherbranch
	Branch 'yetanotherbranch' set up to track remote branch 'yetanotherbranch' from 'origin'.
	Switched to a new branch 'yetanotherbranch'
	bbrydsoe@enterprise-a:~/mytestrepo$ touch mytestfile.txt
	bbrydsoe@enterprise-a:~/mytestrepo$ echo 'Just a fun test file' > mytestfile.txt 
	bbrydsoe@enterprise-a:~/mytestrepo$ git add mytestfile.txt 
	bbrydsoe@enterprise-a:~/mytestrepo$ git commit -m "Created a file with some text"
	[yetanotherbranch 1c3818b] Created a file with some text
	 1 file changed, 1 insertion(+)
	 create mode 100644 mytestfile.txt
	bbrydsoe@enterprise-a:~/mytestrepo$ git push
	Enter passphrase for key '/home/bbrydsoe/.ssh/id_rsa': 
	Enumerating objects: 4, done.
	Counting objects: 100% (4/4), done.
	Delta compression using up to 4 threads
	Compressing objects: 100% (2/2), done.
	Writing objects: 100% (3/3), 311 bytes | 311.00 KiB/s, done.
	Total 3 (delta 1), reused 0 (delta 0)
	remote: Resolving deltas: 100% (1/1), completed with 1 local object.
	To github.com:bbrydsoe/mytestrepo.git
	   fa76703..1c3818b  yetanotherbranch -> yetanotherbranch
	bbrydsoe@enterprise-a:~/mytestrepo$ git checkout main
	Switched to branch 'main'
	Your branch is up-to-date with 'origin/main'.
	bbrydsoe@enterprise-a:~/mytestrepo$ git merge yetanotherbranch
	Merge made by the 'recursive' strategy.
	 mytestfile.txt | 1 +
	 1 file changed, 1 insertion(+)
	 create mode 100644 mytestfile.txt
	bbrydsoe@enterprise-a:~/mytestrepo$ git pull
	Enter passphrase for key '/home/bbrydsoe/.ssh/id_rsa': 
	Already up-to-date.
	bbrydsoe@enterprise-a:~/mytestrepo$ git push
	Enter passphrase for key '/home/bbrydsoe/.ssh/id_rsa': 
	Enumerating objects: 4, done.
	Counting objects: 100% (4/4), done.
	Delta compression using up to 4 threads
	Compressing objects: 100% (2/2), done.
	Writing objects: 100% (2/2), 322 bytes | 322.00 KiB/s, done.
	Total 2 (delta 1), reused 0 (delta 0)
	remote: Resolving deltas: 100% (1/1), completed with 1 local object.
	To github.com:bbrydsoe/mytestrepo.git
	   032fc22..27d1559  main -> main
	```

9. Were you succesful? Why or why not? Is there are difference between what happens when the owner of the branch tries this and when everyone else does?

	There will be a difference between the owner of the repository doing this (permitted) and anyone else (without admin rights) doing it (not permitted). If you have given your collaborators admin rights they will likely be allowed to do the merge. 

10. After doing this, everyone should again do a `git pull` (on the command line)

	It should look similar to this: 

	```shell
	bbrydsoe@enterprise-a:~/mytestrepo$ git pull
	Enter passphrase for key '/home/bbrydsoe/.ssh/id_rsa': 
	remote: Enumerating objects: 1, done.
	remote: Counting objects: 100% (1/1), done.
	remote: Total 1 (delta 0), reused 0 (delta 0), pack-reused 0
	Unpacking objects: 100% (1/1), 656 bytes | 656.00 KiB/s, done.
	From github.com:bbrydsoe/mytestrepo
	   fa76703..032fc22  main       -> origin/main
	Updating 19b6733..032fc22
	Fast-forward
	```

11. Use `git status`, `git branch`, and `git log` to see what has happened. If you want a "prettier" and sometimes easier to read view, use `git log --graph --oneline --decorate --all`

	```shell
	bbrydsoe@enterprise-a:~/mytestrepo$ git status
	On branch main
	Your branch is up-to-date with 'origin/main'.

	nothing to commit, working tree clean
	```

	```shell
	bbrydsoe@enterprise-a:~/mytestrepo$ git branch
	  birgittesbranch
	  fancyfeatures
	* main
	  mybranch
	  mynewbranch
	  mytestbranch
	  yetanotherbranch
	```

The top of the log, after I merged the branch "yetanotherbranch": 

	```shell
	*   27d1559 (HEAD -> main, origin/main, origin/HEAD) Merge branch 'yetanotherbranch' into main
	|\  
	| * 1c3818b (origin/yetanotherbranch, yetanotherbranch) Created a file with some text
	* |   032fc22 Merge pull request #5 from bbrydsoe/mybranch
	|\ \  
	| |/  
	|/|   
	| * 19b6733 (origin/mybranch, mybranch) Adding a file with some info on what candy I like
	|/  
	```

