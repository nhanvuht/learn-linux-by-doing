
# Working with Compressed Files in Linux

There's a text file named  `junk.txt`  in our home directory. It's 133MB and full of random data. We're going to use a few different tools to compress this file, and we'll compare the size differences between each one.

## Objectives


### Try out different compression methods

Note: Please give the lab an extra minute or so before connecting via ssh to allow the lab to fully provision.

Take a look at the original size of your junk.txt file, and make note of it:

`ls -lh junk.txt`

First, let's try the gzip compression method. The following command will compress the junk.txt file using gzip:

`gzip junk.txt`

Now, run the 'ls' command to view the size of the file:

`ls -lh`

Notice that the gzip command replaced the original file with a compressed version of it. The other compression commands we will use will do the same. Take note of the smaller size of the file. Then, decompress the gzip file to get the original junk file back:

`gunzip junk.txt.gz`

Next, perform the same steps, using the bzip2 compression method:

`bzip2 junk.txt`

Note that this compression method will take slightly longer than the previous. Make a note of the bzip2 file's size (typically, these file sizes are smaller than gzip compressed files):

`ls -lh junk.txt.bz2`

Once again, decompress the file to get the original back:

`bunzip2 junk.txt.bz2`

Now we will try out a newer compression method, using 'xz':

`xz junk.txt`

Note that this compression will take some time as well. Once the command completes, view your file's size:

`ls -lh`

And finally, decompress the file:

`unxz junk.txt.xz`

### Create tar files using the different compression methods.

This next set of tasks will focus on working with tar files. First, use the gzip compression method to make a tarball:

`tar -cvzf gztar.tar.gz junk.txt`

Then, make a new tarball using bzip2:

`tar -cvjf bztar.tar.bz2 junk.txt`

Lastly, use xz to make a tarball:

`tar -cvJf xztar.tar.xz junk.txt`

Run the ls command again to compare the file sizes:

`ls -lh`

Notice that creating tar files did not replace the original junk.txt file. Note also how close in size the xz and bzip2 files are to each other.

### Practice reading compressed text files.

The final group of tasks will demonstrate how to read compressed files, without decompressing them on your disk. First, copy over the /etc/passwd file to your home directory:

`cp /etc/passwd .`

Now, compress the file using bzip2 into a tarball:

`tar -cvjf passwd.tar.bz2 passwd`

Use the bzcat command to read the bzip2 compressed file:

`bzcat passwd.tar.bz2`

Do the same for a gzipped tar file:

`tar -cvzf passwd.tar.gz passwd`

And use the zcat command to read this compressed file:

`zcat passwd.tar.gz`

And finally, create an xz tar file:

`tar -cvJf passwd.tar.xz passwd`

And use the xzcat command to read its contents:

`xzcat passwd.tar.xz`

Done

## Solution: Get the Original File Size

Let's take a look at the original size of  `junk.txt`  file and make note of it:

`[cloud_user@host]$ ls -lh junk.txt`

## Creating zip Files

### Gzip

First, let's try compressing with Gzip. The following command will compress  `junk.txt`  using  `gzip`:

`[cloud_user@host]$ gzip junk.txt`

Now, run  `ls`  to view the size of the file:

`[cloud_user@host]$ ls -lh`

Notice that the  `gzip`  command replaced the original file with a compressed version of it. The other compression commands we use will do the same. Take note of the smaller size of the file, and then decompress it to get the original back:

`[cloud_user@host]$ gunzip junk.txt.gz`

### bzip

Now we're going to perform the same steps, but using the bzip2 compression method instead:

`[cloud_user@host]$ bzip2 junk.txt`

Note this compression method will take slightly longer than the previous one. Let's check the resulting file size to see how it compared to using  `gzip`:

`[cloud_user@host]$ ls -lh junk.txt.bz2`

It should be smaller than  `junk.txt.gz`.

Once again, decompress the file to get the original back:

`[cloud_user@host]$ bunzip2 junk.txt.bz2`

### XZ

Now we will try out a newer compression method, XZ. It works with the same syntax as the others:

`[cloud_user@host]$ xz junk.txt`

Note that this compression will take some time as well. Once the command completes, view your file's size:

`[cloud_user@host]$ ls -lh`

The resulting file is about the same size as the last one. Now, like we did with the others, let's decompress the file:

`[cloud_user@host]$ unxz junk.txt.xz`

## Creating  `tar`  Files

Next, we'll focus on working with  `tar`  files. First, we're going to use  `Gzip`  to make a tarball:

`[cloud_user@host]$ tar -cvzf gztar.tar.gz junk.txt`

Then, let's make one using bzip2:

`[cloud_user@host]$ tar -cvjf bztar.tar.bz2 junk.txt`

Finally, we'll use XZ to make one:

`[cloud_user@host]$ tar -cvJf xztar.tar.xz junk.txt`

Run the  `ls`  command again to compare the file sizes:

`[cloud_user@host]$ ls -lh`

Notice that creating tar files did not replace the original  `junk.txt`  file. Note also how close in size the  `xz`  and  `bzip2`  files are to each other.

## Practice Reading Compressed Text Files

What if we want to read the contents of compressed files without having to actually decompress them? There is a way! Let's do that now. First, let's copy over the  `/etc/passwd`  file to your home directory:

`[cloud_user@host]$ cp /etc/passwd /home/cloud_user/`

### Gzip

We can do the same for a tar file, compressing it with Gzip:

`[cloud_user@host]$ tar -cvzf passwd.tar.gz passwd`

And we can use the  `zcat`  command to read this compressed file:

`[cloud_user@host]$ zcat passwd.tar.gz`

### bzip2

Now let's compress the file, using bzip2, into a tarball:

`[cloud_user@host]$ tar -cvjf passwd.tar.bz2 passwd`

We can use the  `bzcat`  command to read the compressed file:

`[cloud_user@host]$ bzcat passwd.tar.bz2`

### XZ

Finally, let's create an xz tar file:

`[cloud_user@host]$ tar -cvJf passwd.tar.xz passwd`

And we can use the  `xzcat`  command to read its contents:

`[cloud_user@host]$ xzcat passwd.tar.xz`

## Conclusion

You're all set. Congratulations on completing this lab!
