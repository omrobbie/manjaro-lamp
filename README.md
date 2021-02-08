# LAMP Installation Guide
> Linux, Apache, MySQL, and PHP.
<br>

## Linux
1. Synchronizing package databases
```bash
sudo pacman -Syyu
```
<br>

## Apache
1. Install Apache
```bash
sudo pacman -S apache
```
2. Edit httpd configuration file
```bash
sudo nano /etc/httpd/conf/httpd.conf
```
3. Make sure mod_unique_id is commented
```bash
#LoadModule unique_id_module modules/mod_unique_id.so
```
4. Enable httpd service, and make sure it is run
```bash
sudo systemctl enable --now httpd
sudo systemctl status httpd
```
5. Test Apache server by writing simple html file on `/srv/http` folder
```bash
sudo nano /srv/http/index.html
```
<br>

## MySQL
1. Install MySQL
```bash
sudo pacman -S mysql
```
2. Initialize data folder to start the MySQL service
```bash
sudo mysql_install_db --user=mysql --basedir=/usr --datadir=/var/lib/mysql
```
3. Enable mysqld service, and make sure it is run
```bash
sudo systemctl enable --now mysqld
sudo systemctl status mysqld
```
4. Set root password if needed
```bash
sudo mysql_secure_installation
```
<br>

## PHP
1. Install PHP
```bash
sudo pacman -S php php-apache
```
2. Edit httpd configuration file
```bash
sudo nano /etc/httpd/conf/httpd.conf
```
3. Comment and uncomment these lines
```bash
#LoadModule mpm_event_module modules/mod_mpm_event.so
LoadModule mpm_prefork_module modules/mod_mpm_prefork.so
```
4. Add this lines at the bottom
```bash
LoadModule php7_module modules/libphp7.so
AddHandler php7-script php
Include conf/extra/php7_module.conf
```
5. Test PHP on Apache server by writing simple php file on `/srv/http` folder
```bash
sudo nano /srv/http/index.html
```
<br>

# All sets!
We can also install phpmyadmin if needed or just use another mysql GUI like MySQL Workbench, DBeaver, etc.
