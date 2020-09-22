* install on linux
```
wget -q -O - http://pkg.jenkins-ci.org/debian/jenkins-ci.org.key | sudo apt-key add -
sudo sh -c 'echo deb http://pkg.jenkins-ci.org/debian binary/ > /etc/apt/sources.list.d/jenkins.list'
sudo apt-get update
sudo apt-get install jenkins
```
in some cases there might be a GPG error (no public key), in this case add the key using
```
sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys <your key>
```
(where <your_key> is what the error message shows; then need to re-run update and install jenkins commands)

also java might be needed for jenkins, install using 
```
sudo apt install default-jdk
```
(useful link https://www.fosstechnix.com/install-jenkins-on-ubuntu/)


* start jenkins server
```
sudo systemctl start jenkins
sudo systemctl status jenkins
```

* allow remote access to jenkins via port 8080
```
sudo ufw allow 8080
sudo ufw status
```

* to access remotely on virtual machine add tunnel 8080 to 8080 
(for this need to use Host Only adapter and real IP address if VM is on virtual box)


* jenkins will create its own user (called jenkins) and Jenkinsfile will run script from this user's side; 
so this like conda, poetry, etc won't be installed or visible from there. May be useful to automatically run those commands under another user, for this
go to /etc/sysconfig/jenkins on RHEL or /etc/default on Debian change the JENKINS_USER to whatever you want. 
(user maybe given in a variable with value 'jenkins' - change just user, not the variable)
```$JENKINS_USER="vlad"```

Then change the ownership of the Jenkins home, Jenkins webroot and logs.
chown -R vlad:vlad /var/lib/jenkins 
chown -R vlad:vlad /var/cache/jenkins
chown -R vlad:vlad /var/log/jenkins

(in production enterprise environment this will probably be already set up in a more proper way)


---------------

* MORE :
	- what plugins to install (Git, Git source)
	- adding Github hook, what about bitbucket?
	- creating hook requires a Jenkins url that github can use (might use ngrok for that)
	but probably manual deploy is fine