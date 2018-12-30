# Adding an ssh Config
## Overview
In this guide, we will be going over how to create an ssh config file to allow for easier access to your remote server.


## Requirements
- A remote server with ssh configured


## Process
### Step 1: Create the config file

Create the config with the following command:
```
$ vim ~/.ssh/config
```

Add the following lines to your config file, making sure to replace `SERVER_ALIAS` with the name you want to give your server, `SERVER_IP` with the corresponding IP address, and `USERNAME` with the username you are connecting as:
```
Host SERVER_ALIAS
    HostName SERVER_IP
    User USERNAME
```


### Step 2: Accessing your server

You can now access your server by entering the following:
```
$ ssh SERVER_ALIAS
```


## Wrap-up
We have now configured a config to access your remote server much easier.
