# Welcome to "Introduction to Git" course 

!!! Note "This material"
   
    Here you will find the content of the workshop "Introduction to Git".

    - Git repository for the course: <a href="https://github.com/hpc2n/course-intro-git" target="_blank">https://github.com/hpc2n/course-intro-git</a>. 

!!! Admonition "Content" 

    - This course aims to give a brief, but comprehensive introduction to using Git from the command line, as well as using GitHub. 
    - You will learn about
        - Basic commands
        - Basic concepts
        - The commit tree
        - Branches
            - merges
            - conflicts
        - Remote repositories
        - Git in teamwork

    - **We aim to give this course every fall.**

!!! Warning 

    **Target group**
 
    - This NAISS course is a given as a cooperation between trainers from the NAISS branches HPC2N and UPPMAX. 
    - It is open for anyone in Swedish academia. 
    - You will be using your own computer or other existing computer access for the course. If you do not have access to a computer that can run Git (or which you can install Git on), then there will be an option to use NAISS resources for this (Tetralith).

## Pre-requirements
    
- Basic knowledge of using the command line.
    - Some material for self-study here: 
        - <a href="http://docs.uppmax.uu.se/getting_started/linux/" target="_blank">UPPMAX Linux getting started</a>
        - <a href="https://docs.hpc2n.umu.se/tutorials/linuxguide/" target="_blank">Linux tutorial and "cheat sheet"</a>
        - <a href="https://github.com/hpc2n/intro-linux" target="_blank">HPC2N's Linux intro course material (including link to recordings)</a> 
- Basic knowledge of using a text editor of your choice on your system.
    - Information about Linux editors here: <a href="https://docs.hpc2n.umu.se/tutorials/linuxguide/#editors" target="_blank">https://docs.hpc2n.umu.se/tutorials/linuxguide/#editors</a>
- A <a href="https://github.com/" target="_blank">GitHub user account</a> (free - can be created for the course).
- A reasonably recent version of Git installed on your system. See <a href="https://git-scm.com/" target="_blank">the Git homepage</a>.

## Some practicals

### Zoom

- You should have gotten an email with the links    
- Main room for lectures (recorded)
- Possibly breakout rooms
    - exercises, including a silent room for those who just want to work on their own without interruptions. 
     help
- The **lectures and demos will be recorded**, but **NOT the exercises**. 
    - If you ask questions during the lectures, you may thus be recorded. 
    - If you do not wish to be recorded, then please keep your microphone muted and your camera off during lectures and write your questions in the Q/A document (see more information below about the collaboration documents which are also listed above).
- Use your REAL NAME.
- Please MUTE your microphone when you are not speaking
- Use the “Raise hand” functionality under the “Participants” window during the lecture. 
- Please do not clutter the Zoom chat. 
- Behave politely!
    
### Q/A collabration document

- Use the Q/A page for the workshop with your questions.
    - <a href="https://umeauniversity.sharepoint.com/:w:/s/HPC2N630/EdGtUQbzqvRDu1UFAj1vrEEBegJLNy3wzrUlu3-oQYyYkw" target="_blank">https://umeauniversity.sharepoint.com/:w:/s/HPC2N630/EdGtUQbzqvRDu1UFAj1vrEEBegJLNy3wzrUlu3-oQYyYkw</a>
    - Create a new line for new questions. Take care if others are editing at the same time. 

### Important info document 

- There is an "important info" document with information for the course. You have gotten an email with a link to this: <a href="https://umeauniversity.sharepoint.com/:w:/s/HPC2N630/Eapzrh9uWHBCj__7L63KFXkBAvUfBfEJfgvTfBHc-S0BiA?e=2GWXsM" target="_blank">https://umeauniversity.sharepoint.com/:w:/s/HPC2N630/Eapzrh9uWHBCj__7L63KFXkBAvUfBfEJfgvTfBHc-S0BiA?e=2GWXsM</a>

### Recordings

- The recordings of the course lectures will be uploaded to HPC2N's YouTube channel: <a href="https://www.youtube.com/@HPC2N" target="_blank">https://www.youtube.com/@HPC2N</a>. 

## Preliminary schedule

**Monday, 2025-11-03**

| Time | Topic | Activity | Teacher |
| ---- | ----- | -------- | ------- |
| 08:30 | Optional installation help (Git) | | All |
| 09:00 | Introduction and course info | Lecture | Birgitte |
| 09:10 | 0. Setup | Lecture+code along | Birgitte |
| 09:30 | 1. Why use version management? | Lecture | Birgitte | 
| 10:00 | Break (15 min) | | |
| 10:15 | 2. Basic commands, part 1 | Lecture+code along+exercises | Pedro |
| 11:15 | Break (15 min) | | 
| 11:30 | 2. Basic commands, part 2 | Lecture+code along+exercises | Pedro |
| 12:00 | End of first day | |

**Tuesday, 2025-11-04**

| Time | Topic | Activity |
| ---- | ----- | -------- | 
| 09:00 | 3. Basic concepts, part 1 | Lecture+code along | Birgitte |
| 10:15 | Break (15 min) | | 
| 10:30 | 3. Basic concepts, part 2 | Lecture+code along+exercises | Birgitte |
| 11:20 | Break (10 min) | |
| 11:30 | 4. Traversing the commit tree, part 1 | Lecture+code along | Diana |
| 12:00 | End of second day | 

**Wednesday, 2025-11-05**

| Time | Topic | Activity |
| ---- | ----- | -------- |  
| 09:00 | 4. Traversing the commit tree, part 2 | Lecture+code along+exercises | Diana |
| 10:15 | Break (15 min) | | 
| 10:30 | 4. Traversing the commit tree, part 3 | Lecture+code along+exercises | Diana |
| 11:00 | Break (10 min) | | 
| 11:10 | 5. Branches, merges, and conflicts, part 1 | Lecture+code along | Diana |
| 12:00 | End of third day | | 

**Thursday, 2025-11-06**

| Time | Topic | Activity |
| ---- | ----- | -------- |  
| 09:00 | 5. Branches, merges, and conflicts, part 2 | Lecture+code along+exercises | Diana |
| 09:55 | Break (10 min) | | 
| 10:05 | Brief intro to SSH-keys and using GitHub | Lecture+code along | Birgitte |
| 10:15 | 6. Working with remotes, part 1 | Lecture+code along | Pedro |
| 10:55 | Break (10 min) | | 
| 11:05 | 6. Working with remotes, part 2 | Lecture+code along+exercises | Pedro |
| 12:00 | End of fourth day | | 

**Friday, 2025-11-07** 

| Time | Topic | Activity |
| ---- | ----- | -------- |
| 09:00 | 7. Teamwork, part 1 | Lecture+code along+exercises | Birgitte |
| 09:55 | Break (10 min) | | 
| 10:05 | 7. Teamwork, part 2 | exercises | All |
| 10:50 | Break (10 min) | 
| 11:00 | 7. Team work, part 3 | exercises | All |
| 11:50 | Summary+evaluation | | 
| 12:00 | End of the course | | 
     

