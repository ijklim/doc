# Unix Commands

```sh
# Check OS
cat /etc/issue

# Check current user
whoami

# Find files
find / -name *.so

# List files with permission info
ls -la /var/www

# Find path of command
which find

# Show ip address of client connecting to server via SSH
echo $SSH_CLIENT
echo $SSH_CONNECTION

# Create log entry in /var/log/syslog
logger 'a test message'
```

## PHP related

```sh
# Find extension folder
php -i | grep extension_dir
```