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

* ```export PATH=$PATH:/some/paths``` changes the value of PATH but only in the current session ($PATH means we append to existing PATH);
if export is used inside a script, the change to path will only be visible inside this script.

* vs source (!)  (or no precommand for bash and . for source):
bash creates a sub-shell which source runs the script in the current shell (so e.g. export action inside script won't be applied to the current session if run with bash; in other words source will run as we copy and run the script content in the current session)

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

 * ```stat filename``` check file stats (e.g. created, last modified etc)

* ```ls | grep -P "^A.*[0-9]{2}$" | xargs -d"\n" rm```
-----------------------------

* create nested dir (with parents)

```
mkdir -p path/to/dir
```

* ```cp -R from to``` : here -R means recursive copy (copy all nested dirs)

* ```cp /home/usr/dir/{file1,file2,file3,file4} /home/usr/destination/``` copy multiple files to another destination (filename coma-separated without spaces!)


* can do smth like ``` cd /home/*/*/dir``` i.e. skip dir names, will work well if the result is uniquely defined

* ```cd -``` cd to the previous location (e.g. cd somewhere and then want to go back)


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


* ```clear``` to clear terminal screen output

* ```application --version``` : check installed version of any application


* create script to add current working dir to python path with 
```
#!/bin/bash

export PYTHONPATH="$PYTHONPATH:$(pwd)"
```
(source it before running python scripts with pdf option)

* single Tab will autocomplete file or command name, while if there're multiple options a double Tab will show all options

* mkdir -p /a/b/c to create nested directories


* run ```bind TAB:menu-complete``` : this will cycle through dir contents when using cd and already being inside dir (will autocomplete part names as usual of course); use right arrow to fix choice

* in general, above function is menu-complete -- using bind it's possible to bind a command to a key

* ```lscpu``` get CPU information (including the number or CPUs)

* some CPUs now can do 2 or more things simultaneously, nb of CPUs times the number of simultaneous threads for each CPU is the number of *logical processors*


* can ```cd dir```, don't need to pass ```cd ./dir```

* apt and apt-get commands are very similar, apt is indended for final users, while apt-get is a kind of back-end command with more backward compatibility requirements

* ```curl <url>``` command can be used to test web-page response message, e.g. when creating web api that returns json data (more handy than using browser)


*```rm /path/to/dir/*``` to remove everything inside a directory (```rm ./*``` for the current dir)
* try removing file (do nothing if exists) ```rm -f /path/to/file```


* ~/.bashrc is a script that is run whenever bash is started. So e.g. to always have some path in the PATH variable can append
```
export PATH=/some/extra/path:$PATH
```
to the .bashrc file


* wget is a command to download files (e.g. installers), simplest version : ```wget <url>``` download to the current directory

* sudo apt-get autoremove, clean, purge, remove, update, apt-mark etc - ADD

* finding files/folders in linux
```
 find . -name name_or_pattern
 ```

 * creating users:
 	* user in sudo group have admin rights, to check sudo group
 	```
 	grep -Po '^sudo.+:\K.*$' /etc/group
 	```
 	* create new user
 	``` sudo adduser username ```
 	* delete user (with its home dir) : ```sudo deluser --remove-home username```
 	* modify username ```usermod -l new_username old_username```
 	* change user password ```sudo passwd username```
 	* to switch user in the current session ```su - username``` (su command); 
 	then use logout to continue your session;
 	(```su username``` will switch user but keep me in my home dir; using ```-``` acts like if I would logout and login to another user properly) 


* ```rm -rf /path/to/dir?``` remove dir if exists otherwise do nothing


* running a command async : ```$ myscript &``` (putting & at the end)


* some the keyboard layout may be slightly wrong (e.g. " swaped with @ etc) - this is likely due to the difference of English (UK) and English (US) - try both layouts (in Ubuntu can add in system settings -> language and region etc) and leave the one that is correct

* ```git diff /path/to/file1 /path/to/file2``` can be used to get git-like colorful output of the difference between two files, even if that is outside any git repository (!!)