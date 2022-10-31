# Creating and Modifying a File with Vim

## Scenario

Knowing how to modify files at the command line is an essential skill for any Linux administrator. This learning activity will focus on using the Vim text editor to practice creating a new file, adding text to the file, and then modifying that text. We will also practice some of the basic keyboard shortcuts to change the text of this file.

## Additional Resources

Keep the Vim cheat sheet that is available with the LPIC-1 Exam 101 course on hand if you need to quickly look up some keyboard shortcuts. ( Note: to write and quit vi/vim you use the :wq )

You are preparing a system report for your audit department. Your report should contain the following characteristics:

-   Create a file in  _/home/cloud_user_  called  _notes.txt_  to contain the information for submitting.
-   At the top of the new file, add the text 'Beginning of Notes File' followed by two blank lines, save and close the file.
-   Add the information from the  _/etc/redhat-release_  file, appending it to  _notes.txt_.
-   Edit that new information, removing the '(Core)' value at the end of the line, and add two more blank lines right after. Then save and close the file.
-   Next, capture the free memory on your system and append that information to  _notes.txt_.
-   Edit that new information: delete the entire line beginning with 'swap', and then add two blank lines under it.
-   Before saving, place your cursor on the 3rd line of the file on your screen, add the text 'This is a practice system', add a blank line right under it, then save and close the file.
-   Finally, append the output of the  `dbus-uuidgen --get`  to  _notes.txt_.
-   Edit that new information, and at the beginning of the UUID line, place 'Dbus ID = '. Then save and close the file.

Once you verify the file contains everything instructed, you can turn it over to your team for audit.

## Objectives

### Create a new file

Using the vim text editor, create a new file called  _notes.txt_  in the cloud_user home directory. Enter the text "Beginning of Notes File" at the top of the document. Leave two blank lines under this top line. Save and close the file.

The process is:

`vi notes.txt i (insert) Text - Beginning of Notes File (2 blank lines) :wq!`

### Send Data to the notes.txt file

Using the  `cat`  command and output redirection, send the contents of the  _/etc/redhat-release_  file to the end of the  _notes.txt_  file, taking care to append the contents so as to not overwrite the file.

This can be accomplished via:

`cat /etc/redhat-release >> notes.txt`

### Modify the notes.txt File

Open the  _notes.txt_  file for editing again. Place the cursor before the openening parentheses around the word "Core." Using a keyboard shortcut, delete the text from the cursor position to the end of the line. Leave two blank lines under this line. Save and close the file.

The following process will meet the criteria:

`vim notes.txt (cursor to 'core') SHIFT D (or d$) remove cursor to end of line o - blank line enter (2nd line) :wq!`

### Send More Data to the File, and Modify Its Contents

Using the  `free -m`  command and output redirection, send the output of the command to the end of the  _notes.txt_  file, taking care to append the contents so as to not overwrite the file.

Open  _notes.txt_  for editing. Move the cursor to the line that begins with "Swap." Using a keyboard shortcut, delete this entire line. Leave two blank lines after the line that begins with "Mem".

Follow this process:

`free -m >> notes.txt vim notes.txt move cursor to Swap line dd (delete line) o - blank line enter (2nd) SHIFT: 3 (3rd line of file) i - insert enter (blank line) :wq!`

### Enter New Text into the File

Using a keyboard shortcut, jump to line 3 of the file, then enter the text: "This is a practice system." Leave a blank line after this text has been entered. Save and close the file.

You can accomplish this via:

`vim notes.txt SHIFT: 3 (moves to 3rd line) i (insert) This is a practice system (enter for blank line) :wq!`

### Finalize the Notes File

Using the  `dbus-uuidgen --get`  command, send the output of this command (which will retrieve the system's dbus unique ID) to the end of the  _notes.txt_  file. Take care to append the contents so as to not overwrite the file. Open  _notes.txt_  in vim, and use a keyboard shortcut to jump to the end of the file. At the beginning of the line that contains the dbus ID, enter in the following text: "Dbus ID = " so that there is a space between the equal sign and the Dbus ID number. Save and close the file. Hand the system over for grading.

`dbus-uuidgen --get >> notes.txt vim notes.txt SHIFT G (end of file) i - insert Dbus ID = (before ID) :wq!`


## Solution
### Create a New File

We're going to create a new file called  `notes.txt`  in  `/home/cloud_user`.

`cd vim notes.txt`

Now, to add the text  _Beginning of Notes File_, we need to get into  _insert_  mode, by pressing  `i`. We can start typing now once we're in  _insert_  mode.

Leave two blank lines after  _Beginning of Notes File_. Now, to save the file and quit Vim, we have to first hit  **Esc**  (to get out of  _insert_  mode), type  `:wq!`  (write and quit).

### Send Data to  `notes.txt`

Using the  `cat`  command and output redirection, send the contents of the  `/etc/redhat-release`  file to the end of the  _notes.txt_  file, taking care to append the contents so as to not overwrite the file (using  `>>`, not  `>`)

Run this to append  `notes.txt`  with the contents of  `/etc/redhat-release`:

`cat /etc/redhat-release >> notes.txt`

### Modify  `notes.txt`

Let's open  `notes.txt`  again for editing. We'll place the cursor before the opening parenthesis around the word  _Core_  and use a keyboard shortcut to delete the text from there to the end of the line. We'll leave two more blank lines at the end of the file and then save and quit again.

Here are all of the steps to do that:

1.  Open the file:
    -   `vim notes.txt`
2.  Use the arrow keys to move to the beginning parentheses before Core
3.  Remove text from the cursor's position to end of line:
    -   `SHIFT D`  (or  `d$`)
4.  Create a blank line under where the cursor is
    -   `o`
5.  Hit  **Enter**  to create the second blank line
6.  Hit  **Esc**  to leave insert mode
    -   Hitting  `o`  added a blank line, but also put us in insert mode
7.  Write and quit:
    -   `:wq!`

### Send More Data to the File, and Modify Its Contents

Now we're going to send  `free -m`  output to the end of  `notes.txt`, edit  `notes.txt`  again, delete the last line of the file, and add two more blank lines to the end of the file.

Then, we're going to jump to the third line of the file, enter some text, and make another blank line afterward.

Here are all of the steps to do that:

1.  Append the  `notes.txt`:
    -   `free -m >> notes.txt`
2.  Edit  `notes.txt`:
    -   `vim notes.txt`
3.  Navigate to the  _Swap_  line with arrow keys.
4.  Delete the line:
    -   `dd`
5.  Create a blank line under where the cursor is (and put us in insert mode):
    -   `o`
6.  Hit  **Enter**  to create the second blank line.
7.  Hit  **Esc**  to get out of insert mode.
8.  Get to the 3rd line of file:
    -   `:3`
9.  Get back into insert mode:
    -   `i`
10.  Type  **This is a practice system**.
11.  Hit  **Enter**  to make another blank line.
12.  Hit  **Esc**  to leave insert mode.
13.  Write and quit:
    -   `:wq!`

### Finalize the Notes File

We're going to dump one last bit of text into the file, then edit it again. We'll take the output from  `dbus-uuidgen --get`, append it to  `notes.txt`  then edit  `notes.txt`  so that the text  _Dbus ID =_  is in the beginning of the new appended line.

We'll do it like this:

1.  Append the  `notes.txt`:
    -   `dbus-uuidgen --get >> notes.txt`
2.  Edit  `notes.txt`:
    -   `vim notes.txt`
3.  Get right to the end of the file:
    -   `G`  (Capital G)
4.  Get into insert mode:
    -   `i`
5.  Type "Dbus ID = " (with a space between the equals sign and the  `dbus-uuidgen --get`  command's output). Only type the text within the quotation marks.
6.  Write and quit:
    -   `:wq!`

## Conclusion

Done


