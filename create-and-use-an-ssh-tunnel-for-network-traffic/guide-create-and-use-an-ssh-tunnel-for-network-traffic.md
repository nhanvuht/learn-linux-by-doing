# Create and Use an SSH Tunnel for Network Traffic

Our security team has dictated that all traffic leaving Datacenter 2 (where the CentOS 7 CLIENT is installed) must be encrypted.

Since  `yum`  makes http calls that means that it can't run updates or install new packages with the current setup.

Your SSH Tunnel SERVER is running a web server on port 80. Once the tunnel is set up another team will set the SERVER up as a yum repository. You've been tasked with setting up an SSH tunnel so that traffic can be encrypted from the CLIENT to the SERVER which will allow the CLIENT to install new packages. You should additionally create an SSH key so that a password isn't required to connect from the CLIENT to the SERVER as the user cloud_user.

## Objectives


### Make sure you can SSH from the CLIENT to the SERVER without a password

You need to generate an SSH key and copy it over to the SERVER from the CLIENT.

To generate the key simply run:  `ssh-keygen`  and accept all defaults.

To copy the key over to the SERVER simply run:

`ssh-copy-id cloud_user@10.0.1.100`  and enter the password.

### Verify that your SSH tunnel works.

For this task you need to have an SSH tunnel set up. To do so, simply enter the following command:

`ssh -f cloud_user@10.0.1.100 -L 2000:10.0.1.100:80 -N`

## Additional Resources

When launched, this Learning Activity will present you with (2) CentOS 7 servers and connection credentials for each.

The first one will function as the SSH Tunnel Server and the second will function as a client. Once connected to the SSH Tunnel Server, open your Activity Guide for instructions on completing this activity
