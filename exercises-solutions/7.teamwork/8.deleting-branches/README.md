# 8. Deleting branches

1. Everyone should now create two more branches in the repo. In each case, switch to the branch, create a file in it, and push the branch

	You can do this on the GitHub page or on the command line, as you prefer. This is how you could do it on the command line: 

	```shell
	bbrydsoe@enterprise-a:~/mytestrepo$ git branch awesomefeature
	bbrydsoe@enterprise-a:~/mytestrepo$ git branch funstuff
	bbrydsoe@enterprise-a:~/mytestrepo$ git checkout awesomefeature
	Switched to branch 'awesomefeature'
	bbrydsoe@enterprise-a:~/mytestrepo$ touch awesome.txt
	bbrydsoe@enterprise-a:~/mytestrepo$ echo 'This branch will have an awesome feature' > awesome.txt 
bbrydsoe@enterprise-a:~/mytestrepo$ git add awesome.txt 
	bbrydsoe@enterprise-a:~/mytestrepo$ git commit -m "Committing the first file in my new awesome branch"
	[awesomefeature aa0f455] Committing the first file in my new awesome branch
	 1 file changed, 1 insertion(+)
	 create mode 100644 awesome.txt
	bbrydsoe@enterprise-a:~/mytestrepo$ git push origin -u awesomefeature 
	Enter passphrase for key '/home/bbrydsoe/.ssh/id_rsa': 
	Enumerating objects: 4, done.
	Counting objects: 100% (4/4), done.
	Delta compression using up to 4 threads
	Compressing objects: 100% (2/2), done.
	Writing objects: 100% (3/3), 344 bytes | 344.00 KiB/s, done.
	Total 3 (delta 1), reused 0 (delta 0)
	remote: Resolving deltas: 100% (1/1), completed with 1 local object.
	remote: 
	remote: Create a pull request for 'awesomefeature' on GitHub by visiting:
	remote:      https://github.com/bbrydsoe/mytestrepo/pull/new/awesomefeature
	remote: 
	To github.com:bbrydsoe/mytestrepo.git
	 * [new branch]      awesomefeature -> awesomefeature
	Branch 'awesomefeature' set up to track remote branch 'awesomefeature' from 'origin'.
	bbrydsoe@enterprise-a:~/mytestrepo$ git checkout funstuff 
	Switched to branch 'funstuff'
	bbrydsoe@enterprise-a:~/mytestrepo$ touch fun.txt
	bbrydsoe@enterprise-a:~/mytestrepo$ echo 'I will find some fun stuff to add' > fun.txt 
	bbrydsoe@enterprise-a:~/mytestrepo$ git add fun.txt 
	bbrydsoe@enterprise-a:~/mytestrepo$ git commit -m "File for fun stuff"
	[funstuff 70738ab] File for fun stuff
	 1 file changed, 1 insertion(+)
	 create mode 100644 fun.txt
	bbrydsoe@enterprise-a:~/mytestrepo$ git push origin -u funstuff 
	Enter passphrase for key '/home/bbrydsoe/.ssh/id_rsa': 
	Enumerating objects: 4, done.
	Counting objects: 100% (4/4), done.
	Delta compression using up to 4 threads
	Compressing objects: 100% (2/2), done.
	Writing objects: 100% (3/3), 311 bytes | 311.00 KiB/s, done.
	Total 3 (delta 1), reused 0 (delta 0)
	remote: Resolving deltas: 100% (1/1), completed with 1 local object.
	remote: 
	remote: Create a pull request for 'funstuff' on GitHub by visiting:
	remote:      https://github.com/bbrydsoe/mytestrepo/pull/new/funstuff
	remote: 
	To github.com:bbrydsoe/mytestrepo.git
	 * [new branch]      funstuff -> funstuff
	Branch 'funstuff' set up to track remote branch 'funstuff' from 'origin'.
	``` 

2. Check which branches exist, remotely and locally

	```shell
	bbrydsoe@enterprise-a:~/mytestrepo$ git branch -a
	  awesomefeature
	  birgittesbranch
	  fancyfeatures
	* funstuff
	  main
	  mybranch
	  mynewbranch
	  mytestbranch
	  yetanotherbranch
	  remotes/origin/HEAD -> origin/main
	  remotes/origin/awesomefeature
	  remotes/origin/birgittesbranch
	  remotes/origin/extrabranch
	  remotes/origin/fancyfeatures
	  remotes/origin/funstuff
	  remotes/origin/main
	  remotes/origin/mybranch
	  remotes/origin/mynewbranch
	  remotes/origin/mytestbranch
	  remotes/origin/spocksbranch
	  remotes/origin/yetanotherbranch
	```

	This repository has a lot of branches! Probably good that I am going to delte some now! 

3. Try and delete a remote branch with `git push origin --delete myownbranch

	I will delete "remotes/origin/awesomefeature" 

	```shell
	bbrydsoe@enterprise-a:~/mytestrepo$ git push origin --delete awesomefeature
	Enter passphrase for key '/home/bbrydsoe/.ssh/id_rsa': 
	To github.com:bbrydsoe/mytestrepo.git
	 - [deleted]         awesomefeature
	```

	Let us see what happened: 

	```shell
	bbrydsoe@enterprise-a:~/mytestrepo$ git branch -a
	  awesomefeature
	  birgittesbranch
	  fancyfeatures
	* funstuff
	  main
	  mybranch
	  mynewbranch
	  mytestbranch
	  yetanotherbranch
	  remotes/origin/HEAD -> origin/main
	  remotes/origin/birgittesbranch
	  remotes/origin/extrabranch
	  remotes/origin/fancyfeatures
	  remotes/origin/funstuff
	  remotes/origin/main
	  remotes/origin/mybranch
	  remotes/origin/mynewbranch
	  remotes/origin/mytestbranch
	  remotes/origin/spocksbranch
	  remotes/origin/yetanotherbranch
	```

	As you can see, there is still a local branch called "awesomefeature", but the remote branch with that name has been deleted. You can get it back again with `git push origin -u awesomefeature` if you want to. 

4. Try delete a local branch with `git branch -D <alsomyownbranch`>

	```shell
	bbrydsoe@enterprise-a:~/mytestrepo$ git branch -D funstuff 
	error: Cannot delete branch 'funstuff' checked out at '/home/bbrydsoe/mytestrepo'
	bbrydsoe@enterprise-a:~/mytestrepo$ git checkout main
	Switched to branch 'main'
	Your branch is up-to-date with 'origin/main'.
	bbrydsoe@enterprise-a:~/mytestrepo$ git branch -D funstuff 
	Deleted branch funstuff (was 70738ab).
	bbrydsoe@enterprise-a:~/mytestrepo$ git branch -a
	  awesomefeature
	  birgittesbranch
	  fancyfeatures
	* main
	  mybranch
	  mynewbranch
	  mytestbranch
	  yetanotherbranch
	  remotes/origin/HEAD -> origin/main
	  remotes/origin/birgittesbranch
	  remotes/origin/extrabranch
	  remotes/origin/fancyfeatures
	  remotes/origin/funstuff
	  remotes/origin/main
	  remotes/origin/mybranch
	  remotes/origin/mynewbranch
	  remotes/origin/mytestbranch
	  remotes/origin/spocksbranch
	  remotes/origin/yetanotherbranch
	```

	As you can see, you cannot delete the branch you are on! 

5. Do a `git status`, `git log` and `git branch` to see what has happened

	```shell
	bbrydsoe@enterprise-a:~/mytestrepo$ git status
	On branch main
	Your branch is up-to-date with 'origin/main'.
	
	nothing to commit, working tree clean
	```

	```shell
	bbrydsoe@enterprise-a:~/mytestrepo$ git log
	commit 27d1559cdfe54dab8445fcc285b21fcc2f31cf72 (HEAD -> main, origin/main, origin/HEAD)
	Merge: 032fc22 1c3818b
	Author: Birgitte Brydsö <bbrydsoe@cs.umu.se>
	Date:   Thu Nov 17 12:30:01 2022 +0100
	...
	```

	As you can see, nothing commmitted - you only did things "locally" and need to push it for it to take effect remotely. 

Your local branches: 

	```shell
	bbrydsoe@enterprise-a:~/mytestrepo$ git branch
	  awesomefeature
	  birgittesbranch
	  fancyfeatures
	* main
	  mybranch
	  mynewbranch
	  mytestbranch
	  yetanotherbranch
	```

6. The branch you deleted locally is still on the repo. Get another copy of it (`git pull` and `git fetch`, possibly with suitable flags will get it back for you)

	```shell
	bbrydsoe@enterprise-a:~/mytestrepo$ git pull
	Enter passphrase for key '/home/bbrydsoe/.ssh/id_rsa': 
	Already up-to-date.
	```

	```shell
	bbrydsoe@enterprise-a:~/mytestrepo$ git fetch origin funstuff:funstuff
	Enter passphrase for key '/home/bbrydsoe/.ssh/id_rsa': 
	From github.com:bbrydsoe/mytestrepo
	 * [new branch]      funstuff   -> funstuff
	```

	Now let us see what local branches we have: 

	```shell
	bbrydsoe@enterprise-a:~/mytestrepo$ git branch
	  awesomefeature
	  birgittesbranch
	  fancyfeatures
	  funstuff
	* main
	  mybranch
	  mynewbranch
	  mytestbranch
          yetanotherbranch
	```

Success! We got the branch back! 

