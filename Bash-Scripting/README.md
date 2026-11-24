# Bash scripting

Bash scripting is a way to tell the computer which commands to run and in what order. It helps automate repetitive tasks in the terminal.

## 1. Basic understanding

- `#!/bin/bash` tells the system which shell to use. The `#!` is called the shebang.
- To run a script, make sure you are in the correct directory and use the following command:
  `./script_name.sh`
- Comments start with `#`. Anything after `#` is ignored by the shell.
- `chmod +x script_name.sh` makes the file executable.
- `> /dev/null` redirects output to a null device so the user does not see unnecessary messages from downloads or other processes.

### Example: basic understanding

The following example uses a template from Tooplate:
<https://www.tooplate.com/zip-templates/2166_ivory_flow.zip>

The script demonstrates basic Bash scripting:

```bash
#!/bin/bash

echo "##################################"
echo "Installing packages"
echo "##################################"
sudo yum install wget unzip httpd -y > /dev/null

# Start and enable HTTPD service
echo "##################################"
echo "Starting and enabling HTTPD service"
echo "##################################"

sudo systemctl start httpd
sudo systemctl enable httpd

# Create temporary directory
echo "##################################"
echo "Starting artifact deployment"
echo "##################################"

mkdir -p /tmp/webfiles
cd /tmp/webfiles

wget https://www.tooplate.com/zip-templates/2166_ivory_flow.zip > /dev/null
unzip 2166_ivory_flow.zip > /dev/null

sudo cp -r 2166_ivory_flow/* /var/www/html/

# Restart service
sudo systemctl restart httpd
echo

# Clean up
echo "##################################"
echo "Removing temporary files"
echo "##################################"

rm -rf /tmp/webfiles

echo

sudo systemctl status httpd
ls /var/www/html/
```

This example shows how a script can install the required packages, start services, download files, deploy them to a web directory, and clean up temporary files afterward.

Example of the deployment process:

![the-art-of-quiet](the-art-of-quiet.png)

## 2. Variables

A variable is a temporary container used to store information that can be reused throughout the script.

- To create a variable, assign a value:
  `NAME="DevOps"`
- To use the value stored in a variable, add `$` before the variable name:
  `echo "$NAME"`
- This prints the value stored in the variable.

Example:

```bash
SKILL="DevOps"
echo "$SKILL"
# Output: DevOps
```

Important:

- Variables are useful to avoid repeating long values in a script.
- They make scripts easier to read and modify.
- The value of a variable can be changed during the script if needed.

### System variables

Bash also provides environment variables that contain system and session information. For example:

- `$USER`: the name of the current user.
- `$HOSTNAME`: the name of the current host.
- `$HOME`: the home directory of the current user.

### Example using variables

```bash
#!/bin/bash

# Variable declaration
PACKAGE="httpd wget unzip"
SVC="httpd"
URL='https://www.tooplate.com/zip-templates/2098_health.zip'
ART_NAME='2098_health'
TEMPDIR="/tmp/webfiles"

# Install dependencies
echo "########################################"
echo "Installing packages"
echo "########################################"
sudo yum install $PACKAGE -y > /dev/null
echo

# Start and enable service
echo "########################################"
echo "Starting and enabling HTTPD service"
echo "########################################"
sudo systemctl start $SVC
sudo systemctl enable $SVC
echo

# Create temporary directory
echo "########################################"
echo "Starting artifact deployment"
echo "########################################"
mkdir -p $TEMPDIR
cd $TEMPDIR
echo

wget $URL > /dev/null
unzip $ART_NAME.zip > /dev/null
sudo cp -r $ART_NAME/* /var/www/html/
echo

# Restart service
echo "########################################"
echo "Restarting HTTPD service"
echo "########################################"
sudo systemctl restart $SVC
echo

# Clean up
echo "########################################"
echo "Removing temporary files"
echo "########################################"
rm -rf $TEMPDIR
echo

sudo systemctl status $SVC
ls /var/www/html/
```

This is how the script looks after it is executed.

![new-file-style](new-file-style.png)

## 3. Quotes

There are several ways to use quotes in Bash:

- Single quotes preserve text literally. Bash does not expand variables or most special characters inside them.
- Double quotes allow Bash to expand variables and perform command substitution.
- The backslash (`\`) escapes the character that follows it.

### Single and double quotes

Example:

```bash
VIRUS="covid19"

echo "I want to know if you have $VIRUS"
# Output: I want to know if you have covid19

echo 'I want to know if you have $VIRUS'
# Output: I want to know if you have $VIRUS
```

### Escaping special characters

Use a backslash to prevent Bash from interpreting a special character:

```bash
echo 'This test costs $9 million'
# Output: This test costs $9 million

echo "This test costs \$9 million"
# Output: This test costs $9 million
```

## 4. Command substitution

Command substitution stores the standard output of a command in a variable or passes it to another command.

The recommended modern syntax uses `$(command)`. The older backtick syntax is also available, but nested commands are more difficult to read and maintain:

```bash
uptime
# Output: 10:42:39 up 1:04, 1 user, load average: 0.00, 0.00, 0.00

UP=$(uptime)
echo "$UP"
# Output: 10:42:39 up 1:04, 1 user, load average: 0.00, 0.00, 0.00
```

Use double quotes around `$UP` when printing the stored value to prevent word splitting and filename expansion:

For example:

```bash
who
# Output: vagrant pts/0 2026-11-23 09:43 (10.0.2.2)

CURRENT_USER=$(who)
echo "$CURRENT_USER"
# Output: vagrant pts/0 2026-11-23 09:43 (10.0.2.2)
```

## 5. Exporting variables

By default, variables created in a shell are local to that shell. The `export` command makes a variable available to child processes started by that shell.

Export the variable name, not the expanded value:

```bash
SEASON="Sprint"
export SEASON

echo "$SEASON"
# Output: Sprint
```

Exporting a variable does not permanently change the system or make it available to every existing shell. The variable is lost after the shell exits unless it is restored from a startup configuration file.

### Make a variable permanent for one user

Add the variable to `~/.bashrc` for Bash sessions or `~/.profile` for login shells:

```bash
export SEASON="Sprint"
```

Then open a new shell or reload the file:

```bash
source ~/.bashrc
```

For system-wide variables, add the export statement to `/etc/profile`. This file affects login shells for all users, and administrative privileges may be required to modify it:

```bash
export SEASON="Sprint"
```

Log out and back in, or open a new login shell, to verify that the configuration is applied.

## 6. User input

Bash can prompt users and store their responses in variables using the `read` command.

- `read NAME` reads input and stores it in a variable named `NAME`.
- `read -p "Prompt: " NAME` displays a prompt before reading the input.
- `read -s` hides the user's input, which is useful when entering passwords.

### Example: user input

```bash
#!/bin/bash

echo "Enter your skill:"
read SKILL

echo "Your $SKILL skills are in high demand in the IT industry."

read -p "Username: " USR
read -sp "Password: " PASS

echo
echo "Login successful. Welcome, $USR."
```

In this example, `USR` stores the username and `PASS` stores the password. The password is not displayed while it is being entered.

## 7. Decision making: if statements

An `if` statement evaluates a condition and executes a block of commands when the condition is true.

### Numeric operators

- `-eq`: equal to.
- `-ne`: not equal to.
- `-lt`: less than.
- `-le`: less than or equal to.
- `-gt`: greater than.
- `-ge`: greater than or equal to.

### File operators

- `-b`: true if the path exists and is a block special file.
- `-c`: true if the path exists and is a character special file.
- `-d`: true if the path exists and is a directory.
- `-e`: true if the path exists.
- `-f`: true if the path exists and is a regular file.
- `-l`: true if the path exists and is a symbolic link.
- `-r`: true if the file or directory is readable.
- `-s`: true if the file is not empty.
- `-w`: true if the file or directory is writable.
- `-x`: true if the file or directory is executable.

### Example: testing a numeric value

```bash
#!/bin/bash

read -p "Enter a number: " NUM
echo

if [ "$NUM" -gt 100 ]
then
        echo "The number is greater than 100."
        sleep 3
        echo "The number: $NUM"
        echo
        date
else
        echo "The number is 100 or less."
fi

echo "Script execution completed."
```

This example uses `-gt` to compare a numeric value with 100. The script runs the commands in the `else` block when the condition is false.

### Example: checking multiple conditions

```bash
#!/bin/bash

VALUE=$(ip addr show | grep -v LOOPBACK | grep -ic mtu)

if [ "$VALUE" -eq 1 ]
then
        echo "One active network interface was found."
elif [ "$VALUE" -gt 1 ]
then
        echo "Multiple active network interfaces were found."
else
        echo "No active network interfaces were found."
fi
```
