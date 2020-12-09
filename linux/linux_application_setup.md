
* Install git, vim, curl using ```sudo apt-get install```

* Change color background of the default gnome terminal (set black on white theme), make bright colour a bit darker

* If right-click does not show New Document option fix it by adding empty file template to Home/Templates (in Ubuntu)


* Installing sublime text (not recommended for ssh-x, better install on windows and use rmate)

	* Install the GPG key:
	```
	wget -qO - https://download.sublimetext.com/sublimehq-pub.gpg | sudo apt-key add -
	```

	* Ensure apt is set up to work with https sources:

	```
	sudo apt-get install apt-transport-https
	```

	* Select the channel to use:

	```
	echo "deb https://download.sublimetext.com/ apt/stable/" | sudo tee /etc/apt/sources.list.d/sublime-text.list
	```

	* Update apt sources and install Sublime Text

	```
	sudo apt-get update
	sudo apt-get install sublime-text
	```

* Installing VSCode on linux (not recommended for ssh-X! unless X11 forwarding is good, use remote ssh otherwise)

	* First install snap

	```
	sudo apt-get install snapd
	```

	* Then install VSCode using snap

	```
	sudo snap install --classic code
	```

	Run VSCode

	```
	code
	```

	(quite slow when used with X11 forwarding, better to use ssh remote access feature)



* Installing Pycharm

	* Install using snap

	```
	sudo snap install --classic pycharm-community
	```

	* Run Pycharm

	```
	pycharm-community
	```

	(works reasonably well with X11 forwarding)


* Modern CSV
	- download free version of Modern CSV 
	- follow the instuction for adding application from linux tutorial
	- open settings file, add light them, and freezing first header row