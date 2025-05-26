# Ubuntu Server Commands Cheat Sheet

## General System Management :computer:
```bash
# Check Ubuntu version
lsb_release -a

# Update & Upgrade system
sudo apt update && sudo apt upgrade -y

# Reboot system
sudo reboot

# Check system uptime
uptime

# Monitor real-time logs
sudo journalctl -xe
sudo tail -f /var/log/syslog

# Check disk space usage
df -h

# Check memory usage
free -m
````

## Services Management \:gear:

```bash
# Check service status
sudo systemctl status <service>

# Start / Stop / Restart / Reload a service
sudo systemctl start <service>
sudo systemctl stop <service>
sudo systemctl restart <service>
sudo systemctl reload <service>

# Enable service on boot
sudo systemctl enable <service>
sudo systemctl disable <service>

# List all active services
sudo systemctl list-units --type=service
```

## Apache Web Server \:satellite:

```bash
# Check Apache version
apache2 -v

# Test Apache configuration
sudo apache2ctl configtest

# List enabled sites
ls /etc/apache2/sites-enabled/

# Enable/Disable site
sudo a2ensite example.conf
sudo a2dissite example.conf

# Enable/Disable Apache modules
sudo a2enmod rewrite
sudo a2dismod php8.1

# Check Apache error logs
sudo tail -f /var/log/apache2/error.log

# Restart Apache service
sudo systemctl restart apache2
```

## PHP \:keyboard:

```bash
# Check PHP version
php -v

# List installed PHP modules
php -m

# Check PHP-FPM status (if used)
sudo systemctl status php8.1-fpm

# Modify PHP settings
sudo nano /etc/php/8.1/apache2/php.ini

# Restart PHP-FPM
sudo systemctl restart php8.1-fpm

# Switch PHP versions
sudo update-alternatives --set php /usr/bin/php7.4
```

## MariaDB \:floppy\_disk:

```bash
# Check MariaDB version
mysql -V

# Log in to MariaDB
sudo mariadb -u root -p

# Show databases and users
SHOW DATABASES;
SELECT user, host FROM mysql.user;

# Check MariaDB service status
sudo systemctl status mariadb

# Secure MariaDB installation
sudo mysql_secure_installation

# Create a new database
CREATE DATABASE mydatabase;

# Create a user and grant privileges
CREATE USER 'username'@'localhost' IDENTIFIED BY 'password';
GRANT ALL PRIVILEGES ON mydatabase.* TO 'username'@'localhost';
```

## Pure-FTPd \:package:

```bash
# Check Pure-FTPd version
pure-ftpd --version

# Check FTP server status
sudo systemctl status pure-ftpd

# Add a new FTP user
sudo pure-pw useradd <username> -u ftpuser -d /var/www/html
sudo pure-pw mkdb

# List FTP users
sudo pure-pw list

# Force reload
sudo systemctl restart pure-ftpd

# Set passive FTP port range
sudo nano /etc/pure-ftpd/pure-ftpd.conf
# Set passive ports:
PassivePortRange 30000 35000
```

## BIND (DNS Server) \:earth\_africa:

```bash
# Check BIND version
named -v

# Check BIND service status
sudo systemctl status bind9

# Check config syntax
sudo named-checkconf
sudo named-checkzone yourdomain.com /etc/bind/db.yourdomain.com

# Reload BIND
sudo systemctl reload bind9

# View logs
sudo tail -f /var/log/syslog | grep named

# Check DNS resolution
dig yourdomain.com
```

## Postfix (Mail Server) \:envelope:

```bash
# Check Postfix version
postconf -d

# Check status
sudo systemctl status postfix

# View mail queue
mailq

# Flush mail queue
sudo postfix flush

# Reconfigure Postfix
sudo dpkg-reconfigure postfix

# Check mail logs
sudo tail -f /var/log/mail.log
```

## Dovecot (IMAP/POP3) \:mailbox\_with\_mail:

```bash
# Check Dovecot version
doveadm --version

# Check status
sudo systemctl status dovecot

# Test IMAP login (replace with real user)
openssl s_client -connect localhost:993

# View logs
sudo tail -f /var/log/mail.log

# Restart Dovecot service
sudo systemctl restart dovecot

# List Dovecot mailboxes
doveadm mailbox list
```

## ISPConfig \:globe\_with\_meridians:

```bash
# Check ISPConfig version
sudo ispconfig_update.sh --version

# Access ISPConfig panel
https://your-server-ip:8080

# Restart ISPConfig services
sudo /usr/local/ispconfig/server/server.sh

# Check ISPConfig logs
sudo tail -f /var/log/ispconfig/ispconfig.log
```

## Firewall (UFW) \:shield:

```bash
# Check UFW version
ufw version

# Allow necessary ports
sudo ufw allow 22      # SSH
sudo ufw allow 80      # HTTP
sudo ufw allow 443     # HTTPS
sudo ufw allow 21      # FTP
sudo ufw allow 53      # DNS
sudo ufw allow 25      # SMTP
sudo ufw allow 993     # IMAPS

# Enable firewall
sudo ufw enable

# View rules
sudo ufw status

# Check firewall status
sudo ufw status verbose

# Disable firewall (if necessary)
sudo ufw disable
```

## Logs Locations \:bookmark\_tabs:

| Service   | Log File                           |
| --------- | ---------------------------------- |
| Apache    | `/var/log/apache2/error.log`       |
| MariaDB   | `/var/log/mysql/error.log`         |
| Pure-FTPd | `/var/log/syslog (or custom)`      |
| BIND      | `/var/log/syslog`                  |
| Postfix   | `/var/log/mail.log`                |
| Dovecot   | `/var/log/mail.log`                |
| ISPConfig | `/var/log/ispconfig/ispconfig.log` |

---

© 2025 Ubuntu Server Cheat Sheet
