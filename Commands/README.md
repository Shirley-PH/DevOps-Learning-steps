# ESSENTIAL COMMANDS FOR A DEVOPS ENVIROMENT

## DESCRIPTION
 Here you will find a short list of commands that you need to know for working with different platforms like Vagrant, Linux, etc. This guide is designed for beginners

## VAGRANT
- *Created and boots up (turn on) the virtual machine*
```bash
vagrant up 
```
- *Connects to your running virtual machine via SSH.*
```bash
vagrant ssh 

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

#### Linux Command Structure
This structure teaches how to write commands properly. Undeerstanding this will helps you use them correctly and avoid common error.
> #### COMMANDS  [OPTIONS] [ARGUMENTS(s)] 

If you ever get stuck, you can use the `--help` option. This will show you the available options and argument for the command.

**As you will see, the following commands all follow this structure:**

- *Shows a history of all the commands you have typed in the current terminal session so far*
```bash
history
``` 
- **~$ (Dollar desing)** *Means you are logged in as standar, non-privileged user*
```bash
#For example  
username@localhost ~ ] $
```

- **~# (Hash/ Pound sign)** *Means you are logged as the root user (superuser) with full administrative privilage*
``` bash
#For examle >
root@localhost ~ ] #
```
- *Show a route direction/files where you are right now*
```bash
#For example:
pwd
# Output: /home/vagrant
``` 
- **mkdir** *Create a directory file*
```bash
#For example
mkdir dev
``` 
- **Touch**: *Creates an empty file. You need to provide the proper extension (e.g., .txt, .pdf, etc.).*
```bash
touch filename.txt
``` 
- **Cp**: *Copies a file from one directory to another. You must specify the source file and the destination directory path.*
```bash
 #For example:
cp example1.txt ./Dev
cd ./Dev
ls
# Output: example1
``` 
- **Mv(Move)** *Moves a file or directory from one location to another.*
```bash
#For example:
mv test1.txt ./Dev
cd ./Dev
ls
# Output: test1
``` 
- **Mv(Rename)**: *This command is also used to rename files or directories*
```bash
#For example:
 mv test1.txt test2.txt
ls
# Output: test2.txt
``` 
- **Rm**: *Removes files. To remove a directory and its contents recursively, you need to add the **-r** flag.* 
```bash
#For example:
rm test1.txt 
rm -r directory
``` 