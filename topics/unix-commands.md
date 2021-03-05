# Unix Commands

```sh
# Check OS
cat /etc/issue

# Find files
find / -name *.so

# List files with permission info
ls -la /var/www

# =========================
# php
# =========================

# Find extension folder
php -i | grep extension_dir

# Show ip address of client connecting to server via SSH
echo $SSH_CLIENT
echo $SSH_CONNECTION
```