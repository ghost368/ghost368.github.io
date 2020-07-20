# Based on linux intro book

- don't use root as the main account (use sudo if permissions are needed)

- terminal prompt: ```[user@host dir]```

- for commands - is used to defined an option, GNU programs use -- for long options

- arguments: ```ls /etc``` here ```/etc``` folder is the argument for ```ls``` command
(default for ```ls``` is the current dir)

- so the structure is 
command arguments -options

- page 16 terminal shortcuts

- ```command --help``` will provide useful information about the command

- ```whatis command``` will provide short command description

- Linux system makes no difference between a file and a directory

- ```ls -l``` option describes the file type
(file types short codes on page 28)

--------------------------------

* partitions

	- a partition for user programs (/usr)
	- a partition containing the users' personal data (/home)
	- a partition to store temporary data like print- and mail-queues (/var)
	- a partition for third party and extra software (/opt)


* system data tends to be separated form user data

* use 

```
cd /
ls
```

to see the partitions in the root (descriptions of partitions on page 33)

	- /bin : common programs
	- /etc : most important system configuration files
	- /home : home dirs of common users
	- /mnt : standard mount point for external file systems
	- /root : home dir of the root user
	- /usr : programs, libraries, documentation for all user-related programs

* we don't always have to specify full paths, PATH environment takes care of this

```
echo $PATH
```

shows full path

* ```su``` command means switch user

* ```export PATH=$PATH:/some/paths``` changes the value of PATH but only in the current session ($PATH means we append to existing PATH)

* There are different shells
	- sh : the original Unix shell
	- bash : the standard GNU shell, intuitive and flexible
	- other shells include csh, ksh etc

```
echo $SHELL
```

to see what shell is currently used


* ```echo $HOME``` shows user's home dir, same as ```~```

* description of config files in /etc : page 40

* /var contains all variable files, i.e. that change frequently, such as log files

* ls command output is colored depending on the file type, see page 45

* nautilus is the default file manager in Gnome, the GNU desktop

-----------------------------

* create nested dir (with parents)

```
mkdir -p path/to/dir
```

* ```cp -R from to``` : here -R means recursive copy (copy all nested dirs)

* can do smth like ``` cd /home/*/*/dir``` i.e. skip dir names, will work well if the result is uniquely defined


* find files

```
find /dir -name file_name
```
(other options available, such as -size)

* Ctrl+R will open history search, the latest options will be autocompleted and shown, can type Ctrl+R to go through other matches

* can use ```head -10 file_name``` to show the files head, same for tail and other nb of lines to show

* links
	- hard links : basically two or more independent versions of the same file 
	- soft link or symlink : just a pointer to another file

* create soft links with ```ln -s targetfile linkname```

* ```chmod``` is used to change the access mode, see all options here https://www.computerhope.com/unix/uchmod.html for more info

(stopped at the beginning of chapter 4)