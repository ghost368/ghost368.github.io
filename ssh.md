Secure Shell (SHH)

* encrypted version of telnet to control and modify remote servers over the network

* ssh command

```
ssh {user}@{host}
```

user - user or root for the admin user
host - IP address or domain name

you will be prompted to enter the password the specified user

* Types of encryption used by ssh
    - Symmetrical encryption (shared key)
    - Asymmetrical encryption (public key used for encryption, private key used for decryption)
    - Hashing (hash is applied to message, it's never decrypted)
    
* Operates on TCP port 22 by default (can be changed if needed)
    - host (server) listens to port 22 for incoming connections
    - it authentificates the client and opens the correct shell environment
    
* It is recommended to use ssh key pairs rather than entering password for convenience and security reasons

* generate ssh key in windows:
    - run cmd as admin (right click -> Run as administrator)
    - command
    
    ```
    ssh-keygen -t rsa -C "your_email@example.com"
    ```
    
    - save to proposed location without passphrase
