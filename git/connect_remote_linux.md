# Connect to remote repo on linux

* install git if needed
```
sudo apt-get install git
```
* run 
```
git close <URL>
```
and enter account password

* run
```
ssh-keygen
```
to generate
```
~/.ssh/id_rsa
~/.ssh/id_rsa.pub
```
then in the github account go to settings, SSHand GPG keys, 
add new ssh key and put the content of id_rsa.pub to the key 
field but without the username at the end

* Run
```
git config --global user.name "<your name>"
git config --global user.email "<your e-mail>"
```

* what is id_rsa?
