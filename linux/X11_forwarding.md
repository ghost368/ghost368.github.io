On server linux:

Validate is whether ssh on the X client is configured to forward X11, ensure “/etc/ssh/ssh_config” has the following values.

```
X11Forwarding yes
X11DisplayOffset 10
PrintMotd no
PrintLastLog yes
TCPKeepAlive yes
```

And then restart the ssh service:

```
sudo service ssh restart
```

or

```
sudo systemctl restart ssh
```
