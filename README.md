# DevOps-BC
## ToC
- [Linux vs. Microsoft Filesystem](#os)  
- [CLI Commands](#cli)




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
Like Network, Linux user data, passwords.

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


weiter bei 22:39 / 6

---

