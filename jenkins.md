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