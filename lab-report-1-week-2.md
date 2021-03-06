# **Lab Report 1 Week 2**

## Step 1: Install Visual Studio Code (Skip if Already Installed)
If you have VSCode already installed then open VSCode and have it ready.
![Starter](VSCodeStarterPage.png)
If not then go to [https://code.visualstudio.com/]( https://code.visualstudio.com/) to download the code.
![VSCodeWebsite](VSCodeWebsite.png)

On that website, make sure to choose the download that is appropriate for your operating system.
![OperatingSystems](OperatingSystems.png)

From there, follow the instructions of the VSCodeUserSetup and open VSCode when done.

## Step 2: Connecting Remotely

Go to Settings, then go to Apps, then go to Apps & Feautues, and click on Optional Features. 
![Settings](Settings.png)
Click "Add a feature" and search for "OpenSSH Client" and "OpenSSH Server" and install them. 
![OpenSSHSearch](OpenSSHSearch.png)

Go to [https://sdacs.ucsd.edu/~icc/index.php](https://sdacs.ucsd.edu/~icc/index.php) to access your course specific account.
![accountLink.png](accountLink.png)

Go to VSCode and enter `ssh cs15lwi22aec@ieng6.ucsd.edu` into your terminal but remember to switch out the `aec` with your course specific account and enter the password, and answer `yes` if prompted.
![TerminalSSH](TerminalSSH.png)


## Step 3: Trying Some Commands
You are now connected to the remote computer and can now try out some commands. Some useful commands to know are `ls` which will show the files and folders in the directory, `cd` which will change the directory to the given directory, `pwd` which will print the path of the working directory, and `mkdir` which will make a directory with the given name,.
![multiCommands.png](multiCommands.png)
![mkDir.png](mkDir.png)

## Step 4: Moving Files with scp
`scp` is a command that will copy a file or folder from your computer to the remote computer. Create a java file to be copied with the following code.
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
The scp command needs to be given the name of the folder or file(`WhereAmI.java`) to be copied and the location(`cs15lwi22aec@ieng6.ucsd.edu:~/` but replace `aec` with your account). 
![scpWhereAmI](scpWhereAmI.png)
After this, you can see that it has been copied correctly by doing the ls command and running the code.
![runWhereAmI](runWhereAmI.png)

## Step 5: Setting a SSH Key (Windows)
Enter `ssh-keygen` into the terminal and then `C:\Users\jwong/.ssh/id_rsa`(switch jwong with your own) and keep pressing enter until the square appears.
![square](square.png) 

Next open Windows PowerShell as administrator and type in these commands.
```
Get-Service ssh-agent | Set-Service -StartupType Manual
Start-Service ssh-agent
Get-Service ssh-agent
ssh-add C:\Users\jwong/.ssh/id_rsa
```
Then enter these commands. 
```
ssh cs15lwi22aec@ieng6.ucsd.edu mkdir .ssh
scp C:\Users\jwong/.ssh/id_rsa.pub cs15lwi22aec@ieng6.ucsd.edu:~/.ssh/authorized_keys
```
(I entered the last two commands in Windows Powershell but they can be entered in VSCode)
![correctPowerShell](correctPowerShell.png)
Now you should be able to enter into your account without needing to type in a password.


## Step 6: Optimizing Remote Running
Running code on the same line can make remote running more efficient. For example, `ssh cs15lwi22aec@ieng6.ucsd.edu "ls"` will log into the account and run `ls` over there and then exit.
![sameLine1](sameLine1.png)
Typing `cp WhereAmI.java OtherMain.java; javac OtherMain.java; java WhereAmI` will copy WhereAmI.java to a new OtherMain.java file, compile OtherMain, and then run WhereAmI.
![Done](Done.png)
Using the up arrow, you can redo the last command.

KeyStrokes With No Techniques: 70

KeyStrokes With Up Arrow: 3 









