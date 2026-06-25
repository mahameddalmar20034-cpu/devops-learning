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
Goal 




 
