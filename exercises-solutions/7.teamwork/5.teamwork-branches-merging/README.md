# 5. Teamwork, branches and merging

1. Each person creates a branch in the repo you created in the previous exercise. You can use `git branch yourbranchname` where you put any name you want for the new branch.

	Example where I call my new branch (in mytestrepo) "fancyfeatures":

	```shell
	bbrydsoe@enterprise-a:~/mytestrepo$ git branch fancyfeatures
	bbrydsoe@enterprise-a:~/mytestrepo$
	```

2. Switch to the new branch with `git checkout yourbranchname`

	Example for above branch:

	```shell
	bbrydsoe@enterprise-a:~/mytestrepo$ git checkout fancyfeatures
	Switched to branch 'fancyfeatures'
	bbrydsoe@enterprise-a:~/mytestrepo$
	```

3. Create a uniquely named file. Put anything you want in it.

	Example for above branch:

	```shell
	bbrydsoe@enterprise-a:~/mytestrepo$ touch fancyfile.txt
	bbrydsoe@enterprise-a:~/mytestrepo$ echo 'Just some text' > fancyfile.txt
	```

4. Do `git log` and `git status` to see any changes.

	Example for above branch:

	```shell
	bbrydsoe@enterprise-a:~/mytestrepo$ git status
	On branch fancyfeatures
	Untracked files:
	  (use "git add <file>..." to include in what will be committed)
		fancyfile.txt

	nothing added to commit but untracked files present (use "git add" to track)
	```

	The command `git log` will not show anything interesting yet, as we have not done a commit, but you can use it to see how it will change when you stage and commit in the next part.

5. Stage and commit the file. Check again with `git log` and `git status`

	Example for above branch:

	```shell
	brydsoe@enterprise-a:~/mytestrepo$ git add fancyfile.txt
	bbrydsoe@enterprise-a:~/mytestrepo$ git commit -m "This new file contains fancy text"
	[fancyfeatures 8b63075] This new file contains fancy text
	 1 file changed, 1 insertion(+)
	 create mode 100644 fancyfile.txt
	```

	```shell
	bbrydsoe@enterprise-a:~/mytestrepo$ git status
	On branch fancyfeatures
	nothing to commit, working tree clean
	```

	```shell
	commit 8b63075efcf6cfa91b40347f7f84cdeaa5f72c0e (HEAD -> fancyfeatures)
	Author: Birgitte Brydsö <bbrydsoe@cs.umu.se>
	Date:   Thu Nov 17 09:45:18 2022 +0100

	    This new file contains fancy text

	commit 6be6d4a9f3b230f7bb1fb00e5dac4c9e61926633 (origin/main, origin/HEAD, main)
	Author: Birgitte Brydsö <bbrydsoe@cs.umu.se>
	Date:   Wed Nov 16 21:39:53 2022 +0100

	    Adding a file to see git complain
	```

	The top commit is the new one. The next one is a previous one that was done on the main/master branch.

6. Push your changes with `git push origin -u yourbranchname` (or with `git push -u origin HEAD` for a fast way when using the same name)

	Example for above branch:

	```shell
	bbrydsoe@enterprise-a:~/mytestrepo$ git push origin -u fancyfeatures
	Enter passphrase for key '/home/bbrydsoe/.ssh/id_rsa':
	Enumerating objects: 4, done.
	Counting objects: 100% (4/4), done.
	Delta compression using up to 4 threads
	Compressing objects: 100% (2/2), done.
	Writing objects: 100% (3/3), 311 bytes | 311.00 KiB/s, done.
	Total 3 (delta 1), reused 0 (delta 0)
	remote: Resolving deltas: 100% (1/1), completed with 1 local object.
	remote:
	remote: Create a pull request for 'fancyfeatures' on GitHub by visiting:
	remote:      https://github.com/bbrydsoe/mytestrepo/pull/new/fancyfeatures
	remote:
	To github.com:bbrydsoe/mytestrepo.git
	 * [new branch]      fancyfeatures -> fancyfeatures
	Branch 'fancyfeatures' set up to track remote branch 'fancyfeatures' from 'origin'.
	```

7. When everyone has done this, all do a `git pull`

	Example, continuing with same as above:

	```shell
	bbrydsoe@enterprise-a:~/mytestrepo$ git pull
	Enter passphrase for key '/home/bbrydsoe/.ssh/id_rsa':
	remote: Enumerating objects: 3, done.
	remote: Counting objects: 100% (3/3), done.
	remote: Compressing objects: 100% (2/2), done.
	remote: Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
	Unpacking objects: 100% (3/3), 975 bytes | 975.00 KiB/s, done.
	From github.com:bbrydsoe/mytestrepo
	 * [new branch]      extrabranch -> origin/extrabranch
	Already up-to-date.
	```

	As you can see, someone else has made another branch, which I am informed about when I do a `git pull`.

8. Use `git status`, `git branch`, and `git log` to see what has happened.

	Example:

	```shell
	bbrydsoe@enterprise-a:~/mytestrepo$ git status
	On branch fancyfeatures
	Your branch is up-to-date with 'origin/fancyfeatures'.

	nothing to commit, working tree clean
	```

	```shell
	bbrydsoe@enterprise-a:~/mytestrepo$ git log
	commit 8b63075efcf6cfa91b40347f7f84cdeaa5f72c0e (HEAD -> fancyfeatures, origin/fancyfeatures)
	Author: Birgitte Brydsö <bbrydsoe@cs.umu.se>
	Date:   Thu Nov 17 09:45:18 2022 +0100

	    This new file contains fancy text

	commit 6be6d4a9f3b230f7bb1fb00e5dac4c9e61926633 (origin/main, origin/HEAD, main)
	...
	```

	Comparing with the previous `git log` you can see that fancyfeatures branch is now on origin.
