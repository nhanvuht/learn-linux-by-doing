# Creating a Directory Structure in Linux

## Intro
We've got a researcher who needs a workstation set up. Before it's handed off, we need to create a certain directory and subdirectory structure, plus a couple of empty text files. This is fairly simple, so let's get right into it.

## Additional Resources

You are responsible for handing a workstation with a specified directory structure to a new user. This user is a historian and will need to keep notes on various research topics separated into eras of time. Within the user's home directory, a new folder called 'Projects' needs to exist with the following subfolders: ancient, classical, and medieval. Under the  _ancient_  directory, two more directories must exist: egyptian and nubian. Within the  _classical_  directory, a folder named  _greek_  must exist. Within the  _medieval_  directory, two more directories need to be created: britain and japan.

A new, empty file named  _further_research.txt_  should be in the  _nubian_  and  _greek_  directories.

At the last moment, the classical directory needs to be renamed to greco-roman

Once these tasks are done, hand the system over to your team member for verification.

## Objectives

### Create the 'Projects' Parent Directories

Create the first parent directory structure with the  `mkdir`  command, and use the  `-p`  switch:

`mkdir -p Projects/ancient 
mkdir Projects/classical
mkdir Projects/medieval`

or

`mkdir -p Projects/{ancient,classical,medieval}`

### Create the 'Projects' Subdirectories

Create the subdirectory structure:

`mkdir Projects/ancient/egyptian mkdir Projects/ancient/nubian 
mkdir Projects/classical/greek mkdir Projects/medieval/britain 
mkdir Projects/medieval/japan`

or

`mkdir Projects/ancient/{egyptian,nubian} 
mkdir Projects/classical/greek 
mkdir Projects/medieval/{britain,japan}`

### Create 'Projects' Empty Files for Next Step

Create the empty files for later use:

`touch Projects/ancient/nubian/further_research.txt touch Projects/classical/greek/further_research.txt`

### Rename a 'Projects' Subdirectory

The user would like for the  _classical_  directory to be renamed to  _greco-roman_.

`mv Projects/classical Projects/greco-roman`





## Solution: Create the Parent Directories

### By Hand

We can create the directory structure by hand with these three commands:

`[cloud_user@host]$ mkdir -p Projects/ancient`

`[cloud_user@host]$ mkdir Projects/classical`

`[cloud_user@host]$ mkdir Projects/medieval`

### With Bash Expansion

We could do it another way, though, using Bash expansion. It's much less typing. This command makes all three directories in one pass:

`[cloud_user@host]$ mkdir -p Projects/{ancient,classical,medieval}`

## Create the Subdirectories

Now, let's create the next level of subdirectories. Again, there are two ways to do it.

### By Hand

`[cloud_user@host]$ mkdir Projects/ancient/egyptian`

`[cloud_user@host]$ mkdir Projects/ancient/nubian`

`[cloud_user@host]$ mkdir Projects/classical/greek`

`[cloud_user@host]$ mkdir Projects/medieval/britain`

`[cloud_user@host]$ mkdir Projects/medieval/japan`

### With Bash Expansion

`[cloud_user@host]$ mkdir Projects/ancient/{egyptian,nubian}`

`[cloud_user@host]$ mkdir Projects/classical/greek`

`[cloud_user@host]$ mkdir Projects/medieval/{britain,japan}`

## Create Some Empty Files

We've got to create a couple of empty text files for the researcher to use, and we'll do it with the  `touch`  command:

`[cloud_user@host]$ touch Projects/ancient/nubian/further_research.txt`

`[cloud_user@host]$ touch Projects/classical/greek/further_research.txt`

## Rename a Subdirectory

We thought we were all done, but heard back from the rest of the team that this researcher needs the  `classical`  directory renamed to  `greco-roman`. We can do that easily with the  `mv`  command:

`[cloud_user@host]$ mv Projects/classical Projects/greco-roman`

And now we can hand the system back to the team.

## Conclusion

You're all set. Congratulations on completing this lab!
