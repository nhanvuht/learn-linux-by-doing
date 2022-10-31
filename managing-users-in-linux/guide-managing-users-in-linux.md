
# Managing Users in Linux



## Introduction

In this lab we are going to manage users and groups to get some practice using these utilities. Knowing how to manage users and permissions means our servers will be more secure.

## Objectives

### Add the Users to the Server

To add users to the system we can run

`useradd <username>`

So we would run

`useradd tstark`

`useradd cdanvers`

`useradd dprince`

### Create the `superhero` Group

To create a new group we would run

`groupadd <groupname>`

So for this task

`groupadd superhero`

### Set `wheel` Group as the the `tstark` Account's Primary Group

For this task we would run  `usermod`  like this

`usermod -g wheel tstark`

### Add `superhero` as a Supplementary Group on All Three Users

There isn't an easy way to do this all at once, so we need to run the following command for each user

`usermod -aG superhero <username>`

So

`usermod -aG superhero tstark`

`usermod -aG superhero dprince`

`usermod -aG superhero cdanvers`

### Lock the `dprince` Account

To lock an account all we have to do is run:

`usermod -L dprince`

## Additional Resources

We have some users that need to be set up on a new machine.

Tony Stark, Diana Prince, and Carol Danvers are developers for a project we're involved with. We need to add user accounts for them to the server, and then create the  `superhero`  group for all of them to be members of.

Tony Stark is a superuser, so we'll replace his primary group with the  `wheel`  group.

But wait! We realize a couple weeks in that Diana Prince has been forced to take leave, in order to fight evil. We'll have to lock her account until she can return.

To get started, log in to the lab server using the credentials provided and then become  `root`  by running:

`sudo -i`

## Solution

1.  Log in to the server using the credentials provided:
    
    `ssh cloud_user@<PUBLIC_IP_ADDRESS>`
    
2.  Become  `root`:
    
    `sudo -i`
    
    Enter the  `cloud_user`  password at the prompt.
    

### Add the Users to the Server

1.  Add our users:
    
    `useradd tstark`
    
    `useradd cdanvers`
    
    `useradd dprince`
    

### Create the  `superhero`  Group

1.  Create the new group:
    
    `groupadd superhero`
    

### Set  `wheel`  Group as the the  `tstark`  Account's Primary Group

1.  The  `usermod`  command will change which group a user is in. Change  `tstark`:
    
    `usermod -g wheel tstark`
    
2.  Make sure it worked:
    
    `id tstark`
    
    The command's output should show his primary group is now  `wheel`.
    

### Add  `superhero`  as a Supplementary Group on All Three Users

1.  Run the  `usermod`  command for each user:
    
    `usermod -aG superhero tstark`
    
    `usermod -aG superhero dprince`
    
    `usermod -aG superhero cdanvers`
    
2.  Check with any of the users to make sure it worked:
    
    `id <USERNAME>`
    
    We should see they're now in  `superhero`, as well as their own groups.
    

### Lock the  `dprince`  Account

1.  Run the following:
    
    `usermod -L dprince`
    

## Conclusion

Well, we did it. We got all of the required users set up and in the groups they needed to be in. And in the end, we were able to lock Diana's account down while she flies her invisible jet around chasing criminals. Congratulations!
