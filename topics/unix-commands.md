# Unix Commands

```sh
# Check OS
cat /etc/issue

# Check current user
whoami

# Find files
find / -name *.so
# Changed in the last day
find /var/www/html -mtime -1 -ls

# List files with permission info
ls -la /var/www

# Find path of command
which find

# Show ip address of client connecting to server via SSH
echo $SSH_CLIENT
echo $SSH_CONNECTION

# Create log entry in /var/log/syslog
logger 'a test message'

# Show installed packages
dpkg --get-selections

# Remove directory
# -d for directory
# -r for recursive
# -f force
rm -r <dir_name>

# Restart apache server
sudo apache2ctl configtest
sudo apache2ctl restart

# Check for new release
sudo do-release-upgrade -d

# Update packages
sudo apt-get upgrade -y
sudo apt-get dist-upgrade
```

## PHP related

```sh
# Find extension folder
php -i | grep extension_dir
```