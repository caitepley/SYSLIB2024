## Install Wordpress

General instructions (not the ones I actually used): [Install Wordpress](https://developer.wordpress.org/advanced-administration/before-install/howto-install/ )

### Requirements:
WordPress installation requires at least PHP version 7.4 and MySQL version 5.7

To check that the system meets the requirements:
```
php --version
mysql --version
```
Add some PHP modules so that Wordpress works better:
```
sudo apt install php-curl php-xml php-imagick php-mbstring php-zip php-intl
```
Restart:
```
sudo systemctl restart apache2
sudo systemctl restart mysql
```

### Download & Extract the Wordpress Software:
```
cd /var/www/html
sudo wget https://wordpress.org/latest.tar.gz
sudo tar -xzvf latest.tar.gz
```

### Create the Database & a User
Switch to root and log in to MySQL
```
sudo su
mysql -u root
```
Create the database and a user:
```
create user 'wordpress'@'localhost' identified by 'XXXXXXXXX';
create database wordpress;
grant all privileges on wordpress.* to 'wordpress'@'localhost';
show databases;
\q
```

### Set up wp-config.php
To have password functionality, we need this file
Toe create this file in the correct directory:
```
cd /var/www/html/wordpress
sudo cp wp-config-sample.php wp-config.php
sudo nano wp-config.php
```
Disable FTP uploads:
```
define('FS_METHOD','direct');
```

### Change File Ownership
WordPress will need to write to files in the base directory
```
sudo chown -R www-data:www-data /var/www/html/wordpress
```

### Run the Install Script
```
http://11.111.111.11/wordpress/wp-admin/install.php
```

### Finishing Up
Now Wordpress should be installed. If done correctly, there will be instructions on the browser page to set up the account and a webpage. Now, the browser can be used to edit the site.
