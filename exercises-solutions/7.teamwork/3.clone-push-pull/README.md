# 3. Clone, push, pull

We now have SSH keys set up. Time to test using them from your own machine! 

1. Clone the repository, using the SSH address: 

	- Click the CODE on your GitHub repository, above the file browser area, and then pick SSH. 
	- Clone it on your own computer. You will be asked for the SSH key passphrase
	- git clone git@github.com:<your repo name and stuff>

2. Enter the local repository that was created on your computer. Then do a pull to see that it works. You will have to enter your key passphrase. 

	- cd <repo name>
	- git pull

3. Create/edit a file. 

	- If you already have a file in the repository you could edit it. Otherwise create a file with your favourite editor, or just use `touch <filename>` if you are on Linux. 

4. Add and commit the file. 

	- Add the file with `git add <filename>`
	- Commit the file with `git commit -m "<filename>"`. Using the flag "-m" means you are just committing with the following message instead of opening a editor for writing the message. 

5. Push the file. 

	- Use `git push`
	- You will be asked for the passphrase

