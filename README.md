# DevOps-BC
## ToC
- [Linux vs. Microsoft Filesystem](#os)  
- [CLI Commands](#cli)
- [Package Manager](#manager)
- [Vim Editor](#vim)
- [Linux Accounts & Groups - Users Management](#users)
- [Linux Accounts & Groups - Users Permission](#users-permission-2)
  - [Ownership](#lx-owner)
  - Permissions
    - [with Symbols](#lx-permission-sb)
    - [with octal numbers](#lx-permission-num) (preferred way)
- [Basic Linux Commands - Pipes & Redirects](#basic-commands)
- [Introduction to Shell Scripting](#sh-scripting)
  - [Variables](#sh-scripting-variables)
- [Environment Variables](#env-variables)
- [Networking](#networking)
- [SSH - Secure Shell](#ssh)
  - [Demo - Connect via SSH (Digital Ocean)](#ssh-demo)
- [Databases](#db)
  - [Databases](#db-types)
- [What are Build and Package Manager Tools?](#bpm-tools)
- [IaaS (Infrastructure as a Service)](#IaaS-tools)
- [Docker](#docker)




# Linux File System vs. Microsoft <a id="os"></a>
We have a hierarchical tree structure
We have `1 root folder`.
```
root/
├── bin/
├── etc/
├── opt/
└── var/
```

#### Compared in Windows.
We have `multiple root folders`.
```
C:\
├── Program Files\
├── Users\
├── Windows\
├── bin\
├── etc\
├── opt\
└── var\
```

## Linux Folders

### `/bin`
- executables for most essential user commands.
- available system-wide for all users

### `/sbin`
Are for 'system binaries'
- used for Administrators and for the system itself.
- These binaries need a superuser permission for execution.

### `/lib`
Hold the libraries for that executables from `/bin` or `/sbin`.

### `/usr`
Comes from the older times, where storage was important. Less important nowadays.
The `root /bin and /sbin` have less commands.  
Inside the /usr folder we have a `/local` folder.  
Third Party Applications **that WE install** on the computer, will be placed in here. -> `/usr/local/` like Java, Docker...  
- programs installed here, will be **available for all users on the computer**.  
- **If only we as the current user** want to have this program installed, we have to install it in the users `/home folder`.

### `/opt`
Programs in here, will be system-wide available for all users.  
There are some programs, that don't split their app into binaries and libraries.
Differences between `/opt` and `/usr/local`:
- `/usr/local` Programs, which split its components
- `/opt` Programs, which **NOT** split its components.  

### `/boot`
Contains files required for booting.
**We should not touch this folder**.

### `/etc`
Here we can `read and write`.  
Here is the system configuration stored and the main configuration location.  
Like Network, Linux user data, passwords, php config...

### `/dev`
Location of device files, like webcam, keyboard, hard drives etc.
- apps and drivers will access this, **NOT** the user.
- all files that the system needs to interact with the device.

### `/var`
Log files, cached data from applications.
- `/var/log` contains log files
- `/var/cache` contains cached data from application programs

### `/tmp`
Stores temp files for different applications.
### `/media` and `/mnt`
- /media where external media is mounted. Like Network Drive, CD, USB etc. They will also be referenced in the /dev folder.  
- /mnt for **manually** mounting file systems to operating system.  
### `hidden files (dotfiles)`
is primarily used to help prevent important data from being accidentally deleted.  
Are used to execute some scripts, store config etc.
- automatically generated py programs or operating system.
- File name **starts with a dot**
- in UNIX called "dotfiles"
- are usually stored in `/home folder`. for the current user.

---

# CLI Commands <a id="cli"></a>
### user and machine
```
name@name-ubuntu: ~$
```
- `name` is our logged-in user.
- `name-ubuntu` is our computer name.
- `~` current directory is home.
- `$` the dollar sign means "regular user"
- If we are logged in as a `root user` the dollar sign would be a hashtag instead `#`
## Basic Linux Commands
Everything in Linux is a file, if it is a document, pictures, directories, commands like pwd, ls etc.

#### Go to folders:
- root folder `/` (we should **not** change anything in here)
  - go to a specific folder `/$` and we can define an absolute path `cd /usr/local/bin`
- home folder `~`

### Flags
- `-r` does operation recursively
  - usage: 
    - file and folder deletion.
### Directory Operations:
- get current directory:
  - `pwd`
- list folders and files
  - `ls`
  - `ls -a` list all, incl. hidden files / folders.
- change directory
  - `cd [dir name]` example `cd Documents`
  - `cd ..` go up one level in the hierarchy.
- create folder
  - `mkdir [folder name]` example `mkdir python-project`
- remove folder
  - `rmdir [folder name]` example `rmdir python-project`
  - `rm -r [folder name]` to delete a **non-empty** folder with all its content.
  - `rm -d [folder name]` delete **empty directory**
- copy folder
  - `cp -r [original folder] [new folder]` example `cp -r java-app my-project` (To move the content with it, we need to add the -r flag.)
- rename folder
    - `mv [original name] [new name]` example `mv web-app java-app`
### File Operations:
- create file
  - `touch [filename]` example `touch main.py`
- remove file
  - `rm [filename]` example `rm main.py`
  - `rm -r [filename]` example `rm -r main.py`
- rename file
  - `mv [original name] [new name]` example `mv web-app java-app`
- copy file
  - `cp [filename] [new filename]` example `cp Readme.md NewReadme.md`
- display hidden files
  - `ls -a` show all files and folders including hidden ones.
- display content from a file
  - `cat [filename]` stands for concat

### Helpful commands
- Show contents from folders
  - `ls -R Documents`
- show history file 
  - `history` this gives us a list of all past commands typed in the current terminal session.
- search history
  - `CTRL + r` reverse search from history
- stop current command
  - `CTRL + c`
- copy and paste into terminal
  - `CTRL + SHIFT + V` paste copied text into terminal
- get kernel info, os version
  - `uname -a`
- get os release file info
  - `cat /etc/os-release`
- get information about installed hardware
  - `lscpu` for cpu
  - `lsmem` for memory
- change user
  - `su - [username]` example `su - admin`
- logout current user
  - `exit` 
### Superuser
Use these commands when we are `not writing a script`. Use these `only` when you are just in the terminal.
- add user 
  - `sudo adduser [name]`
- add group
  - `1 sudo addgroup devops`
- add user to group
  - `adduser [username] [groupname]` example `adduser tom devops`
---

# Package Manager <a id="manager"></a>
There are two common ways to install software in linux.
### Using APT
We should use `APT` and **not** `APT-GET`
#### Apt Commands
- search for package
  - `apt search [packagename]` example `apt search openjdk`
- install package
  - `sudo apt install [packagename]`
- remove package
  - `apt remove [packagename]`
### Using Snap

---

# Vim Editor<a id="vim"></a>
### Install Vim
We use the cli for this `sudo apt install vim`
### Vim CLI Commands
- create new file and use vim editor
  - `vim config.yaml` if the file does not exist, it will create it as well.

### Normal Mode `n`
- delete entire line `dd`
- delete next lines below `d[number]`
- undo changes `u`
- jump to end of line `A` or `$`
- jump to start of line `I` or `0`
### Command Mode `:[command]`
- write file and quit vim `:wq`
- jump to line `[lineNumber]G`
- Search `/[pattern]` example `/nginx`
- jump to next occurrence `n`
- replace old string with new string `:%s/old/new`

### Insert Mode `i`


---
# Linux Accounts & Groups <a id="users"></a>
### Users Management
stores user account information:
- `/etc/passwd` everyone can read it, but only the root user can change the file.
  - `cat /etc/passwd` this prints out a list of all users on the system.
```
sirstich:x:1000:1000:bernhard:/home/sirstich:/bin/bash
USERNAME : PASSWORD : UID : GID : GECOS : HOMEDIR : SHELL 
```
Username - Used when user logs in  
Password - `x` means, that encrypted password is stored in `/etc/shadow file`  
User ID (UID) - each user has a unique ID, UID 0 is reserved for root.  
Group ID (GID) - the primary group ID (stored in `/etc/group file`)  
User ID Info - Comment field for extra information about users
GECOS - a commented field about the user
HOMEDIR - Absolute path of users home dir
Shell - Absolute Path of a shell
### Manage Users from CLI
- add user
  - `sudo adduser [username]`
- change users password
  - `sudo passwd [username]`
- switch user
  - `su - [username]`
- switch to root user
  - `su -`
- remove user
  - `deluser [username]`
- create new group
  - `groupadd devops`
    - to print out our groups we can use `cat /etc/group`
- change primary group of a user
  - `sudo usermod -g [groupname] [username]` example `sudo usermod -g devops tom`
- overwrite subgroups to user
  - `sudo usermod -G [groupname1, groupname2] [username]` example `sudo usermod -G admin,othergroup tom` (Note that the `-G` will overwrite the existing group list.)
- add subgroups to user
  - `sudo usermod -aG [groupname] [username]` example `sudo usermod -aG newgroup tom` (Note: This will **append** this group to the user.)
- remove user from group
  - `sudo gpasswd -d [username] [groupname]`
- print out the groups for the current logged-in user
  - `groups`
- print out the groups for any user
  - `groups [username]`
### Manage Users from Scripts
When we want to have automation, we should use the commands suffixed by `add`.  

Commands:
- `useradd`
- `groupadd`
- `userdel`
- `groupdel`
## User Permissions <a id="users-permission-2"></a>
### Ownership <a id="lx-owner"></a>
- print files in a long listing format to see all information
  - `ls -l` this will give as an output `-rw-r--r--  1 bernhard  staff    790 Jul  9 18:08 README.md`
    - explanation for output:
      - `bernhard` is the owner
      - `staff` is the primary group from that user
- change ownership of file for user and group
  - `chown [username]:[groupname] [filename]` we use the `primary group` from that user. example `sudo chown tom:admin test.txt`.
- change ownership file for user
  - `chown [usernmae] [filename]` when we only want to change the user, we don't need to provide the group.
- change ownership of file for group
  - `chrgp [groupname] [filename]`
### File Permission
We can see the current permissions when we run `ls -l`, this will give us the list of what are the owner, group and the permissions for the current file.
```shell
# output like this when we ran `ls -l`
drwxr-xr-x  3 bernhard  staff     96 Jul  9 18:08 migrations
```
![img.png](img.png)  
#### First Character is for File Type⤴️
`-` means regular file  
`d` means directory  
`c` means character device file  
`l` means symbolic link  
#### Second Block (green) is for user
`r` readonly access  
`w` write access  
`x` execute access  
#### Third Block (red) is for group
`r` readonly access  
`w` write access  
`x` execute access  
#### Fourth Block (blue) is for other
`r` readonly access  
`w` write access  
`x` execute access  
#### No Permission
`-` no permission is represented as a dash  

### Modify Permissions <a id="lx-permission-sb"></a>
For this we use the `chmod` command.
#### User, Owner or Other targeting flags (target-flag)
```shell
u- # user
g- # group
o- # other
```
#### Read, Write or Execute Permission flags (permission-flag)
operator: 
- `-` to remove permission
- `+` to add permission
```shell
chomd [target-flag][operator][permission-flag] [filename]
# full example `chmod u+w filename`

u-r # remove read permission
g+w # add group permission (primary group)
o-x # remove execute permission for others


# or we can use multiple selection
sudo chmod a=r-- filename # a is for all affected
# only for group
sudo chmod g=rw- filename # g is for group and we add write and read
# only for user
sudo chmod u=rw- filename # g is for group and we add write and read
```
#### Shorthand for permission - using octal numbers <a id="lx-permission-num"></a>
using octal number:
- `0` no permission
- `1` execute permission
- `2` write permission
- `4` read permission
- `7` all permissions  
Example: **Read** and **Write** for **User** (4 + 2 = 6), read for group and other (4)
  - `chmod 644 filename.txt`
```shell
# first run 
ls -l # to see the current permissions
# for hidden files we use `ls -la`
chomd 777 [filename]
# full example `chmod 777 filename.txt`
chmod 775 # all permissions for user, read and execute for group and other.
chmod 644 # read and write for user, read for group and other

u-r # remove read permission
g+w # add group permission (primary group)
o-x # remove execute permission for others
```
- read files current permission 
  - `ls -l`
  
---
# Basic Linux Commands - Pipes & Redirects  <a id="basic-commands"></a>
![img_4.png](img_4.png)
### Standard I/O
Every Program has 3 built-in streams:
- STDIN (0) = Standard Input
- STDOUT (1) = Standard Output
- STDERR (2) = Standard Error
![img_1.png](img_1.png)
### Passing input to output
![img_2.png](img_2.png)
### Using `less` tool
`'less' displays the contents of a file or a command output. One page at a time.`  
Mostly used for opening large files, as less doesn't read the entire file, which results in faster load times.  
We use the `pipe` command: `|`  
Pipes the output of the previous command as an input to the next command  
```shell
cat /var/log/syslog | less
```
### Filter output - using `grep` tool
We use `grep` for this  
`grep` stands for Globally Search for Regular Expression and Print out.  
Searches for a particular pattern of characters and displays all lines that contain that pattern.
```shell
history | grep [searchCriteria]
# example
history | grep sudo // this will search for any input with sudo
# search for a sentence, we need " " quotes
history | grep "sudo chmod"
```
### Redirects in Linux
![img_3.png](img_3.png)
We can take the output from the previous command and send it to a file
```shell
history | grep sudo > sudo-commands.txt # > will replace the content
# if we want to append to the end of the file we use >>
history | grep rm >> sudo-rm-commands.txt
```
# Introduction to Shell Scripting <a id="sh-scripting"></a>
Shell scripts have a `.sh` file extension
### Shell vs. sh vs. Bash
![img_5.png](img_5.png)
![img_6.png](img_6.png)
### Create a simple bash script
```shell
touch setup.sh
```
### `Shebang Line` - Tell the OS which shell it should execute
![img_7.png](img_7.png)
We have to write the `shebang` in the first line in our script.  
The Shebang line points to the absolute path to the bash program.
```shell
# to check if the bash exists
ls /bin | grep bash
```
### Execute Shell Script
Before we can run the shell script, we have to change the `permission` of the file.
Because by default, we don't have an execute permission.
```shell
# here we add the execute permission only for the current user.
sudo chmod u+x setup.sh
# check permission
ls -l setup.sh
# if the color of the file changed, this is now an executable
# - execute setup.sh file
./setup.sh # this is how we execute ANY shell script, no matter what syntax
# or if we want to run this for bash specific
bash setup.sh
```
### Shell Variables <a id="sh-scripting-variables"></a>
- Define a variable
  - `file_name=config.yaml` Here we assign the string config.yaml to file_name
- Access variable
  - `$file_name` We use the `$` sign
- Store output of a command in a variable
  - `variable_name=$(command)` We also can store the output from another command
  

#### Conditionals
- if else
```shell
#!/bin/bash
file_name=config.yaml

if [ -d "config" ] # this will check if there is a directory named config
then
  echo "reading config directory contents"
  config_files=$(ls config)
else
  echo "config dir not found. Creating one"
  mkdir config
fi # reverse of if, the program
```
#### File Test Operators & Permission Operators
- `-b file` Checks if file is a block special file, if yes, then condition become true.
- `-c file` Checks if file is a character special file; if yes, then the condition becomes true.
- `-d file` Checks if file is a directory; if yes, then the condition becomes true.
- `-f file` Checks if file is an ordinary file as opposed to a directory or special file; if yes, then the condition becomes true.
- `-g file` Checks if file has its set group ID (SGID) bit set; if yes, then the condition becomes true.
- `-k file` Checks if file has its sticky bit set; if yes, then the condition becomes true.
- `-p file` Checks if file is a named pipe; if yes, then the condition becomes true.
- `-t file` Checks if file descriptor is open and associated with a terminal; if yes, then the condition becomes true.
- `-u file` Checks if file has its Set User ID (SUID) bit set; if yes, then the condition becomes true.
- `-r file` Checks if file is readable; if yes, then the condition becomes true.
- `-w file` Checks if file is writable; if yes, then the condition becomes true.
- `-x file` Checks if file is executable; if yes, then the condition becomes true.
- `-s file` Checks if file has size greater than 0; if yes, then the condition becomes true.

#### Relational Operators - Works only for numeric values
- `-eq` Checks if the value of two operands are equal or not; if yes, then the condition becomes true.
- `-ne` Checks if the value of two operands are equal or not; if values are not equal, then the condition becomes true.
- `-gt` Checks if the value of left operand is greater than the value of the right operand; if yes, then the condition becomes true.
- `-lt` Checks if the value of left operand is less than the value of the right operand; if yes, then the condition becomes true.
- `-ge` Checks if the value of left operand is greater than or equal to the value of the right operand; if yes, then the condition becomes true.
- `-le` Checks if the value of left operand is less than or equal to the value of the right operand; if yes, then the condition becomes true.

#### String Operators
```shell
#!/bin/bash
echo "Setup and configure server"

user_group="nana" 

if [ "$user_group" == "nana" ]
then
	echo "configure the server"
else
	echo "No permission to configure server. wrong user group"
fi

```
#### Positional Parameters
When we want to run our script with some args, we can access them in order by using `$1`.
Range is from `$1 - $9`
```shell
# access
user_group=$1
# calling script
bash setup.sh admin # here admin is the parameter we want to access.
```
- Get all params
  - `$*` With this we can get all the arguments as a single string
- Get number of provided params
  - `$#` We can get the total arguments, which the user entered
- loop through all params
```shell
for param in $*
  do
    echo $param
done
```
#### Read User Input
- `-p` for prompt
```shell
#!/bin/bash

read -p "Enter your password: " user_pwd

echo "$user_pwd" 
```

#### While loop
```shell
sum=0
while true
do
  read -p "enter a score " score
  if [ "$score" == "q" ]; then
      break
  fi
  sum=$(($sum+$score)) # for arithmetic operations, we use Double Parenthesis
  echo "doing something"
done
```
NOTE:
Using Bash `[[` this is bash specific, which allows us to write our variables `without ""`.  

#### Functions
Without parameters
```shell
# definition
function score_sum {
  # logic
}

# calling func
score_sum
```
With Parameters  
- Note:
  - Don't use more than 5 parameters
```shell
function create_file() {
  file_name=$1 # access like args with $
  is_shell_script=$2
   touch $file_name
   echo "file $file_name created"
 
 if [ "$is_shell_script" = true ]; then
     then
       # current user can execute this file
    chmod u+x $file_name
    echo "added execute permission"
 fi
}

# calling with params (must be done with space)
create_file test.txt true
```
#### function with Return value
We can capture the returned value from the last command with `$?`
```shell
function sum() {
  total=$(($1+$2))
  return $total
}
# calling the func
sum 2 10
result=$? # we can capture the returned value from the sum function here with `$?`

# or regular, like this
result=$(sum 2 10)

```
#### Backup Script Example
```shell
# what to backup
backups_files="/home/stich/myfolder"

# where to backup to
dest="/home/stich/backup"

# create archive filename
day=$(date +%A)
hostname=$(hostname -s)
archive_file="$hostname-$day.tgz"

# print start status message
echo "Backing up $backups_files to $dest/$archive_file"
date
echo

# backup files using tar
tar czf $dest/$archive_file $backups_files

# print end status message
echo
echo "Backup finished"
```

### Environment Variables <a id="env-variables"></a>
Env variables are stored on the server. 
> ⚠️ Note:  
> When we `create` an env with `export` , this env variable is only alive `for current session` . When we close our terminal, the env variables are gone. ( ⚠️ Not persistent )
#### PATH Environment Variable
- List of directories to executable files, seperated by `:`
- Tells the shell **which directories to search in for the executable**
#### Env Terminal Commands
- Get all envs from current user
  - `printenv`  
- Show env value for specific key
  - `printenv USER`
  - or to get multiple `printenv | grep USER`  
- Create an env key
  - `export DB_USERNAME=dbuser` - this will work on all linux distros.  
- Delete an env variable
  - `unset KEY_NAME`
### Persist env (user wide)
  - go to `vim ~/.bashrc` file and add your env variables
  - in the **.bashrc** file add your envs 
    - `export DB_NAME=dbuser`
  - reload required 
    - back in the terminal, with `source ~/.bashrc` command. This will load the new env into the current session.

### Persist env (system wide)
This is not linux specific, it will work on all linux distros
```shell
export DB_USERNAME=dbuser # with export we want to store this in env
```
### Add a custom command / program (env) - PATH 
When we want to add our custom program and make it executable like `ls` instead of writing the full path `/usr/bin/ls`. Thanks to the PATH variable, we don't need to provide the full path. Just calling the binary we want is enough.  
#### Short Explanation
- Every time we type in `ls`, it will look into the `PATH Variable` list of directories for the `ls commands binary file`.  
---
#### For our custom program
When we create an executable program, and provide the path variable, with its location. We can run this binary from any location.
This works because of `global env variables` -> `/etc/environment`   
If we want to have this `specifically for the user`, we have to set a variable in `~/.bashrc`.  
- Get the Global Path and append our path to it, to make a custom path
  - `PATH=$PATH:/home/stich` - here we get the global path and append our users dir to it. (We don't need to `export` it, because the Path variable already exists, we just `modify the value`)
```shell
# .bashrc file
# we use the global PATH from /etc/environment and append our location for the executable for it
PATH=$PATH:/home/stich # here we should append the path, where the `welcome` executable is located
# means the welcome script is in /home/stich located, adjust this accordingly to your location
```
---
### Networking <a id="networking"></a>

#### Networking Commands
- `ifconfig`
  - ip address
  - subnet mask address
  - gateway address (router ip address)
- `netstat`
  - what active connections we have on our machine (which apps are listening active on a specific port)
- `ps aux`
  - current running apps and processes
- `nslookup`
  - get ip address of any domain name
    - example `nslookup google.com`
- `ping`
  - check if service or application is accessible
    - example `ping google.com` 

### SSH - Secure Shell <a id="ssh"></a>
#### What is SSH?
SSH is a network protocol that gives users a secure way to access a computer over the internet.  

#### Use cases for ssh:
- Copy File to remote server
- Install software on new server

#### Connect to Server over the internet
There are **two** possible ways of connecting to the remote server.  
1. Using Password Authentication.
   - Username and Password is configured `on server`.
   - User can then connect with username and password.
2. Using SSH Keys
   - The **public key** is installed on the remote server.
   - How to create SSH Key Pair (Public + Private Key)
     1. **Each Client** creates SSH Key Pair on their local machine.
     2. **Private Key** = Secret Key. Is stored securely on the client machine.
     3. **Public Key** = Can be shared, with remote server.
     4. **Admin of Remote Server** can add the public ssh keys for all team members on the remote server.
        1. **Remote Server**: Add **public** key to **authorized_keys** on application server.
        2. Default Port for SSH is **Port 22**  

#### Demo - Connect to Remote Server via SSH <a id="ssh-demo"></a>
1. Create a Remote Server on Cloud Platform
2. Generate SSH Key Pair on local machine
3. Copy Bash Script File to Remote Server
4. Execute Script file on Remote Server
#### Create Droplet 
- Create a Droplet
- Choose Ubuntu OS
- Choose Smallest CPU and Disk
- Authentication -> Password (we have to use this before we can connect to SSH)
##### Connect to Remote Server (Create SSH Key Pair)
- We can connect to the remote server with the `ipv4` from Droplet, this will be the public address from where we can access this server.  
In the terminal on our machine:
```shell
pwd /home/stich
ls .ssh/
ssh-keygen -t rsa 
# the `-t` flag means use the rsa crypto algorithm
cat .ssh/id_rsa.pub # this is the key we have to put onto the remote server
```
On the remote server:
- if there is no `.ssh` folder, we have to create it on the `remote server` 
- Add `public key` to location on server `~/.ssh/authorized_keys`
  - using vim `vim .ssh/authorized_keys`
- in `known_host` is the remote server saved on the client machine  

##### Copy Bash Script & execute
To copy a file to our remote server, we use `scp` command.
```shell
scp test.sh root@64.255.108.123:/root # this takes the private key as an argument
# if we want to use a specific private key
scp -i .ssh/id_rsa test.sh root@64.255.108.123:/root


# while connected on the remote server
ls -l # check file permission 
chmod u+x test.sh # add execute permission
```

# Databases <a id="db"></a>
Databases are used to persist data.
### Database for local development
- Connect to a dev database to develop the new features
- Connect to a test db to test the new feature with realistic data  
### 2 ways for developers to work wit DB
Option 1:
- Each dev installs DB locally
- Each dev has **own DB with own test data**
Option 2:
- Shared DB **hosted remotely**

### Configure Database Connection
The DB Connection is configured in the applications code.  
Each programming language has a lib/module for DB Connection.  
Define in 1 place as environment variables
Configure DB connection from **outside**
- Set entpoint and credentials from outside for each environment.
- Depending on env (dev, test, prod) connects to different DB!
### Pass Env Variables on application Startup
- Either from CLI
- Configure in code editor
- use properties/configuration files
**The best option is to pass them via properties or configuration file**
### Configuration File Example:
```json
{
  "dev": {
    "mongodb": {
      "host": "localhost",
      "port": "27017",
      "database": "db-name"
    }
  },
  "staging": {
    "mongodb": {
      "host": "mongo-host-staging",
      "port": "27017",
      "database": "staging-db-name"
    }
  },
  "prod": {
    "mongodb": {
      "host": "mongo-host-prod",
      "port": "27017",
      "database": "prod-db-name"
    }
  }
}
```
### Databases in Production
- Application connects to db.
- DB must be available, when application starts
- **Before** app is deployed, we need to **install and configure database**
**Data is important so we need to secure them**:
- Replicate db
- Do regular backups
- Make sure it performs under high load  

## Database Types <a id="db-types"></a>
### Key Value DB
Don't use this as a primary DB
Characteristics
- Data is saved in key-value pairs
- unique key
- no joins
- in-memory
Best for:
- Caching
- Message Queue

### Wide Column DB
Don't use this as a primary DB
Characteristics
- two-dimensional key-value store
- Data is saved in tables, rows and columns
- Names and format can vary from row to row (Schema-less)
  Best for:
- Time Series
- IoT Records
### Document DB
Characteristics
- Data is stored in a JSON-like documents
- Schema-less
- no joins
- Denormalized
  Best for:
- Mobile Apps
- Game Apps
- CMS
- Most Apps
### Relation DB
Characteristics
- Data is stored in Tables, Rows and Columns
- Schema (schema and data types need to be created first)
- Normalized to avoid duplicated data
- Most used in industry
  Best for:
- Structured data
### Graph DB
Characteristics
- Data is stored as Nodes and Relationships instead of tables or documents
- Directly connect Entities
- Edges are Relationships
  Best for:
- Graphs
- Patterns
### Search Engine DB
Characteristics
- Dedicated to the search of data
- Optimized for dealing with data
- Full-text search in efficient and fast way
- Similar to document-orientated database

# Build and Package Manager Tools <a id="bpm-tools"></a>
The Application needs to be deployed on a production server.  
For that, we want to **package** application into a **single moveable file (artifact), also called "building the code"**.  
This is what a build tool or package manager tool does.
### What is an "artifact"?
Includes application code and all its dependencies.

### What does "building the code" mean?
- **Compiling** the code
- **Compressing** the code
- Package hundred of files **to 1 single file**

# IaaS <a id="IaaS"></a>
### What do we need on our servers?
- Jenkins on Server for CI/CD

# Docker <a id="docker"></a>
### Docker Main Commands
- list all images
  - `docker images`
- start a container
  - `docker run [imageName]` docker run redis - this will start the image in a container
  - docker run - pulls image and starts container
  - run on specific port
    - `docker run -p [host:container] [imageName]` docker run -p 6000:6379 redis
- start a container in detached mode
  - `docker run -d redis`
- list running containers
  - `docker ps`
- stop running container
  - `docker stop [containerId]`
- list running and stopped containers
  - `docker ps -a`

### Docker Debug Commands
- show container logs
  - `docker logs [containerId]`
- get the terminal of a running container
  - `docker exec -it [containerName] sh`
    - print env variables
      - `env` - inside the terminal

