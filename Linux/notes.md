# Linux

## File system commands list

### Viewing Files
`head -n 5 README.md` - This shows the first 5 lines of the README.md file
`tail -n 5 README.md` - This shows the last 5 lines of the README.md file
### Moving Files
`mv Networking/README.md Linux/README.md` - Used to move files in this case as well as renaming files
`touch notes.md` - creates a file named notes.md
`rm -r Linux/` -  usually deletes a file with the `-r` option it deletes the directory and everything within it

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
The password for the next level is stored in the file data.txt, which contains base64 encoded data
**Solution**
base64 -d data.txt
**Explanation**
The `-d` option in `base64` decodes the password.
**What I have learned**
Encoding and decoding can be used to hide important data.
**Password**
pYfOY6HwUsDj5rL9UvyhU7MCmv8vN5Ro

Level 11 -> Level 12
**Challenge**
The password for the next level is stored in the file data.txt, where all lowercase (a-z) and uppercase (A-Z) letters have been rotated by 13 positions
**Solution**
cat data.txt |    tr 'A-Za-z' 'N-ZA-Mn-za-m'
**Explanation**
The command of cat is used since tr doesnt output the files data.  `tr` is used to shift the words down 13 positions to decode the password.
**What I have learned**
The order and letter you begin with matters as beginning with A here would get you the wrong output.
**Password**
GROozWPO8QyN0mGrjUkID0WCYkZiQxrN




Level 12 -> Level 13
**Challenge**
The password for the next level is stored in the file data.txt, which is a hexdump of a file that has been repeatedly compressed.
**Solution**
`mktemp -d`
`xxd -r`
`/tmp/tmp.0n9nXcwFlq`
`mv data6.bin data6.gz`
`gunzip data6.gz`
mv `Stage1 stage1.bz2`
`bunzip2 staeg1.bz2`
`tar -xvf stage1`
**Explanation**
First a temporary directory is made to create files.First it was hexdumped so it needed to be converted into readable form.Then there was multiple layers of bzip, gzip and tar archive files that needed to be unzipped.
**What I have learned**
Files can be archived and zipped behind multiple layers for storage.
**Password**
qQYQiHOBPR8zR61qxYqX45quvihF2uzk

Level 13 -> Level 14
**Challenge**
The password for the next level is stored in /etc/bandit_pass/bandit14 and can only be read by user bandit14.
**Solution**
`scp -P 2220 bandit13@bandit.labs.overthewire.org:sshkey.private .`
chmod 400 sshkey.private
`ssh -p 2220 -i sshkey.private bandit14@bandit.labs.overthewire.org`
**Explanation**
The ssh key was given but it could be only used to access the level from outside the server from my local machine.`scp` is the ssh of copying.It was used to copy the key to my local machine.They keys permissions were changed to 400 to satisfy ssh.Then this key was used with the `i` option which allows for private keys to access the next level.
**What I learned**
You can copy keys or information from a server with sshing in fully.SSH key will throw away and not use a key that is too open in which it is too acessible so make sure to check permissions on the keys.
**Password**
aaWecNkG4FhxJQxz07uiwzVP6bJiYS65


Level 14-> Level 15
**Challenge**
The password for the next level can be retrieved by submitting the password of the current level to port 30000 on localhost.
**Solution**
`cd etc/`
`ls | grep bandit14`
`nc localhost 3000`
**Explanation**
First the password for level 14 is optained from the etc directory.Then instructions are given to submit the password to localhost.The `nc` command is then used and the password is submitted giving the password to next level.
**What I have learned**
Sumitting a password to a server means that a command is needed to send data to a server.A common tool used is net cat .When connected you can send whatever.The data was submitted and whatever was listening on the port recognised the correct handshake and returned data 
.**Password**
pbLYuZtTg4MgaqfJx8jbA9gKKGqM68A7

Level 15-> Level 16
**Challenge**
The password for the next level can be retrieved by submitting the password of the current level to port 30001 on localhost using SSL/TLS encryption.
**Solution**
`openssl s_client -connect localhost:30001`
**Explanation**
The command for SSL/TLS encryption  is `openssl` and as the client making the connection we use `s_client`.The option of `-connwct` is used to input the host and the port in order to conenect.The password is then submitted and the server listening on the port sends back the password.
**What I have learned**
Commands can have subcommands tailored to the need at hand.There is always a service listening on the port on the server so when you connect to the port on the server the service is waitiing for a specific handshake to hand over the specific data.
**Password**
kS0Hf0u5HiXFwKMKFqXvPdOTNGGa0X8V

Level 16 -> Level 17
**Challenge** 
The credentials for the next level can be retrieved by submitting the password of the current level to a port on localhost in the range 31000 to 32000. First find out which of these ports have a server listening on them. Then find out which of those speak SSL/TLS and which don’t. There is only 1 server that will give the next credentials, the others will simply send back to you whatever you send to it.
**Solution**
`nmap -p 31000-32000 -sV localhost`
`openssl s_client -connect localhost:31790 -quiet`
`vim sshkey`
`chmod400 sshkey`
`ssh -p 2220 -i sshkey bandit17@bandit.labs.overthewire.org`
**Explanation**
First nmap with the option `p` to specify the ports and `-sV` are to use to see their service and version.This displayed the active ports and which ones usse ssl.Those with echo would simply just print back whatever was sent.It was the sshed into using `openssl s_client` however whenever placing the password it read the first letter as something else so errors occurred.The option `-quiet` overrides this error giving the sshkey.The sshkey is then copied to the local machine  permissions are changed to make it useable for ssh and used to enter the next level.
**What I have learned**
The option `-quiet` can be used to overrun errors and mistakes.Sometimes you need to literally copy the sshkey and place it in a file to use it.It will not always be handled to you.
**Password**
pWXMAZoxGC8JmDMfmT5MGEsobMM3vnj2

Level 17->Level 18
**Challenge**
There are 2 files in the homedirectory: passwords.old and passwords.new. The password for the next level is in passwords.new and is the only line that has been changed between passwords.old and passwords.new
**Solution**
`diff passwords.new passwords.old`
**Explanation**
The `diff` command is used to compare each file line by line and output the different lines.The first different output was the new password hence the answer.
**What I have learned**
The diff command can be used to compare files.It shows you the co-ordinates too so the location can be found.
**Password**
OQxXZjELndr90zuhOTDYBEomI0SZITXI


Level 18->Level 19
**Challenge**
The password for the next level is stored in a file readme in the homedirectory. Unfortunately, someone has modified .bashrc to log you out when you log in with SSH.
**Solution**
ssh -p 2220 bandit18@bandit.labs.overthewire.org  cat readme
**Explanation**
ssh allows you to run a command as soon as you enter to only run and command without entering the server. This helps overcome waiting for the interactive shell to load.This bypasses .bashrc which is used to set up the interactive shell which in this case is coded to also log you out.
**What I have learned**
You can run a command alongside ssh without the interactive shell loading but it only runs a command and doesnt fully ssh you in.
**Password**
KpsOfPkcP7i1FlIExk2QEjyt6dw8dxZI

Level 19->Level 20
**Challenge**
To gain access to the next level, you should use the setuid binary in the homedirectory. Execute it without arguments to find out how to use it. The password for this level can be found in the usual place (/etc/bandit_pass), after you have used the setuid binary.
**Solution**
`./bandit20-do cat /etc/bandit_pass/bandit20`
**Explanation**
Running on ls-l I saw that the owner had setuid permissions and I had the ability "x" to execute the file.What this setuid binary permission does is give lower privellaged users the ability to use the owners permisson to complete privalleged tasks.This ends after running the file and the returns the user back to their original permissions.This was used to access the next level password using bandit20's permissions.
**What I have learned**
You can use setuid binary as an ability to access more privilaged users permissions and execute tasks the user wouldn't normally be able to.

**Password**
4pIjcunZ0fK2vmp3IwfG8Vf7VhxD6pOA










































 
