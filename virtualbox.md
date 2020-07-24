* Installation: download from Oracle website and follow the installation guide

* To install ubuntu distribution need to first download its .iso image file

* Choose New, allocate enough RAM and create VDI with enough memory, then 
go to Settings -> Storage -> Controller IDE -> Optical Drive (under Attributes) and add the iso file

* Start the VM, choose the iso for boot and follow the instructions

* Download and install MobaXterm on windows

* Settings -> Network -> Adapters
  * Host-only only permits network operations with the Host OS.
  * NAT mode will mask all network activity as if it came from your Host OS, although the VM can access external resources.
  * Bridged mode replicates another node on the physical network and your VM will receive it's own IP address if DHCP is enabled in the network.

* Need linux server with ```openssh-server``` installed and ssh authentification authorized. This is easy to configure with 
Ubuntu Server but less clear with Fedora and CentOS

* Run 
```
sudo apt-get install openssh-server
sudo service ssh status
```
(should be active, also has start, restart, stop options)

* Use this article 
https://medium.com/platform-engineer/port-forwarding-for-ssh-http-on-virtualbox-459277a888be 
for post-forwarding settings.

* To solve potential problems with resolution when using VM GUI application install guest additions on VM

```
sudo apt update
sudo apt install build-essential dkms linux-headers-$(uname -r)
```

TODO:
post-forwarding, host, NAT, Host only, TCP, SSH, HTTP, port, host port, guest port, proxy
