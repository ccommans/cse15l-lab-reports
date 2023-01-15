# Remote Access Tutorial

Signing in to the *@ieng6* servers remotely is a tricky process involving password changes and seemingly complex terminal commands.
However, following these steps will make the process much easier.

## I. Your Remote Account
In order to login to the server, you first need the class-specifice credentials for your account, which can found [here](https://sdacs.ucsd.edu/~icc/index.php) after entering your username and PID:

![pic]()

This is your account username; you must also change the password with the link on screen ([also here](https://sdacs.ucsd.edu/~icc/password.php)). Make sure to select "No" for "Change MyTritonLink password?" and "Yes" for "Change course-specific account passwords?":

![pic]()

>Note 1: Here are the password requirements
> * 12-30 characters
> * Use a mix of uppercase, lowercase, numbers, and special characters.
> * Do not use any part of your name or username.
> * Do not use alphabet, number, or keyboard sequences.

>Note 2: I've previously had trouble logging in with my password if the special character is an asterisk (\*), so try to use some other character like @ or !

## II. Accessing the Terminal
Visual Studio Code is an IDE that we can use to access the terminal and can be downloaded [here](https://code.visualstudio.com/). Once downloaded and installed, a terminal window can be opened with Terminal -> New Terminal seen below (or via the shortcut Ctrl+Shift+\`):

![pic]()

## III. Logging on
With now the terminal window open and password reset, you can finally access the remote server. Type (or copy) the command:

`ssh cs15lwi23ABC@ieng6.ucsd.edu`

with "ABC" being replaced by your specific username. Immediately the window will say:

`The authenticity of host 'ieng6.ucsd.edu (128.54.70.227)' can't be established. RSA key fingerprint is SHA256:ksruYwhnYH+sySHnHAtLUHngrPEyZTDl/1x99wUQcec. Are you sure you want to continue connecting (yes/no/[fingerprint])? `

This message appears only the first time you remotely connect, so type `yes` and hit enter. You now can enter your account's password to login.

>Note: No characters on the terminal will appear when inputting your password. They are still being inputted however, and hitting enter will verify it. If  `Password:` immediately appears again, that means the password failed and you must re-enter it.

This is what a successful login looks like:

![pic]()

Congratulations! You are now logged in on the remote server.

## A: Running Commands
Here are some useful commands:
* `pwd`             prints working directory
* `cat [filename]`  will print out the file's content
* `cd [dir]`        changes working directory to new one
* `ls`              lists files in working directory
* `cp [dir1][dir2]` copies content of first directory into second
* `clear`           clears the terminal window
* `exit`            logs out of the remote server

Here are some of the above commands being used:

![pic]()
