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
- *This command allow you change the root user*
```bash
sudo -i
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
- **mkdir -p** *Create a directory file with direction, you can create even if the router doesn't exit yet, adding **-p***
```bash
#For example
mkdir -p /opt/dev/devops/test1
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
- **cat**: *Show the content of the file.* 
```bash
#For example:
cat test1.txt 
#Output: Lorem ipsu..
``` 
- **ln -s** *Create a link direction*: You can create a pointer/shortcut route from one file or directory to another..
```bash
#For example:
ln -s router/direction/text.txt newRoute
ls -l
#Output: newRoute => router/direction/text.txt
``` 
- **unlink** *Remove a symbolic link *
```bash
#For example:
unlink newRoute
ls -l
#Output: 
``` 
- **ls -l** *Displays every file and directory with its type, permissions, owner, size, and modification time.*
```bash
#For example:
ls -l
#Output: 
``` 
You can also sort by the newest changes using `-t`, or reverse the order using `-r`:
```bash
#For example:
ls -lt /directory
ls -ltr /directory
``` 
- **Head** *Display the first 10 lines by default. Also you can search a keyword inside of the file by using `/`*
```bash
#For example:
head fileName
#Output: 
...
``` 

Note: In case, you want only read the first 5 lines, you online need to specify after the word  `head`
```bash
#For example:
head -5 fileName
#Output:
...
...
...
...
... 
``` 

In the opposite side,
- **Tail**: *Display the last 10 lines by default. Also, you can specify how many line you want display*
```bash
#For example:
tail -5 fileName
#Output: 
...
...
...
...
...
``` 
- **Tail -f**: *Read ans show dynamicly the changes in real time*

Note: this is very usuful for monitoring logs

```bash
#For example:
tail -f fileName
#Output: 
...
...
...
...
...
``` 
- **Cut [OPTIONS] [FILE]**: *This command filter specific sections or fiels from each line of file. Your need to follow the proper structure*

Extra information:
- `-d`: Specify the delimiter, which separates the fields, in this case was `(:)`.

- `-f:` Selects nº of colummn which is the objective. In this case, the first field `(1)`.

- `directionFile`: The file containing relevant information.

```bash
#For example: Display the usernames registered on the system /etc/passwd
#This file contains line started like this: john:x1000:1000:John Doe:/home/john:/bin/bash
cut -d: -f1 /etc/passwd
#Output: 
root
daemon
bin
sys
sync
games
...
``` 
## SED (Stream editor)

The sed command is a text-processing tool used to search, replace, delete, or modify text in a file or command output.

- **Sed -i** *Replaces every occurrence of oldWord with newWord and prints the result to the terminal without modifying the original file*

Note:  `Sed` will show you how would looks like the result and `-i` make the really change*
```bash
#For example: 
#There is a file called "testing.txt" with the folloing content:
# "Only I want to add more information with this key word
# salad, that has a lot  vitamins and fruits, vegetable... salad"

## Replace "salad" with "onion" in the output
sed  's/salad/onion/g' testing.txt
#Output: 
# Output: Only I want to add more information with this key word
#onion, that has a lot  vitamins and fruits, vegetable...onion

cat testing.txt
#Output: 
# Only I want to add more information with this key word
#salad, that has a lot  vitamins and fruits, vegetable... salad

sed  -i 's/salad/onion/g' testing.txt
#Output: 
# Output: Only I want to add more information with this key word
#onion, that has a lot  vitamins and fruits, vegetable...onion
``` 

## GREP 
### Linux grep Syntax ###
This structure teaches how to write commands properly. Undeerstanding this will helps you use them correctly and avoid common error.
> #### GREP [OPTIONS] PATTER [FILE…] 

- **Grep -i** *The `-i` option performs a case-insensitive search. This means that uppercase and lowercase letters are treated as equivalent.*

```bash
#For example: Search for "firewall" regarless of capitalization
grep -i firewall fileDirection
#Output: 
Firewall configuration
firewall --desable
``` 
- **Grep -R** *The `-R` option searches recursively through a directory, including files in its subdirectories.*

Note: `/*` The asqueristic allow us to search throught all files that contains the route.
Note: Recursive searching is useful when you need to find a keyword across multiple files and directories.

```bash
#For example: Search recursively for "SELINUX" in /etc
grep -R SELENUX /etc/*
#Output: 
/etc/selinux/config:# SELINUX= can take one of these three values:
/etc/selinux/config:# NOTE: In earlier Fedora kernel builds, SELINUX=disabled would also
/etc/selinux/config:SELINUX=permissive
/etc/selinux/config:# SELINUXTYPE= can take one of these three values:
/etc/selinux/config:
...
``` 
- **Grep -vi** *Display lines that do not contain the specified keyword, regardless of capitalization.*
```bash
#For example: Display lines that do not contain "firewall"
grep -vi firewall fileDirectory*
#Output: 
System configuration
Network settings
Service status
...
``` 

## VIM EDITOR
### Commands for this editor ###
When you are inside a file, if you want to apply any command from this list, you must press the **ESC** key to enter Command Mode and then type the instruction.
- **:w** to write/save
- **:q** to quite
- **:w <filename.txt>** to name a new file
- **:q!** to quite **without** **saving** the changes to the file
- **:se nu** Enumering every line of the file
- **:%d** Remove the entire content of the file
- **:%s/replaceWord/newWord/g** Searches for replaceWord and replaces it with newWord throughout the entire file..

You can also combine commands together:
```bash
#For example:
:wq
#Output: save and close the file
``` 

Example of replace word:

Note: `g` means all occurrences on each line, while `%`  means all lines in the file. Together, they replace all matches throughout the document

``` bash
#For example: 
:%s/firewall/security/g
#Output: Replaces every occurrence of firewall with security throughout the file.
```

**During edition of the file**

*Note: Make sure you are in Command Mode (press ESC) to use these.*

- ``o`` Insert a new line below the current line and enter Insert Mode
- ``gg`` Move the cursor to the very first line of the file.
- ``G`` (or Shift + g) you drop at the last line of the file
- ``yy`` Copy the current line.
- ``[number]yy``To copy multiple lines (e.g., `5yy` copies 5 lines counting downwards from your cursor position).
- ``p`` Paste the copied line below the cursor.
- ``dd`` Delete (cut) the entire current line.
- ``u`` Undone the last action
- ``/`` Search the next work after **/** in the entire file (e.g `/word`)

