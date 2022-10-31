
# Managing File Attributes and Permissions

## Scenario

Your organization's development team is working on their new Web-based API. They have just had another developer leave the team and they were working on a key component of the API. The directory he was working in will not allow anyone else on the system to even view the files within the directory. You have been asked to provide the team with a view into that directory by resetting the file and directory permissions. First, you have been provided with the credentials and connection information to the server in question and asked to change the permissions on the /opt/myapp directory so that everyone can change to and read the files within that directory. They have also requested that you ONLY change the permissions of the files and directories within the /opt/myapp directory so that everyone has read and write (but not execute). Please be sure to apply those permissions to all subdirectories recursively. Once you verify the files and directories are accessible, you can turn it back to the development team to continue their work.

## Goals

1.  Reset a directory's permissions to the following:
    -   Everyone can access the directory
    -   Everyone can read the files in the directory
    -   No one can execute files in the directory
2.  Apply all of these permissions to all subdirectories recursively

## Additional Resources

Your organization's development team is working on their new Web-based API. They have just had another developer leave the team and they were working on a key component of the API. The directory he was working in will not allow anyone else on the system to even view the files within the directory.

You have been asked to provide the team with a view into that directory by resetting the file and directory permissions. First, you have been provided with the credentials and connection information to the server in question and asked to change the permissions on the /opt/myapp directory so that everyone can change to and read the files within that directory.

They have also requested that you ONLY change the permissions of the files and directories within the /opt/myapp directory so that everyone has read and write (but not execute for files). Please be sure to apply those permissions to all subdirectories recursively. Once you verify the files and directories are accessible, you can turn it back to the development team to continue their work.

## Objectives

### Reset Permissions on /opt/myapp Directory

In order to allow access to the /opt/myapp directory, the student will need to provide specific permissions to the directory itself so it can be read by users other than the owner.

Accomplish this task with:

`sudo chmod 755 /opt/myapp`

Optionally, although less secure, the following would meet the requirements as well:

`sudo chmod 777 /opt/myapp`

### Permissions on Files and Folders Within /opt/myapp

The student is asked to allow read and write permissions to all files and folders within the /opt/myapp directory (including files within the subfolders recursively).

This task can be completed successfully via:

`sudo chmod 666 -R /opt/myapp/*`

**Note:**  For users to be able to navigate into directories, the directories must be set as executable. You can do this with:

`sudo find /opt/myapp -type d -exec chmod o+x {} \;`


## Solution

### Grant Access to the Directory

Change to the  `opt`  directory.

`cd /opt`

Next, open all of the directory's files and permissions with the following command:

`ls -la`

Let's try to access the  `myapp`  directory. Run the following command:

`cd myapp/`

We get a "Permission denied" message because permissions are currently restricted to the  `tkirk`  user. Let's change that now. Enter the following command:

`sudo chmod 777 myapp`

Then, enter your password when prompted.

Reopen the directory files and permissions using the  `ls -la`  command. Now let's try to open the directory again.

`cd myapp`

We can now open the directory.

### Change the Directory Permissions

The next step is to give all users read and write permissions for this directory. However, we also need to make sure no one can execute anything. Let's start by removing execute permissions. Enter the following command:

`sudo chmod -f -x -R *`

Now let's give everyone read and write permissions. Note that this would also remove the execute permissions we did in the previous step, but we wanted to show how to do that explicitly.

`sudo chmod 666 -f -R *`

List the directory files and permissions again.

`ls -la`

We can see that everyone now has read and write permissions.

**Note:**  For users to be able to navigate into directories, the directories must be set as executable. You can do this with:

`sudo find /opt/myapp -type d -exec chmod o+x {} \;`

## Conclusion

Congratulations, you've successfully completed this lab!
