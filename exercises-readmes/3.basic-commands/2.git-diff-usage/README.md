## Exercise

The purpose of this exercise is to show you the usage of the *git diff* command.

1. Create a folder called "myfirstrepo" which will contain your repository. 
Tasks:
      - initialize the repository
      - create a README.md file and add this text on the first line: "File created on Sep. 30, 2020" 
      - stage the file
      - commit the changes

At this point, your working directory, the staging area, and the local repository
(committed changes) are all synchronized.

2. Make a change to the README.md file by adding a line with the string "TODO list". Now, the
staging area and the local repository are synchronized with each other but the working
directory is not synchronized with them. 
      - check the differences between the working directory and the staging area
        (hint: git diff)
      - check the differences between the working directory and the local repository
        (hint: git diff HEAD)

confirm that the changes correspond to what you expected by looking at the diff outputs.

3. Add the file README.md to the staging area. Now, the working directory and the staging area
are synchronized with each other but they are not synchronized with the local repository.
      - check the differences between the staging area and the local repository
        (hint: git diff --staged)
      - check the differences between the working directory and the local repository
        (hint: git diff HEAD)

confirm that the changes correspond to what you expected by looking at the diff outputs.

4. Make an additional modification to the README.md file by adding a line with the string 
"Add the support email". Now, all the three areas working directory, the staging area
and the local repository are not synchronized with each other. 
      - check the differences between the working directory and the staging area
        (hint: git diff)
      - check the differences between the staging area and the local repository
        (hint: git diff --staged)
      - check the differences between the working directory and the local repository
        (hint: git diff HEAD)


confirm that the changes correspond to what you expected by looking at the diff outputs.

5. End of exercise
