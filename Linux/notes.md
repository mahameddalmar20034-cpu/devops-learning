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
`chmod +x Day1.txt`   -This makes it executable
`./Day1.txt`         -This executes a file
`sudo chown :netdev Day1.txt` -This changers the ownership to a new group
`ls -l Day1.txt`    - This lists the file with all of its permissions and details `
 
