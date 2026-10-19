# ESSENTIAL COMMANDS FOR A DEVOPS ENVIROMENT

## DESCRIPTION
 Here you will find a short list of commands that you need to know for working with different platforms like Vagrant, Linux, etc. This guide is designed for beginners

## VAGRANT
- *Connects to your running virtual machine via SSH.*
```bash
vagrant ssh 
``` 
- *Created and boots up (turn on) the virtual machine*
```bash
vagrant up 
``` 
- *Shows if the current virtual machine are on/off/suspended*
```bash
vagrant status
``` 
- *Lists all Vagrant machines created across your entire system*
```bash
vagrant global-status
``` 
- *Refreshes the global status and prunes (removes) entries of machines that no longer exist*
```bash
vagrant global-status --prune
``` 
- *Close the current SSH conextion and turns to your host terminal*
```bash
exit
``` 
- *Shuts down (turns off) the virtual machine gracefully*
```bash
vagrant halt
``` 
- *Remove the entire virtual machine*
```bash
vagrant destroy
``` 
## LINUX BASIC & PROMPTS
- *Shows a history of all the commands you have typed in the current terminal session so far*
```bash
history
``` 
- **~$ (Dollar desing)** *Means you are logged in as standar, non-privileged user*
```
For example > username@localhost ~ ] $
```

- **~# (Hash/ Pound sign)** *Means you are logged as the root user (superuser) with full administrative privilage*
```
For examle > root@localhost ~ ] #
```