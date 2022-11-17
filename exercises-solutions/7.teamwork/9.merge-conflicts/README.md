# 9. Merge conflicts

In this exercise everyone in the team will be working in the same branch, for instance the main branch (yes, it is not normally recommended to work in the main/master branch, but this could just as well be done in another branch, so we are just using main here). 

Merge conflicts generally happen when two (or more) teammembers edit the same file and the same line, or when one edits a file and another deletes it.

1. Create a new repository on GitHub. Add your team members as in the previous exercises. Everyone clones the repository (from the command line).

	Follow the instructions from the first exercise for how to create a repository and from the fourth exercise for how to add members. 

2. Create a couple files. Add, commit, and push.
   - If more than one creates files, remember to either pull your teammates work first, or do a `git pull --rebase` before pushing.

	First everyone should clone the repository: click the green "CODE" button over the file area for the repository on GitHub, then pick SSH and copy the link. Then clone with `git clone <repo-link>`. 

	Change to the directory. 

	Then do something similar to this: 

	```shell 
	bbrydsoe@enterprise-a:~/mytestrepo$ touch morefiles.txt
	bbrydsoe@enterprise-a:~/mytestrepo$ echo 'Just some text' > morefiles.txt 
	bbrydsoe@enterprise-a:~/mytestrepo$ touch yetmorefiles.txt
	bbrydsoe@enterprise-a:~/mytestrepo$ echo 'Just some text to the file' > yetmorefiles.txt 
	bbrydsoe@enterprise-a:~/mytestrepo$ git add .
	bbrydsoe@enterprise-a:~/mytestrepo$ git commit -m "adding some files"
	[main 944cd2c] adding some files
	 2 files changed, 2 insertions(+)
	 create mode 100644 morefiles.txt
	 create mode 100644 yetmorefiles.txt
	bbrydsoe@enterprise-a:~/mytestrepo$ git push
	Enter passphrase for key '/home/bbrydsoe/.ssh/id_rsa': 
	Enumerating objects: 4, done.
	Counting objects: 100% (4/4), done.
	Delta compression using up to 4 threads
	Compressing objects: 100% (2/2), done.
	Writing objects: 100% (3/3), 342 bytes | 342.00 KiB/s, done.
	Total 3 (delta 1), reused 0 (delta 0)
	remote: Resolving deltas: 100% (1/1), completed with 1 local object.
	To github.com:bbrydsoe/mytestrepo.git
	   27d1559..944cd2c  main -> main

4. After doing this, everyone should again do a `git pull`

	Everyone do the above under part 3. Then do `git pull`

5. Now one or more make changes to the same file, in the same line. Add, commit, push.

	Pick one of the files that you all agree to make changes to. 

	In my example here I make changes to one of the files I just created, namely the file "morefiles.txt". It will also be changed by another, and in this case before I push my changes: 


	```shell
	bbrydsoe@enterprise-a:~/mytestrepo$ vi morefiles.txt 
	bbrydsoe@enterprise-a:~/mytestrepo$ git add morefiles.txt 
	bbrydsoe@enterprise-a:~/mytestrepo$ git commit -m "Let us create a conflict"
	[main 7e14cc9] Let us create a conflict
	 1 file changed, 2 insertions(+)
	bbrydsoe@enterprise-a:~/mytestrepo$ git push
	Enter passphrase for key '/home/bbrydsoe/.ssh/id_rsa': 
	To github.com:bbrydsoe/mytestrepo.git
	 ! [rejected]        main -> main (fetch first)
	error: failed to push some refs to 'git@github.com:bbrydsoe/mytestrepo.git'
	hint: Updates were rejected because the remote contains work that you do
	hint: not have locally. This is usually caused by another repository pushing
	hint: to the same ref. You may want to first integrate the remote changes
	hint: (e.g., 'git pull ...') before pushing again.
	hint: See the 'Note about fast-forwards' in 'git push --help' for details.
	```

6. Did you get a conflict? Use `git status`, `git branch`, and `git log` to see what has happened. Try to resolve the conflict.

	As you can see, there is a conflict. This is what `git status` tells me: 

	bbrydsoe@enterprise-a:~/mytestrepo$ git status
	On branch main
	Your branch is ahead of 'origin/main' by 1 commit.
	  (use "git push" to publish your local commits)

	nothing to commit, working tree clean
	```

	Not hugely helpful! 

	Let us try and do a `git pull` so we can see those other changes: 

	```shell
	bbrydsoe@enterprise-a:~/mytestrepo$ git pull
	Enter passphrase for key '/home/bbrydsoe/.ssh/id_rsa': 
	remote: Enumerating objects: 3, done.
	remote: Counting objects: 100% (3/3), done.
	remote: Compressing objects: 100% (3/3), done.
	remote: Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
	Unpacking objects: 100% (3/3), 1.10 KiB | 563.00 KiB/s, done.
	From github.com:bbrydsoe/mytestrepo
	   944cd2c..a17248b  main       -> origin/main
	Auto-merging morefiles.txt
	CONFLICT (content): Merge conflict in morefiles.txt
	Automatic merge failed; fix conflicts and then commit the result.
	```

	Now let us see if `git status` gives more information: 

	```shell
	bbrydsoe@enterprise-a:~/mytestrepo$ git status
	On branch main
	Your branch and 'origin/main' have diverged,
	and have 1 and 1 different commits each, respectively.
	  (use "git pull" to merge the remote branch into yours)
	
	You have unmerged paths.
	  (fix conflicts and run "git commit")
	  (use "git merge --abort" to abort the merge)
	
	Unmerged paths:
	  (use "git add <file>..." to mark resolution)
		both modified:   morefiles.txt

	no changes added to commit (use "git add" and/or "git commit -a")
	```

	We can try to auto-merge, but let us first open the file in question and see. Most likely we will have to fix it manually (often the only option in cases like this where the changes are in the same lines of the file). This is how it looks: 

	```shell
	Just some text
	<<<<<<< HEAD
	Maybe I should add text here as well.
	Then when I have added text I will add more text.
	=======
	I am now writing more text.
	And also yet more text
	>>>>>>> a17248b99d90ebd0fb654c70eedaac99bfecbe73

	You can see the "conflict dividers". What I added to the file is above the ======= and what is below is what was added elsewhere. The only way to resolve it is manually. You (and your collaborators, or maybe the owner of the repository) will have to make a choice. After correcting the above file as you want it to be (including removing the "conflict dividers"), redo the add, commit, and push: 

	```shell
	bbrydsoe@enterprise-a:~/mytestrepo$ git add morefiles.txt 
	bbrydsoe@enterprise-a:~/mytestrepo$ git commit -m "Fixing the conflict"
	[main 4883b99] Fixing the conflict
	bbrydsoe@enterprise-a:~/mytestrepo$ git push
	Enter passphrase for key '/home/bbrydsoe/.ssh/id_rsa': 
	Enumerating objects: 10, done.
	Counting objects: 100% (10/10), done.
	Delta compression using up to 4 threads
	Compressing objects: 100% (6/6), done.
	Writing objects: 100% (6/6), 659 bytes | 659.00 KiB/s, done.
	Total 6 (delta 3), reused 0 (delta 0)
	remote: Resolving deltas: 100% (3/3), completed with 1 local object.
	To github.com:bbrydsoe/mytestrepo.git
	   a17248b..4883b99  main -> main
	```

7. Now again all will work on one file. One or more edit it and one deletes it (`git rm file`). What happens when you push your work? You should get a conflict. Try and resolve the conflict. Should the file be kept or deleted?

	Let us say, as an example, that I want to delete the file "yetmorefiles.txt": 

	```shell
	bbrydsoe@enterprise-a:~/mytestrepo$ git rm yetmorefiles.txt 
	rm 'yetmorefiles.txt'
	bbrydsoe@enterprise-a:~/mytestrepo$ git commit -m "Deleting the file yetmorefiles.txt as I don't need it"
	[main fbfd12b] Deleting the file yetmorefiles.txt as I don't need it
	 1 file changed, 1 deletion(-)
	 delete mode 100644 yetmorefiles.txt
	bbrydsoe@enterprise-a:~/mytestrepo$ git push
	Enter passphrase for key '/home/bbrydsoe/.ssh/id_rsa': 
	To github.com:bbrydsoe/mytestrepo.git
	 ! [rejected]        main -> main (fetch first)
	error: failed to push some refs to 'git@github.com:bbrydsoe/mytestrepo.git'
	hint: Updates were rejected because the remote contains work that you do
	hint: not have locally. This is usually caused by another repository pushing
	hint: to the same ref. You may want to first integrate the remote changes
	hint: (e.g., 'git pull ...') before pushing again.
	hint: See the 'Note about fast-forwards' in 'git push --help' for details.
	```

	Oh no, someone has edited the file I was trying to delete! What now? 

	The only way to resolve this is to agree on if the file should be kept or deleted (or by the owner of the repository making a decision). Decide. 

	What if I decide to let the file stay? How do I recover my attempt at deleting?

	If nothing else works, you can throw out your changes and do a hard reset and then a new pull: 

	```shell
	git reset --hard HEAD~1
	git pull
	```

Other ways to save your work includes `git stash` which you later `git apply`, but a remove of a file will in any case usually need discussion with the person who had edited the file you wanted to delete. 


