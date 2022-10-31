# Configuring a Default Boot Target

## Introduction

The LPIC-1 exam expects the candidate to know how to change a default target for a Linux computer using systemd. This exercise will assist you in your practice of determining what the default target is, and changing it to a new one.

**Note:**  If you have an issue connecting to the instance, wait a minute or two to allow the instance to finish provisioning and retry.

## Check the Default Target

The current default target is set to multi-user.target. Use the appropriate command to verify this:

`systemctl get-default`

## Change the Default Target

The administrator will need to change the default target so that the computer boots into a graphical desktop:

`sudo systemctl set-default graphical.target`

## Check the Default Target again

Now verify that the system is set for a graphical boot:

`systemctl get-default`

## Additional Resources

Your developers share a system that utilizes a desktop environment for the IDE tools. The other system administrator changed the environment so that it only boots into a command line shell, just before he went on vacation. You will need to correct the default boot environment.

Once you have set up the system to boot into a desktop environment, hand it back over to the developers for their use.


