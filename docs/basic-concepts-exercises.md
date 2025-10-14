# Exercises - Basic Concepts

1. Create a repository, add (stage) and commit a file

   ```bash
   mkdir repository 
   cd repository 
   git init 
   nano file.txt 
   git add file.txt 
   git commit -m "This is quite interesting" 
   ```
2. Take a look at the stuff under the .git directory 

   ```bash
   cd repository
   tree .git 
   git cat-file -p <hash> 
   ```

   where <hash> is the various hash'es you can see with 

   ```bash
   tree .git
   ```
 
   Remember that the two-letter name of the subdirectory under objects-dir is included in the hash 

3. Make some changes. 

Change one or more files. Add and commit. Make some changes. Add and commit. 

Look at what happens in the .git tree 

4. Go to earlier commits and make a new branch 

Try go back to an earlier commit with “git checkout <hash>” 

Make come changes to a file there, or try adding a new file (and add+commit) 

Create a new branch from that commit: “git checkout -b second_branch” 

Find the hash of the commit the HEAD points to now  

```bash 
cat .git/HEAD    
cat <path you got above> 
git cat-file -p <hash you just got from above command> 
```

5. Go back on primary branch and merge the branches

Go back to the primary branch (main or master) with “git checkout main” or “git checkout master” 

Merge the new branch you created to master with “git merge --no-ff second_branch” (or whatever you called the new branch) 

Fix any conflict by going into the conflicting file(s) and removing the stuff you don’t want and also the git markers set there 

Add the fixed file and do “git merge --continue"  

Now look at what the HEAD is pointing to 

6. Check out the commit tree   

You can also just try jump around in the commit tree with “git checkout <hash>” and see how your working tree looks in various places (see that files are there or not, and with different content). 

You get the list of hash’s and commit messages with “git log” 

