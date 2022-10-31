# Modify a Text File Using  `sed`

## Scenario
You are working at a firm that is collecting information about ancient Greece that will be published in a new book.

A member of your team has contributed a text file that contains the fable of the "The Ants and the Grasshopper." However, the text is incorrect as all of the instances of the word 'ants' has been replaced with the word 'cows'.

You will need to modify this file using a sed command so that the file will have the correct text. All instances of the word 'cows', regardless of case, needs to be replaced with the word 'ants'.

Once you have accomplished this task, leave the file on the system so that your editor can review your work.

NOTE: You only need to ignore case sensitivity on the input, not match case on the output.

## Objectives


### Use `sed` to Change a Word in the File

The word 'cows' needs to be replaced with the word 'Ants' in the  `fable.txt`  file.

This can be done with the following command:

`sed -i 's/cows/Ants/Ig' fable.txt`

### There Should Be No Other File in the Home Directory

There should be no other file in the home directory. The  `sed`  command must be run "in place," and no other temporary file should be used.

## Introduction

Someone got confused and wrote about cows instead of ants in a text file. We've got to replace all instances of _cows_ and with _Ants_, regardless of whether or not _cows_ contains any capital letters.

## Solution
### The File

Let's look at the file we're dealing with.

`cat fable.txt`

### The Fix

We're going to run a  `sed`  command. The -i means "do this in place," as in don't create another file. The capital  `I`  near the end stands for "case-insensitive" and means that whether  _cows_  has any capital letters in it or not, change it to  _Ants_. The  `g`  means do it globally, throughout the whole file. Here is the complete command:

`sed -i 's/cows/Ants/Ig' fable.txt`

Now if we run our  `cat`  command again, we'll see that all the cows are gone.

## Conclusion

The  `sed`  command is very handy. Congratulations on getting a bit more familiar with it.
