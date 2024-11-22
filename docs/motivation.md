---
title: "Lecture 1: Motivation"
tags: Lecture, Birgitte, day 1
description: "Why use version control?" 
---

<!-- Lecture material made by Mirko Myllykoski for the version of the course that was given in fall 2020. The lecture was first given by Mirko Myllykoski in fall 2020.
Very minor modifications have been made by Birgitte Brydsö for the fall 2021, fall 2022, fall 2023, and fall 2024 versions of the course.-->

<!-- Slides: https://hackmd.io/@git-fall-2024/L1-motivation/ --> 

---

# What is version control?

---

In software engineering, version control (also known as revision control, source control, or source code management) is a class of systems responsible for __managing changes__ to computer programs, documents, large web sites, or other collections of information.
--- Wikipedia

---

## Version control systems (VCS)

... systems responsible for **managing changes** ...

---

## Why use version control?

---

In an ideal world, things develop linearly: 

- Every new version is an improvement upon the previous version. 
    - No need to backtrack. 
- Everyone knows what everyone else is doing 
- In the end, things are simply finished. 

```mermaid
flowchart LR
    A@{ shape: stadium, label: "Monday's improvements"} --> B@{ shape: stadium, label: "Tuesday's improvements"}
    B --> C@{ shape: stadium, label: "Wednesday's improvements"}
```

```mermaid
%% Direction is top->down
flowchart TD

    %% Give a white background, instead of a transparent one
    classDef node fill:#fff,color:#000,stroke:#000
    classDef focus_node fill:#fff,color:#000,stroke:#000,stroke-width:4px
    classDef basic_node fill:#fdd,color:#000,stroke:#f00
    classDef basic_extra_node fill:#ffd,color:#000,stroke:#ff0
    classDef intermediate_node fill:#dfd,color:#000,stroke:#0f0
  
    %% subgraph sub_basic_use[Basic use of Bianca]
      understand_login(Understand login, has 2FA):::basic_node
      can_login_to_remove_desktop(Can login to remote deskop):::basic_node
      can_login_to_console(Can login to console):::basic_extra_node
      can_navigate_filesystem_using_gui(Can navigate filesystem using GUI):::basic_node
      can_navigate_filesystem_using_cli(Can navigate filesystem using CLI):::basic_extra_node
      can_find_wharf(Can find the wharf):::basic_node
      can_use_command_line_1(Can use the command line 1):::basic_node
      can_use_modules(Can use modules):::basic_node
      can_use_interactive_node(Can use an interactive node):::basic_node
      can_manage_files_using_cli(Can manage files using CLI):::basic_extra_node
      can_schedule_jobs(Can schedule jobs):::basic_node
      can_create_bash_script_using_cli(Can create a bash script using CLI):::basic_node
      can_tranfer_files_using_gui(Can transfer files using GUI):::basic_node
    %% end
    %% style sub_basic_use fill:#fcc,color:#000,stroke:#fcc

    %% subgraph sub_intermediate_use[Intermediate use of Bianca]
      can_tranfer_files_using_rsync(Can transfer files using rsync):::intermediate_node
      can_use_command_line_2(Can use the command line 2):::intermediate_node
      can_use_custom_software(Can use custom software):::intermediate_node
      can_use_custom_python_pip(Can use custom Python packages using pip):::intermediate_node
      can_use_custom_python_conda(Can use custom Python packages using conda):::intermediate_node
      can_use_custom_r(Can use custom R packages):::intermediate_node
      can_use_container(Can use a container):::intermediate_node
      can_build_from_source(Can build software from source):::intermediate_node

      can_monitor_jobs(Can monitor jobs):::intermediate_node
      can_use_gpus(Can use GPUs):::intermediate_node
      can_use_partitions(Can use partitions):::intermediate_node
      can_use_ide(Can use an IDE):::intermediate_node
    %% end
    %% style sub_intermediate_use fill:#ffc,color:#000,stroke:#ffc


    %% Basic
    understand_login --> can_login_to_remove_desktop
    can_login_to_remove_desktop --> can_login_to_console
    can_login_to_remove_desktop --> can_use_command_line_1
    can_login_to_remove_desktop --> can_navigate_filesystem_using_gui
    can_navigate_filesystem_using_gui --> can_find_wharf
    can_login_to_console --> can_navigate_filesystem_using_cli
    can_navigate_filesystem_using_cli --> can_find_wharf
    can_find_wharf --> can_tranfer_files_using_gui
    understand_login --> can_login_to_console
    can_login_to_console --> can_use_command_line_1
    can_use_command_line_1 --> can_use_modules
    can_use_command_line_1 --> can_use_interactive_node
    can_use_command_line_1 --> can_use_command_line_2
    can_use_command_line_1 --> can_create_bash_script_using_cli
    can_use_command_line_1 --> can_schedule_jobs
    can_navigate_filesystem_using_cli --> can_manage_files_using_cli
    can_use_modules --> can_schedule_jobs
    can_create_bash_script_using_cli --> can_schedule_jobs

    %% Basic -> Intermediate
    can_manage_files_using_cli --> can_tranfer_files_using_rsync
    can_find_wharf --> can_tranfer_files_using_rsync
    can_schedule_jobs --> can_monitor_jobs
    can_schedule_jobs --> can_use_gpus
    can_schedule_jobs --> can_use_partitions
    can_use_interactive_node --> can_use_ide
    can_use_modules --> can_use_ide

    %% Make sure Intermediate is below Basic,
    %% using invisible nodes
    can_schedule_jobs ~~~ can_use_command_line_2

    %% Intermediate
    can_use_command_line_1 --> can_tranfer_files_using_rsync
    can_use_command_line_2 --> can_use_custom_software

    can_use_custom_software --> can_use_custom_python_pip
    can_use_custom_software --> can_use_custom_python_conda
    can_use_custom_software --> can_use_custom_r
    can_use_custom_software --> can_build_from_source
    can_use_custom_software --> can_use_container
```


---

In the real world, things develop non-linearly: 

- A new version can be anything between 
    - a complete catastrophe and 
    - a major breakthrough.
- People do not know what others are doing 
- Sometimes we are simply fixing earlier mistakes... 

```graphviz
digraph {
  rankdir=LR
  Mon[label="Monday's\n improvements"] [fixedsize=circle]
  Tue[label="Tuesday's\n mistakes"] [fixedsize=circle]
  Wed[label="Wednesday's\n corrections"] [fixedsize=circle]
  Mon -> Tue
  Tue -> Wed
}
```
<!-- .element: class="fragment" data-fragment-index="3" -->

---

### Going back to an earlier version

Sometimes, it is easier to simply backtrack to an *earlier version*...

```graphviz
digraph {
  rankdir=LR
  Mon[label="Monday's\n improvements"] [fixedsize=circle]
  Tue[label="Tuesday's\n mistakes"] [fixedsize=circle]
  Wed[label="Wednesday's\n improvements"] [fixedsize=circle]
  Mon -> Tue
  Mon -> Wed
}
```

---

#### Where is this *earlier version*?

 - CTRL + Z <!-- .element: class="fragment" -->
 - my_file.txt, my_file.txt.old, ... <!-- .element: class="fragment" -->
 - My project/ <!-- .element: class="fragment" -->
     - 2020-08-12/
     - 2020-08-13/
     - ...
 - Daily home directory backup <!-- .element: class="fragment" -->

---

#### Challenges and obstacles

 - Prone to mistakes <!-- .element: class="fragment" -->
     - CTRL + Z has limits, overwritten/deleted files, human/hardware error <!-- .element: class="fragment" -->
 - How much to save? <!-- .element: class="fragment" -->
     - Individual files? Everything? How much space is required? <!-- .element: class="fragment" -->
 - How to organize versions? <!-- .element: class="fragment" -->
     - What is the difference between different versions? <!-- .element: class="fragment" -->

*Overall, difficult to manage!* <!-- .element: class="fragment" -->

---

#### What about the granularity?

```graphviz
digraph {
  rankdir=LR

  subgraph cluster1 {
    t1a [label="Component A\n improvement"] [fixedsize=circle]
    t1b [label="Component B\n mistake"] [fixedsize=circle]
    t1c [label="Component C\n improvement"] [fixedsize=circle]
    label="Mondays's changes"
  }

  subgraph cluster2 {
    t2a [label="Component A\n improvement"] [fixedsize=circle]
    t2b [label="Component B\n correction"] [fixedsize=circle]
    t2c [label="Component C\n mistake"] [fixedsize=circle]
    label="Tuesday's changes"
  }

  subgraph cluster3 {
    t3a [label="Component A\n mistake"] [fixedsize=circle]
    t3b [label="Component B\n improvement"] [fixedsize=circle]
    t3c [label="Component C\n correction"] [fixedsize=circle]
    label="Wednesday's changes"
  }
  
  t1a -> t2a
  t1b -> t2b
  t1c -> t2c

  t2a -> t3a
  t2b -> t3b
  t2c -> t3c
}
```

*This compounds the problems!*

---

#### How does VCS solve this?

 - Stores the history using snapshots (commits) <!-- .element: class="fragment" -->
     - Each snapshot represents the project at a given point in time <!-- .element: class="fragment" -->
 - Manages snapshots and associated metadata <!-- .element: class="fragment" -->
     - Naming (tags), comments, dates, authors, etc <!-- .element: class="fragment" -->
 - Easy to move between different snapshots <!-- .element: class="fragment" -->
 - Can handle different degrees of granularity <!-- .element: class="fragment" -->
 - Can handle multiple development paths (branches) <!-- .element: class="fragment" -->

---

### Comparing and joining

 - VCS makes it easy to compare different snapshots <!-- .element: class="fragment" -->
     - Named revisions, comments, time information, author information <!-- .element: class="fragment" -->
     - Diff tools <!-- .element: class="fragment" -->
     - Search tools <!-- .element: class="fragment" -->
     - Bisection search <!-- .element: class="fragment" -->
 - VCS also allows the joining (merging) of different snapshots  <!-- .element: class="fragment" -->
     - Easy to experiment with ideas <!-- .element: class="fragment" -->

---

### Collaboration

 - One of the primary functions of VCS is to allow collaboration <!-- .element: class="fragment" -->
 - Usual setup: server (remote) + multiple clients <!-- .element: class="fragment" -->
     - People work locally and send (push) the changes to the server <!-- .element: class="fragment" -->
     - VCS keeps track of what has been done and by whom <!-- .element: class="fragment" -->
 - Safer since mistakes can be easily remedied <!-- .element: class="fragment" -->
 - The contributions of several people can be merged <!-- .element: class="fragment" -->

---

### Backup

 - VCS functions as a backup <!-- .element: class="fragment" -->
 - Locally, the system maintains a copy of each file <!-- .element: class="fragment" -->
     - Usually only the changes or the files that have changed are stored <!-- .element: class="fragment" -->
 - Globally, lost files can be recovered from the server <!-- .element: class="fragment" -->

---

### Integration

 - VCSs such as Git have been integrated with several services <!-- .element: class="fragment" -->
     - HackMD, Overleaf, ...
 - Services such as GitHub can do almost everything for you <!-- .element: class="fragment" -->
     - Store history, distribute, testing / continuous integration, bug reports, milestones, website, ... <!-- .element: class="fragment" -->

---

### Summing up

Version control systems

- keeps track of your files and other output
- tracks what is created and modified
- tracks who made the modifications
- tracks why the modifications were made (if you make good commit comments)

---

## Practical use cases

What are the practical use cases for VCS?

---

### Source code

 - Many VCSs are designed for managing source code <!-- .element: class="fragment" -->
 - Manage deployment (production, development, testing, etc) <!-- .element: class="fragment" -->
 - Manage published versions (v0.1 etc) <!-- .element: class="fragment" -->
 - Manage (experimental) features <!-- .element: class="fragment" -->
 - Bug hunting <!-- .element: class="fragment" -->
 - But also for: writers, artists, composers... <!-- .element: class="fragment" -->

---

### Latex files

 - Track which version of a manuscript has been <!-- .element: class="fragment" -->
     - submitted, 
     - revised and/or 
     - accepted
 - Collaboration between several authors <!-- .element: class="fragment" -->

---

### HPC: batch files and data

 - Track different versions of your batch scripts <!-- .element: class="fragment" -->
     - Easy to check the used configuration afterwards
 - Track input and output files <!-- .element: class="fragment" -->
     - Limited to smallish files

---

### Examples of VCS

<!-- .slide: style="font-size: 24px;" -->

- SCCS: The first VCS. Created in 1972 at Bell Labs. Was available only for UNIX and worked with Source Code files only.
- RCS (Revision Control System): First release July 1985. Usually superseded by other systems such as CVS, which began as a wrapper on top of RCS. 
- CVS (centralized version control system): First release July 1986; based on RCS. Expands on RCS by adding support for repository-level change tracking, and a client-server model. 
- Apache Subversion (SVN): First release in 2004 by CVS developers with the goal of replacing CVS. 
- BitKeeper: Initial release May 2000. Distributed version control. Was shortly used for developing the Linux kernel. Proprietary. No longer maintained.
- **Git**: Started by Linus Torvalds in April 2005, originally for developing the Linux kernel. Distributed version control. Open source. 
- ...

---

