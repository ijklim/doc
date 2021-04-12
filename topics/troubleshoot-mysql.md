# MySQL Troubleshooting Guide


## Installation on Ubuntu

```sh
# Stop current version if necessary
sudo -i
sudo service mysql stop
killall -KILL mysql mysqld_safe mysqld
apt-get --yes purge mysql-server mysql-client
apt-get --yes autoremove --purge
apt-get autoclean
deluser --remove-home mysql
delgroup mysql
rm -rf /etc/apparmor.d/abstractions/mysql /etc/apparmor.d/cache/usr.sbin.mysqld /etc/mysql /var/lib/mysql /var/log/mysql* /var/log/upstart/mysql.log* /var/run/mysqld
updatedb
exit

sudo apt update
sudo apt install mysql-server

# Configuration, including password
sudo mysql_secure_installation

# Connect to MySQL
sudo mysql
mysql> SELECT user,authentication_string,plugin,host FROM mysql.user;
mysql> CREATE USER 'db_username_here'@'localhost' IDENTIFIED WITH caching_sha2_password BY 'db_password_here';
mysql> GRANT ALL PRIVILEGES ON *.* TO 'db_username_here'@'localhost' WITH GRANT OPTION;
mysql> FLUSH PRIVILEGES;

# Test
systemctl status mysql.service
sudo mysqladmin -p -u root version
```

## ERROR 1524 (HY000): Plugin 'caching_sha2_password' is not loaded

* Upgrade to Ubuntu 20 and MySQL 8 to solve issue

## ERROR 1130 (HY000): Host 'ip-172-31-63-251.ec2.internal' is not allowed to connect to this MySQL server

* Need to change host of user from 'localhost' to '%'

```sh
# Connect to MySQL
sudo mysql
mysql> UPDATE mysql.user SET host = '%' WHERE user = 'admin';
mysql> FLUSH PRIVILEGES;
```
