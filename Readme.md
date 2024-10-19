# Playbook Set Up
Note to self, ansible does not support windows as a control host, meaning we can't run ansible straight out of the terminal. We need to launch Ubuntu via wsl in order to run the playbook.

```
    wsl -d Ubuntu
    ansible --version
```

## Steps to run

### Install Python on your unraid server "required"

navigate to community applications and install https://forums.unraid.net/topic/175402-plugin-python-3-for-unraid-611/

If you just search python it will be one of the results at the top. /

### Set up SSH Keys

```
ssh-keygen -t rsa -b 4096 -C "yourEmail@provider.com"
ssh-copy-id root@$unraid_server_ip_address
```

This should be sufficient for running your playbooks

### Recommendations

#### Update your ssh config to more easily ssh to your server

run 
```
nano ~/.ssh/config
```

```
   Host tower
       HostName your_server_ip
       User root
       IdentityFile ~/.ssh/id_rsa  # default path change if you put your key somewhere else

```

Now you should be able to just, 

```
    ssh tower
```

and you should be auth'd and in your server. 

#### truncate ansible-playbook to 'play'

Personally im not typing this over and over so if that floats your boat as well:

```
nano ~/.bashrc
```

Add at the bottom
```
alias play='ansible-playbook'
```
press CTRL X  | Y | ENTER to save

finally source so your session uses your changes

```
source ~/.bashrc
```

Now you can just type play instead of ansible-playbook everytime. Thanks for reading!