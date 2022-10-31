
# Generating and Exchanging SSH Keys for Secure Access

## Introduction

Understanding the creation and exchange of SSH keys is a key concept to grasp as a new system administrator. In this lab, we will generate keys on two systems using the  `ssh-keygen`  utility and learn how to exchange and verify the keys with a remote system using  `ssh-copy-id`  and associated key files on each. At the end of this lab, you will understand how to create secure keys for remote access, how to exchange them, and where to store them on each system involved in the chain.

## Scenario

The development team in your organization is setting up their new development servers in preparation for the creation of a new web-based API. They are going to be creating configurations, copying files, etc. between two servers using a single service account. You have been provided with credentials and connectivity information to those two new server instances. The service account they wish to use is the `cloud_user` account that you were provided. Following company security policy, a complex password has been set that is making periodic connections, copies, and service configuration hard for the team. They have asked you to simplify the process and create a trust for the service account between the two systems.

## Objectives

0 of 4 completed

Create the Key on Server 1

1.  In your terminal, log in to Server 1.

`` `ssh cloud_user@[SERVER1_PUBLIC_IP]` ``

1.  Change to the  `.ssh`  directory.

`cd .ssh`

1.  Generate a key for Server 1.

`ssh-keygen`

1.  List the contents of the  `id_rsa.pub`  file.

`cat id_rsa.pub`

1.  Copy the output of this command to your clipboard.

Create the Key on Server 2

1.  Log in to Server 2.

`` `ssh cloud_user@[SERVER2_PUBLIC_IP]` ``

1.  Change to the  `.ssh`  directory.

`cd .ssh/`

1.  Install the nano text editor.

`sudo yum install nano`

1.  Open the  `authorized_keys`  file in nano.

`nano authorized_keys`

1.  Add the key we just generated to the file. (Note: We don't see the other accounts shown in the video, but it won't impact the lab activity.)
2.  Press  **Ctrl + X**.
3.  Press  **Y**  and then  **Enter**  to save the changes.

Exchange the SSH Keys between the Servers

1.  In your Server 2 terminal window, create a new key.

`ssh-keygen`

1.  List the contents of the  `id_rsa.pub`  file.

`cat id_rsa.pub`

1.  Copy the output of this command to your clipboard.
2.  Type  `exit`  to log out of Server 2.
3.  Install nano.

`sudo yum install nano`

1.  Open the  `authorized_keys`  file in nano.

`nano authorized_keys`

1.  Add the key we just generated to the file.
2.  Press  **Ctrl + X**.
3.  Press  **Y**  then  **Enter**  to save the changes.

Test the Configuration

1.  Attempt to log in to Server 2 from Server 1 without a password.

`` `ssh cloud_user@[SERVER2PUBLIC_IP]` ``

1.  Attempt to log in to Server 1 from Server 2 without a password.

`ssh cloud_user@[SERVER1PUBLIC_IP]`

## Create the SSH Keys on Server 1 and Server 2

### Create the Key on Server 1

1.  In your terminal, log in to Server 1.

`ssh cloud_user@&lt;SERVER1_PUBLIC_IP&gt;`

1.  List the contents of the current directory.

`ls -la`

1.  Change to the  `.ssh`  directory.

`cd .ssh`

1.  List the contents of the  `.ssh`  directory.

`ls -la`

1.  Generate a key for Server 1.

`ssh-keygen`

1.  Press  **Enter**  at the next three prompts.
2.  List the contents of the  `.ssh`  directory again.

`ls -la`

1.  List the contents of the  `id_rsa.pub`  file.

`cat id_rsa.pub`

1.  Copy the output of this command to your clipboard.

### Create the Key on Server 2

1.  Log in to Server 2.

`ssh cloud_user@&lt;SERVER2_PUBLIC_IP&gt;`

1.  Change to the  `.ssh`  directory.

`cd .ssh/`

1.  List the contents of the  `.ssh`  directory.

`ls -la`

1.  Install the nano text editor.

`sudo yum install nano`

1.  Enter your password at the prompt.
2.  Open the  `authorized_keys`  file in nano.

`nano authorized_keys`

1.  Add the key we just generated to the file. (Note: We don't see the other accounts shown in the video, but it won't impact the lab activity.)
2.  Press  **Ctrl + X**.
3.  Press  **Y**  and then  **Enter**  to save the changes.

## Exchange the SSH Keys between the Servers

1.  In your Server 2 terminal window, create a new key.

`ssh-keygen`

1.  Press  **Enter**  for the next three prompts.
2.  List the contents of the current directory.

`ls -la`

1.  List the contents of the  `id_rsa.pub`  file.

`cat id_rsa.pub`

1.  Copy the output of this command to your clipboard.
2.  Type  `exit`  to log out of Server 2.
3.  Install nano.

`sudo yum install nano`

1.  Type  `y`  to continue.
2.  List the contents of the current directory.

`ls -la`

1.  Open the  `authorized_keys`  file in nano.

`nano authorized_keys`

1.  Add the key we just generated to the file.
2.  Press  **Ctrl + X**.
3.  Press  **Y**  then  **Enter**  to save the changes.

## Test the Configuration

1.  Attempt to log in to Server 2 from Server 1 without a password.

`ssh cloud_user@&lt;SERVER2PUBLIC_IP&gt;`

1.  Attempt to log in to Server 1 from Server 2 without a password.

`ssh cloud_user@&lt;SERVER1PUBLIC_IP&gt;`

## Conclusion

Congratulations, you've successfully completed this hands-on lab!
