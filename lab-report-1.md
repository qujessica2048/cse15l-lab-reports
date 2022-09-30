# week 1 lab report!

This is a guide on how to log into a course-specific account on ieng6! 

For context, the actual account for remote access starting with cs15lfa22 was not working, so a personal account with TritonLink credentials was used instead.

This procedure was also done on a Windows computer, so there are a couple extra steps marked with * that can be ignored if done on a non-Windows device.

---
&nbsp;

## 1. Installing VSCode
&ensp; 1.1 &ensp; Navigate to [VSCode website](https://code.visualstudio.com/) and download

![Image](res\lab1\installVS.png)

&ensp; 1.2 &ensp; If done correctly, the app should open and show a blank-ish home screen that shows possible commands

&nbsp;

## 2. Remotely Connecting
&ensp; 2.1 &ensp; Find course-specific account name for classes on the [UCSD database](https://sdacs.ucsd.edu/~icc/index.php)

![Image](res\lab1\accountLookup.png)

&ensp; 2.2 &ensp; Click the Global Password Change Request hyperlink

&ensp; 2.3 &ensp; Fill out the current and new password (the current password, if it hasn't been changed before, should be the TritonLink password). Select **No** for the option of changing TritonLink password, and **Yes** for the option of changing course-specific account password.

***Note:*** If possible, change the password well before you need to use it, since time is required for it to process!

&ensp; 2.4* &ensp; [Install OpenSSH](https://docs.microsoft.com/en-us/windows-server/administration/openssh/openssh_install_firstuse), a program that allows your computer to connect to other computers remotely. 

&ensp; 2.5 &ensp; Open a new terminal in VSCode and type in the command below, replacing the part before the @ with the account name found in Step 2.1.

```
$ ssh cs15lfa22mb@ieng6.ucsd.edu
```

&ensp; 2.6 &ensp; When asked if you want to continue connecting, select **yes**, and then enter the password that was set in Step 2.3.

***Note:*** If the password was recently changed and the account was signed in unsccessfully, try repeating Steps 2.5-2.6 with the account name ```[insert TritonLink username]@ieng6.ucsd.edu``` and the same password as TritonLink.

&ensp; 2.7 &ensp; The terminal should now look like this:

![Image](res\lab1\connected.png)

&nbsp;

## 3. Trying Some Commands

``` 
# Command Bank (there are more out there, these are some)
cd <directory>          | change directory to <directory>
cd                      | move to parent directory
ls                      | list files in directory
mkdir <directory>       | create new directory called <directory>
cat <file>              | print contents of <file>
cp <file> <directory>   | copy <file> to <directory>
```

&ensp; 3.1 &ensp; Run some commands to try things out on both the home computer and remotely accessed computer!

***Example:*** Running ```ls``` on the home computer returned this, 
&nbsp;

![Image](res\lab1\homeCommandEx.png)

while running it on the remote computer returned this:
&nbsp;

![Image](res\lab1\remoteCommandEx.png)

&nbsp;

## 4. Moving Files with ```scp```
Since we are now able to run commands both locally and remotely, let's try copying a file to the remote computer from the local one!

``` 
scp <file> <user>@<host>:/remote/path
```

&ensp; 4.1 &ensp; Create a file on the home computer called ```WhereAmI.java``` and copy the following into it:
```
class WhereAmI {
  public static void main(String[] args) {
    System.out.println(System.getProperty("os.name"));
    System.out.println(System.getProperty("user.name"));
    System.out.println(System.getProperty("user.home"));
    System.out.println(System.getProperty("user.dir"));
  }
}
```

&ensp; 4.2 &ensp; Compile and run the program using the following commands:

```
# Compile
javac WhereAmI.java
# Run
java WhereAmI
```

&ensp; 4.3 &ensp; Use ```scp``` to copy WhereAmI.java to the remote computer:

```
scp WhereAmI.java cs15lfa22mb@ieng6.ucsd.edu:~/
```

&ensp; 4.4 &ensp; Connect back to the remote computer by using ```ssh``` as shown in Steps 2.5-2.6 and use the command ```ls``` to show all files, which should show the ```WhereAmI``` program:

&ensp; 4.5 &ensp; Repeat Step 4.2 to run the program on the remote computer, which should result in something like this:

![Image](res\lab1\remoteRun.png)


&nbsp;

## 5. Setting an SSH Key
Now that everything works, there are ways to make things easier by taking out the login step.

&ensp; 5.1 &ensp; Use the command ```ssh-keygen``` to generate a pair of private and public keys, where the private keys remain on the home computer and the public keys are stored remotely.

&ensp; 5.2 &ensp; When prompted for the file path, password, and password confirmation, hit enter.

&ensp; 5.3* &ensp; Windows computers require the extra step of an ```ssh-add``` command as follows:

```
# By default the ssh-agent service is disabled. Configure it to start automatically.
# Make sure you're running as an Administrator.
Get-Service ssh-agent | Set-Service -StartupType Automatic

# Start the service
Start-Service ssh-agent

# This should return a status of Running
Get-Service ssh-agent

# Now load your key files into ssh-agent
ssh-add $env:USERPROFILE\.ssh\id_ed25519
```

&ensp; 5.4 &ensp; There should now be the private key saved in a file called ```id_rsa``` and the public key saved in a file called ```id_rsa.pub```. Sign into the remote computer with ```ssh``` and enter password as prompted.

&ensp; 5.5 &ensp; Using the command below, create a new directory called ```.ssh``` and 
```
mkdir .ssh
```

&ensp; 5.6 &ensp; Copy the public keys file ```id_rsa.pub``` to the remotely accessed computer using ```scp``` and logout of the remote computer using ```exit```.
```
scp /Users/[your home username]/.ssh/id_rsa.pub [your course-specific username]@ieng6.ucsd.edu:~/.ssh/authorized_keys

exit
```

&ensp; 5.7 &ensp; To test the keys, use ```ssh``` to sign into the remote computer again, and this time, it should not prompt for a password like so:

![Image](res\lab1\sshKeys.png)

&nbsp;

## 6. Optimizing Remote Running

- Running commands with quotes at the end of an ```ssh``` command runs it on the remote server and then exits:
```ssh cs15lfa22mb@ieng6.ucsd.edu "ls"```
![Image](res\lab1\shortcut1.png)

- Using the up arrow will copy the last command run!
