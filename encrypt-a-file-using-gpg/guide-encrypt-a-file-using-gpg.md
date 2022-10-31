# Encrypt a File Using GPG

## Introduction

With the prevalence of cloud servers in use today, security should be at the forefront of their deployments. Just as important is the security of important local files and documents. We can employ the GNU Privacy Guard, or GPG, toolset to encrypt files; and through the use of sharing public keys with other users, we can decrypt files from other people. In this hands-on lab, we will walk through creating a new public GPG key, encrypt a file and sign it, and send that file to another user to decrypt with our public key.

## Objectives (WIP)


### Create a GPG Key for `cloud_user`

1.  After you log in to the server as the  `cloud_user`  account, generate a new GPG key, accepting the defaults for each prompt. For the user ID, enter  `cloud_user`, and for the email address, use  `cloud_user@localhost`. You can leave the comment field blank by just pressing  **Enter**.

`gpg --gen-key`

1.  Use the following for the key's passphrase:  `password321`  (In the real world, you would want to use a more secure passphrase!).
    
2.  After the key has been created, we will need to export it so that Gordon Freeman can decrypt files from us. Export the  `cloud_user`  public key for  `gfreeman`  to use.
    

`gpg -a -o gfreeman.key --export [key ID]`

`Use the public key reference ID from the output of the key generation.`

1.  Using the  `mail`  command, send an email to Gordon Freeman containing the  `cloud_user`  public key as an attachment.

`mail -s "here is your key" -a gfreeman.key gfreeman@localhost Don't lose this! I'll call you with the passphrase.`

1.  Press  **Enter**  after the final dot to send the message.

### Configure GPG for Gordon

1.  Now you will need to set up the GPG environment for Gordon Freeman. Use a secure shell session to log into the  `gfreeman`  account (the password for this user is the same as the  `cloud_user`  account).

`ssh gfreeman@localhost`

1.  Just as you did with the  `cloud_user`  account, generate a GPG key for Mr. Freeman, accepting the defaults for each prompt. For the user ID, enter  `gfreeman`, and for the email address, use  `gfreeman@localhost`. You can leave the comment field blank (just press  **Enter**).

`gpg --gen-key`

1.  Use the following for the key's passphrase:  `password321`  (In the real world, you would want to use a more secure passphrase!).
    
2.  After creating the key for Mr. Freeman, open up the  `mutt`  email client, and save the public key sent over by the  `cloud_user`  account. Press  **Enter**  on the email message, then the [`v`] key to view the attachment, and press the [`s`] key to save it to Mr. Freeman's home directory. Press the [`q`] key to exit  `mutt`.
    
3.  Now we need to import the public key from  `cloud_user`  into Mr. Freeman's keyring. Run the following command to do so:
    

`gpg --import gfreeman.key`

1.  Run the following command to view the contents of Mr. Freeman's keyring:

`gpg --list-keys`

1.  Log out of  `gfreeman`'s account:

`exit`

### Generate a Signed Document and Send It to Gordon

When we digitally sign a file, we are using our private GPG key to guarantee that this file came from us. The user that receives the file will use their copy of the public key from you to verify that the file was signed by you.

1.  Run the following command to generate a test document:

`echo "Just need you to verify this file." > note.txt`

1.  Now we are going to use  `cloud_user`'s  _private_  key to sign the file. Run the following command to do so, and use the passphrase that was set for the key:

`gpg --clearsign note.txt`

There should now be a  `note.txt.asc`  file in  `cloud_user`'s home directory.

1.  Create an email, attach the  `note.txt.asc`  file to the message, and send it to  `gfreeman@localhost`.

`mail -s "check this out" -a note.txt.asc gfreeman@localhost Could you verify this file for me?`

### Verify the Signature of the Emailed Document

1.  Use a secure shell session to log in to the  `gfreeman`  account (the password for this user is the same as the one for the  `cloud_user`  account).

`ssh gfreeman@localhost`

1.  Use the  `mutt`  email client to view and save the new email message's attachment.
    
2.  Next, verify the  `note.txt.asc`  file that was emailed using the following:
    

`gpg --verify note.txt.asc`

1.  You will receive a warning about the signature not being verified by a third party, and that's ok. What is important is the following line from the output:

`gpg: Good signature from "cloud_user <cloud_user@localhost>"`

This is what a verfied file displays.

1.  Next, encrypt a copy of the  `/etc/fstab`  file with the following:

`cp /etc/fstab ~ gpg -a -r cloud_user -e ~/fstab`

You will see a general warning displayed about the key possibly not belonging to the named person. We know that this key is from  `cloud_user`, as we have verified this. Type  `y`  at the prompt.

1.  Verify that there is a file called  `fstab.asc`  in  `gfreeman`'s home directory. Create a new email to  `cloud_user`, and attach this file:

`mail -s "looks good" -a fstab.asc cloud_user@localhost Can you decrypt this? .`

1.  Log out of Mr. Freeman's account:

`exit`

### Decrypt the Attached File

1.  As the  `cloud_user`, open up the  `mutt`  email client and save the  `fstab.asc`  attachment from the new email.
    
2.  Decrypt the saved  `fstab.asc`  file with the  `gpg`  command. Enter the passphrase for  `cloud_user`'s key when prompted.
    

`gpg fstab.asc`

1.  Verify that you can read the contents of the decrypted file.

`cat fstab`

====================

## Solution

### Log In to the Lab Environment

Use the credentials and server IP in the hands-on lab overview page to log into the lab server.

###  Create a GPG Key for  `cloud_user`

Generate a new GPG key:

`[cloud_user@host]$ gpg --gen-key`

Accept the defaults for each prompt. For the user ID, enter  `cloud_user`, and use  `cloud_user@localhost`  for the email address. We can leave the comment field blank by just pressing  **Enter**, and press  `o`  at the end for  _OK_.

We'll use  `password321`  when we're prompted for a passphrase, and when we're prompted to confirm it.

Now that the key has been created, we need to export it so that Gordon Freeman can decrypt files he gets from us. We'll do that like this:

`[cloud_user@host]$ gpg -a -o gfreeman.key --export &lt;KEY_ID>`

In that command, use the public key reference ID from the output of the key generation. It will be a random string, and the line it's sitting on (in the key generation output) looks like this:

`gpg: key XXXXXXXX marked as ultimately trusted`

Now, we'll use the  `mail`  command to send an email to Gordon Freeman containing the  `cloud_user`  public key as an attachment:

`[cloud_user@host]$ mail -s "here is your key" -a gfreeman.key gfreeman@localhost Don't lose this! I'll call you with the passphrase. .`

Include that final period (on the line by itself) and then press  **Enter**  to send the message.

### Configure GPG for Gordon

Now we've got to set up the GPG environment for Gordon Freeman. Rather than just  `su -`, we'll actually log in to our host as  `gfreeman`  with SSH. The password for  `gfreemen`  is the same as it is for the  `cloud_user`  account:

`[cloud_user@host]$ ssh gfreeman@localhost`

Just as we did with the  `cloud_user`  account, we'll generate a GPG key for Mr. Freeman, accepting the defaults for each prompt. The only difference will be having a user ID of  `gfreeman`  and an email address of  `gfreeman@localhost`:

`[gfreeman@host]$ gpg --gen-key`

Once we've created the key for Mr. Freeman, we can open up the  `mutt`  email client, and save the public key sent over by the  `cloud_user`  account:

`[gfreeman@host]$ mutt`

Arrow up and down to highlight the  `cloud_user`  message, then press  **Enter**. Press  `v`  to view the attachment, and press  `s`  to save it to Mr. Freeman's home directory. Finally, press  `q`  to quit Mutt.

Now, to import the public key from  `cloud_user`  into Mr. Freeman's keyring, run the following command:

`[gfreeman@host]$ gpg --import gfreeman.key`

We can run this to view the contents of Mr. Freeman's keyring:

`[gfreeman@host]$ gpg --list-keys`

Let's log out of  `gfreeman`'s account:

`[gfreeman@host]$ exit`

### Generate a Signed Document and Send It to Gordon

When we digitally sign a file, we are using our private GPG key to guarantee that this file came from us. The user that receives the file will use their copy of the public key from us to verify that we signed the file. Let's generate a test document:

`[cloud_user@host]$ echo "Just need you to verify this file." > note.txt`

Now we'll use  `cloud_user`'s  _private_  key to sign the file:

`[cloud_user@host]$ gpg --clearsign note.txt`

Remember that we need to use the passphrase we created earlier (`password321`).

Now there should now be a  `note.txt.asc`  file in  `cloud_user`'s home directory. We can run a quick  `ls`  to make sure.

Now that we've made the file, let's email it to  `gfreeman@localhost`:

`[cloud_user@host]$ mail -s "check this out" -a note.txt.asc gfreeman@localhost Could you verify this file for me? .`

### Verify the Signature of the Emailed Document

Log in to  `localhost`  again, as  `gfreeman`:

`[cloud_user@host]$ ssh gfreeman@localhost`

Use the  `mutt`  email client, and just as before, view and save the new email message's attachment.

Now, verify the  `note.txt.asc`  file that was emailed:

`[gfreeman@host]$ gpg --verify note.txt.asc`

We'll get a warning about the signature not being verified by a third party, and that's ok. What is important is the following line from the output:

`gpg: Good signature from "cloud_user <cloud_user@localhost>"`

This is what a verified file displays.

Next, encrypt a copy of the  `/etc/fstab`  file like this:

`[gfreeman@host]$ cp /etc/fstab ~ [gfreeman@host]$ gpg -a -r cloud_user -e ~/fstab`

You will see a general warning displayed about the key possibly not belonging to the named person. We already know that this key is from  `cloud_user`, so just press  `y`  at the prompt.

Verify that there is a file called  `fstab.asc`  in the  `gfreeman`  home directory (by running  `ls`). Create a new email to  `cloud_user`  and attach this file:

`[gfreeman@host]$ mail -s "looks good" -a fstab.asc cloud_user@localhost Can you decrypt this? .`

Log out of Mr. Freeman's account:

`[gfreeman@host]$ exit`

###  Decrypt the Attached File

Now, as  `cloud_user`, open up the  `mutt`  email client and save the  `fstab.asc`  attachment from the new email.

Decrypt the saved  `fstab.asc`  file with the  `gpg`  command, and enter the passphrase for  `cloud_user`'s key when prompted:

`[cloud_user@host]$ gpg fstab.asc`

Now let's verify that we can read the contents of the decrypted file:

`[cloud_user@host]$ cat fstab`

## Conclusion

Being able to encrypt and decrypt files that you share with others will come in handy. We've got the process down now, and this will help down the road. Congratulations!
