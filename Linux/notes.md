# Linux

## File system commands list

### Viewing Files
`head -n 5 README.md` - This shows the first 5 lines of the README.md file
`tail -n 5 README.md` - This shows the last 5 lines of the README.md file
### Moving Files
`mv Networking/README.md Linux/README.md` - Used to move files in this case as well as renamnig files
`touch notes.md` - creates a file named notes.md
`rm -r Linux/` -  usually deletes a file with the -r option it deletes the directory and everything within it

## Script for changing ownership and permissions

 `#!/bin/bash`     
**This makes it executable**
`chmod +x Day1.txt`
**This executes the file**
`./Day1.txt`
**This changers the ownership to a new group**
`sudo chown :netdev Day1.txt`
**This lists the file with all of its permissions and details** `
`ls -l Day1.txt`  


## Process Management
`ps aux`- used to state the processes being used and the PID numbers and more
`ps aux | grep ping`- show the specific details for that process
`kill <PID>` - ends the process
`&`- used to run the process in the back so the terminal is free for use


## Text processing 

- The following command is used in the task to parse /etc/passwd to list all users with /bin/bash as their shell.

`cat /etc/passwd | grep /bin/bash | awk -F: '{print $1}'`
the option -F is used as it tells awk that the column seperate is a colon rather than the standard space.


# OverTheWire Bandit game
 ## Level 0
 **Challenge**
SSH into the server
**Solution**
`ssh -p 2220  bandit0@bandit.labs.overthewire.org`
**Explanation**
Since the main port is blocked using the  -p option specifies the port that is open and hence can sshed into.
**What I learned**
When SSHing into a remote server sometimes it is ran on on a different port rather than the usual port 22.By using the -p option it allows you to tactically specify which port to enter.



Level 0 -> Level 1
**Challenge**
Find the password for the next level in a readme file
**Solution**
`cat README`
**Password**
6y2kwnwK6grgvwvpvLaa2T1cpFEKOhNR
**Explanation**
The  README file contains the password .The command was used to reveal its contents.
**What I learned**
`cat` is a good command for dealing with content within files


Level 1-> Level 2
**Challenge:**
The password is stored in a file called "-"
**Solution:**
`cat ./-`
**Explanation**
The command doesnt recognise the "-" alone so by writing its parent directory alongside it. Where "." is the directory we are in followed by "/-" the terminal recognises what file is being discussed and so when combining this with cat reveals its content.
**What I Learned**
Using "./" before a strange name of a file allows the terminal to determine what you are talking about in the case of confusion
**Password**
PK8fYLZg2hnHSz83plBL1iEPKdD3QToB


Level 2-> Level 3
**Challenge**
The password for the next level is stored in a file called --spaces in this filename-- located in the home directory
**Solution**
cat ./"--spaces in this filename--"
**Explanation**
The weird syntax meant the cat command didnt recognise the unique name so by combining "./" to show it is a file combine with speech marks to take into account that the spaces in the name is part of it and not seperate.
**What I learned**
By using "./" to specify it is file in a diretory aswell as speech marks to highlight where the name begins and ends you can overcome the commands confusion.
**Password**
7ZZ2LFrykP2zEyvBl4m3clcL7tGYJPME

Level 3-> Level 4
**Challenge**
The password for the next level is stored in a hidden file in the inhere directory.
**Solution**
ls -a
cat "...Hiding-From-You"
**Explanation**
The file is hidden using the `-a` option reveals hidden files when running the `ls` command.The speech marks and then used due to the weird syntax of the name to ensure clarification to the terminal.
**What I learned**
There are sometimes hidden files with a directory that isnt visible normally.
**Password**
xzTXq1rDJQVVAzdv5cHq1TQytTWufAMq

Level 4 -> Level 5
**Challenge**
The password for the next level is stored in the only human-readable file in the inhere directory. Tip: if your terminal is messed up, try the “reset” command.
**Solution**
`file ./*`
`cat ./"-file07"`
**Explanation**
The only human readable file uses ascii text.To identify this the command `file` which checks the type of file combined with the globus checks all of the files in the directory.
**What I learned**
The command file can show you what type of file it is.Globus `*` can be used as a shortcut to check all files simultaneously.
**Password**
6C7h9GD8M6ai5nr7wo1RonrzFjj9yIrG

Level 5-> Level 6
**Challenge**
The password for the next level is stored in a file somewhere under the inhere directory and has all of the following properties.
**Solution**
find . -type f -size 1033c ! -executable  -exec file {} \; | grep text
**Explanation**
So a long find command with many options was used to  pinpoint that exact file.`-type f` filters for the file, `-size 1033` filters for those that are 1033 bytes in size, `!` means not so here it means not executable.The last part of the command uses execute the file command to find the types of file that have survived the options so far. `{}` is where the file name is subsituted. `\ ` is used to end the command and the semi colon is used to clarify that to the kernel that the line has ended.This is all piped for the output to only show the ones that have text.
**What I have learned**
You can chain options to narrow down and find what you need depending on their characteristics.Piping can be used to filter for what you exactly need.`-exec <command> {} \;` is used to depending on what is found to execute another command.
**Password**
pXa26xhMWaC2SvDotA4r9EgZkulOeSBW

Level 6-> Level 7
**Challenge**
The password for the next level is stored somewhere on the server and has all of the following properties
**Solution**
find / -type f -user bandit7 -group bandit6 -size 33c 2&>/dev/null
**Explanation**
Using the find command to filter down to the exact group permissions.The last part redirects all errors only leaving those succesful outputs.
**What I have Learned**
Redirecting errors is handy for filtering down to take only what you need
**Password**
Bmnnvf82KzQlfxgAI2d1zYbr1u9pr3E3

Level 7 -> Level 8
**Challenge**
The password for the next level is stored in the file data.txt next to the word millionth
**Solution**
grep Millonth data.txt
**Explanation**
The grep command allows you to find a specific word and outputs the line it is in
**What I have learned**
Grep can be used to locate certain specific words in a file
**Password**
VR1ljMayciFxbnUokuQmJFw6QC9VKtub


Level 8->Level 9
**Challenge**
The password for the next level is stored in the file data.txt and is the only line of text that occurs only once
**Solution**
sort data.txt | uniq -u
**Explanation**
So `sort` puts all of the lines in order this is paired with `uniq -u` which removes any lines that repeat more than once.
**What I have learned**
You must pair them together starting with sort so that uniq can see which lines repeat otherwise it just sees them as not repeating but rather different patterns.
**Password**
EjmOSvuAu7sGAHqHVcBDPirRe9T03kxl


Level 9->Level 10
**Challenge**
The password for the next level is stored in the file data.txt in one of the few human-readable strings, preceded by several ‘=’ characters.
**Solution**
strings data.txt | grep =
**Explanation**
The `strings` command outputs only human readable files.This is piped into the grep command extracting the line with the "=" which was next to the password.
**What I have learned**
Strings can be used to extract human readable files.
**Password**
B0s2khmbT9u0geKuOoVGW3JZKhndE3BG

Level 10-> Level 11
**Challenge**























 
