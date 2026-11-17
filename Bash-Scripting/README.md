# Bash scripting

Bash scripting is a way to tell the computer which commands to run and in what order. It helps automate repetitive tasks in the terminal.
## 1. Basic understanding

- `#!/bin/bash` tells the system which shell to use. The `#!` is called the shebang.
- To run a script, make sure you are in the correct directory and use the following command:
  `./script_name.sh`
- Comments start with `#`. Anything after `#` is ignored by the shell.
- `chmod +x script_name.sh` makes the file executable.
- `> /dev/null` redirects output to a null device so the user does not see unnecessary messages from downloads or other processes.

## Example basic understanding
I used a template from Tooplate to create a simple HTML example. Here is the link:
https://www.tooplate.com/zip-templates/2166_ivory_flow.zip

Here is a small example usign bash scripting:

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
systemctl restart httpd
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
![the-art-od-quiet](the-art-of-quiet.png)

## 2. Variables

A variable is a temporary container used to store information that can be reused throughout the script.

- To create a variable, assign a value:
  `NAME="DevOps"`
- To use the value stored in a variable, add `$` before the variable name:
  `echo $NAME`
- This prints the value stored in the variable.

Example:
```bash
SKILL="DevOps"
echo $SKILL
# Output: DevOps
```

Important:
- Variables are useful to avoid repeating long values in a script.
- They make scripts easier to read and modify.
- The value of a variable can be changed during the script if needed.

## Example using variables
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
systemctl restart $SVC
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
