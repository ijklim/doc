# Unix Commands

```sh
# Check OS
cat /etc/issue
# Apache version check
apache2ctl -v

# Check current user
whoami
# Show user accounts
cat /etc/passwd
# Simulate superuser
sudo -i
su
# Show server date and time
date

# Find files
find / -name *.so
# Changed in the last day
find /var/www/html -mtime -1 -ls

# List files with permission info
ls -la /var/www

# Copy file from remote to local
scp <username>@<host>:<remote-filepath> <local-filepath>
# e.g. scp ubuntu@example.com:~/tmp/backup.sql.gz ~/Documents/backup/

# Remove directory
# -d for directory
# -r for recursive
# -f force
rm -r <dir_name>

# Find path of command
which find

# Show ip address of client connecting to server via SSH
echo $SSH_CLIENT
echo $SSH_CONNECTION

# Create log entry in /var/log/syslog
logger 'a test message'

# Show installed packages
dpkg --get-selections

# Restart apache server
sudo apache2ctl configtest
sudo apache2ctl restart

# Check for new release
sudo do-release-upgrade -d

# Update packages
sudo apt-get upgrade -y
sudo apt-get dist-upgrade

# List user specific cronjob/crontab
sudo ls -l /var/spool/cron/crontabs
# Show what is in crontab
sudo cat /var/spool/cron/crontabs/root
sudo cat /var/spool/cron/crontabs/ubuntu

# List services controlled by `System V`
service --status-all
# Check specific service
service php7.4-fpm status
systemctl status php7.4-fpm.service
# Restart a service
sudo systemctl restart php7.4-fpm.service
```

## PHP related

```sh
# Find extension folder
php -i | grep extension_dir
```


## Tasks

### Clean up log folder

```sh
# Change permission of file
sudo chmod 777 /var/log/apache2/error.log
# Change permission of folders
sudo chmod -R 775 /var/log/apache2 /var/log/apache2/cache
# Change file ownership
sudo chown ubuntu /var/log/apache2/error.log

# Find files older than a certain time
sudo find . -maxdepth 1 -type f -mtime +7
```

### Enable mods-available for edit
```sh
sudo chmod 777 /etc/apache2/mods-available
sudo chmod 777 /etc/apache2/mods-enabled
sudo chmod 755 /etc/apache2/mods-available
sudo chmod 755 /etc/apache2/mods-enabled
```


## Troubleshooting Guide

### Error: Config variable ${APACHE_RUN_DIR} is not defined. apache2: Syntax error on line 83 of /etc/apache2/apache2.conf: DefaultRuntimeDir must be a valid directory, absolute or relative to ServerRoot

* Solution: Run `source /etc/apache2/envvars`

* Verification: apache2 -S

### Error: Apache is running a threaded MPM, but your PHP Module is not compiled to be threadsafe. You need to recompile PHP. AH00013: Pre-configuration failed

* Solution: Steps to enable http2

  ```sh
  # Apache version check
  apache2ctl -v

  # Install php fpm that supports http2
  sudo apt-get install php7.4-fpm

  # Disable necessary modules
  # Note: Files located at /etc/apache2/mods-available/*.[load|conf]
  sudo a2dismod php7.4
  sudo a2dismod mpm_prefork
  # Enable necessary modules
  sudo a2enmod mpm_event
  sudo a2enmod http2
  sudo a2enmod proxy_fcgi setenvif
  sudo a2enconf php7.4-fpm

  # Check MPM enabled
  apache2ctl -V | grep MPM

  # Test configuration settings
  sudo apache2ctl configtest

  # Restart apache
  sudo apache2ctl restart

  # Check apache
  apache2ctl -V
  sudo apache2ctl -t -M
  ```

  * Following 2 lines should be in `/etc/apache2/apache2.conf`

  ```
  Protocols h2 http/1.1
  Protocols h2 h2c http/1.1
  ```
