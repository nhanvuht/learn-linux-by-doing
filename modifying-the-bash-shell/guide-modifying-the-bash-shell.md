# Modifying the Bash Shell

## Scenario
A Linux system administrator should have a solid understanding of the Bash shell environment. The Bash shell is the default command line interface used on the vast majority of Linux distributions. Linux administrators can extend the capabilities of the Bash shell by providing their own aliases to commonly used commands and options, as well as create their own functions to use in the Bash environment. In this hands-on lab, we will create our own alias for a command and then create a new command that will take a positional argument.

## Objectives
Create the alias.

Load and test the alias.

Create your function.

Use the `webspace` function.

## Additional Resources

You have just started a new job managing a web server for a small company. To make your job a bit easier, you have decided to create some shorthand commands that will help you in your daily tasks.

1.  First, you will create an alias to view the status of the HTTP service that is running on the company's small web server.
    
2.  Next, you will create a function that allows you to monitor the disk usage of a couple of web content directories.

## Instructions

You have just started a new job managing a web server for a small company. To make your job a bit easier, you have decided to create some shorthand commands that will help you in your daily tasks.

1.  First, you will create an alias to view the status of the HTTP service that is running on the company's small web server.
    
2.  Next, you will create a function that allows you to monitor the disk usage of a couple of web content directories.
    

## Solution

Begin by logging in to the lab server using the credentials provided on the hands-on lab page:

`ssh cloud_user@PUBLIC_IP_ADDRESS`

### Create the alias

The first step is to create an alias for the Bash shell that will allow you to view the service status of the web server itself. You will name this alias  `webstat`. When you type the command  `webstat`  at the prompt, you will see the output of the command  `systemctl status httpd.service`.

User-created aliases and functions should go in your local  `~/.bashrc`  file. Using the commands listed, append the following alias to your  `~/.bashrc`  file:

`echo 'alias webstat="systemctl status httpd.service"' >> /home/cloud_user/.bashrc`

### Load and test the alias

Now that we have created an alias that displays the status of the web server, we need to tell Bash that we want to use it in our current session. First, we need to source our  `.bashrc`  file using the “dot” (`.`) command:

`. ~/.bashrc`

Now that the Bash environment has been refreshed with the new alias from our  `~/.bashrc`  file, we can use our new alias:

`webstat`

We should be able to see the output of our service's status command.

### Create your function

The next step is to create a function that will take the name of a directory as a parameter and print out how much disk space that directory is using.

Using the vi text editor, open up the  `~/.bashrc`  file and add the following function to the bottom, beneath the alias that you created earlier:

`vim ~/.bashrc`

`function webspace() { du -h /var/www/html/$1; }`

Save and close your file. Then source the  `.bashrc`  file again:

`. .bashrc`

### Use the  `webspace`  function

Since the  `/var/www/html`  directory is the root location for all of the individual site locations for this web server, all you need to do is provide the name of the folder that contains a particular part of the site to the  `webspace`  function. To view the size and contents of the main public web page, enter this command:

`webspace main`

This will print out the contents of the  `/var/www/html/main`  directory and how much disk space this directory uses. The  `$1`  used in your function is a positional argument. When you type  `webspace main`  at the prompt, the word  `main`  is replaced by the  `$1`  argument, thus providing the output of the command for the  `/var/www/html/main`  directory.

Try the same command again, this time for the  `customer`  directory on the web server:

`webspace customer`

You should see more directories in the output, plus a 5 MB client binary file.

## Conclusion

Congratulations, you've completed this hands-on lab!
