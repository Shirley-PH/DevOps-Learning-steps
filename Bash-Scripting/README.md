# Bash scripting

Bash scripting is a way to tell the computer which commands to run and in what order. It helps automate repetitive tasks in the terminal.

- `#!/bin/bash` tells the system which shell to use. The `#!` is called the shebang.
- To run a script, make sure you are in the correct directory and use the following command:
  `./script_name.sh`
- Comments start with `#`. Anything after `#` is ignored by the shell.
- `chmod +x script_name.sh` makes the file executable.
- `> /dev/null` redirects output to a null device so the user does not see unnecessary messages from downloads or other processes.

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

