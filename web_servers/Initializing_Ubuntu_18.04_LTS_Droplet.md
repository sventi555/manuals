# Initializing Ubuntu 18.04 LTS Droplet
## Overview
In this guide, we will be setting up an Ubuntu 18.04 LTS remote server. This will entail connecting to the server, setting up a user, and ensuring that ssh authentication is configured. Lastly, we will be updating the software in our system.


## Requirements
- A system running Ubuntu 18.04 LTS


## Process
### Step 1: Connecting to the server

ssh into the server.
```
$ ssh root@SERVER_IP
```


### Step 2: Adding a user

Enter the following command then enter the additional information when prompted. Be sure to replace `sven` with your username:
```
$ adduser sven
```

We now need to give the new user root privileges.
```
$ usermod -aG sudo sven
```


### Step 3: Configuring ssh for new user

Next, we are going to create the .ssh directory in our user's home folder, then copy the authorized_keys file into that directory so we can connect to our server as the user.
```
$ mkdir /home/sven/.ssh
$ cp ~/.ssh/authorized_keys /home/sven/.ssh/authorized_keys
```

We now need to switch users and change the ownership of the file.
```
$ su - sven
$ sudo chown -R sven:sven ~/.ssh
```

**ALTERNATIVELY** if authorized_keys doesn't exist in the root .ssh directory, run the following as the non-root user:
```
$ mkdir ~/.ssh && touch ~/.ssh/authorized_keys
```


### Step 4: Updating the system

Finally, update existing software by running the following:
```
$ sudo apt update
$ sudo apt upgrade
```

Optionally, clean out unnecessary and outdated files and update the dependency tree with these commands respectively: `sudo apt autoremove` and `sudo apt autoclean`.


## Wrap-up
We've now initialized our Ubuntu 18.04 droplet by adding a user, configuring ssh, and updating the system. Consider [adding an ssh config](./Adding_an_ssh_Config.md) now that your server is set up.

