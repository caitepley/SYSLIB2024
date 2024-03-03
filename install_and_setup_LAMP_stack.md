## Part 1: Installing the Apache Web Server
**Apache** is a web server application. Here it is used to display web pages on a web browser in a local machine.

### To install Apache:
Make sure the system is updated first:
```
sudo apt update
sudo apt -y upgrade
```
**Note:** if there is anything to upgrade, the VM will probably want to restart. To do that, run `sudo reboot`

Search for the package to install:
`apt search apache2 | head`
**Note:** in the line above 'head' means to just return the first few results. It is used here so that search doesn't return a bunch of extra stuff.

Show the specifics of the package to install:
`apt show apache2`

Install the package:
`sudo apt install apache2`

See if package is enabled/running:
`systemctl status apache2`
The package should be enabled and running.

### Make a Web Page
To make a web page, a text based web browser needs to be installed on the machine. Here, `w3m` will be used.

**Install w3m** `sudo apt install w3m`

**Visit the default site**
Run `w3m 127.0.0.1` OR `w3m localhost`

**Use your private IP address to run w3m**
Search the local IP address using the command `ip a`, then run `w3m <IP address>`

**Run web page in regular web browser**
Use the server's public IP address from the gcloud console (**the VM's IP address**) to be able to show the web page in a web browser.
Like above, run `w3m <IP address>`

**To create a new web page:**

To create a new file besides the default one, you can create an HTML file on your local machine, under the /var/www/html directory. Then, to access the web page in a browser, you need to specify the IP address and then the file name.

Ex:
```
cd ~
cd /var/www/html
sudo nano example.html
```
Once you have the file open in VIM, you can add whatever HTML you want. Then to view the file in a browser, use the command
```
http://<Private IP address>/example.html
```

## Part 2: Installing & Configuring PHP
PHP is a server-side programming language, which means it must be installed on the server. So, this means that PHP has be installed on a server, but it must also be configured to work with the HTTP server (Apache2).

### To Install PHP:
```
sudo apt install php libapache2-mod-php
sudo systemctl restart apache2
```
To check for errors:
`systemctl status apache2`

## To Check Install:
Create a file called info.php:
```
cd /var/www/html/
sudo nano info.php
```
Add this to the file:
```
<?php
phpinfo();
?>
```
Visit the file using the VM's IP address:
`http://<IP address>/info.php`

The page should look like this:
![image](https://github.com/caitepley/SYSLIB2024/assets/148588703/eff4dad1-2c82-4a6a-9b84-4a3f5e13a988)

**NOTE: use http NOT https when viewing the web pages here

### Basic Configurations
Goal: have Apache2 default to a file titled index.php 
Need to edit the **dir.conf** file in the **/etc/apache2/mods-enabled/** directory.
#### Create a copy of the file as a backup before editing, like so:
```
cd /etc/apache2/mods-enabled/
sudo cp dir.conf dir.conf.bak
sudo nano dir.conf
```
Change the line in the file to this:
`DirectoryIndex index.php index.html index.cgi index.pl index.xhtml index.htm`

#### Test the configuration
`apachectl configtest`
**NOTE:* returns "Syntax Ok" if you did it correctly

#### Reload and Restart Apache2:
```
sudo systemctl reload apache2
sudo systemctl restart apache2
```
### Create an index.php File
Create the file:
```
cd /var/www/html/
sudo nano index.php
```
The code in the file is available in the class text. It works as a browser detector; i.e. it will tell you what browser you are using to run the script.

Once the file is saved, you can run it in the browser by typing this into the browser:
http://<VM's IP Address>
Since the configuration has been changed, it will show the browser detector, rather than the HTML that was at this address initially.

## Part 3: Installing & Configuring MySQL
### Install & Set Up MySQL
Install:
`sudo apt install mysql-server`
Check status:
`systemctl status mysql`
Perform security checks:
`sudo mysql_secure_installation`
Respond to prompts like this:
```
Remove anonymous users: Y
Disallow root login remotely: Y
Remove test database and access to it: Y
Reload privilege tables now: Y
```
Log in to the database to test it. For this, we have to become the root Linux user, like this:
`sudo su`

**Note: we need to be careful when we enter commands on the command line, because it's a largely unforgiving computing environment. But we need to be especially careful when we are logged in as the Linux root user. This user can delete anything, including files that the system needs in order to boot and operate.**

#### Login to MySQL:
Connect to MySQL server as the root user:
`mysql -u root`
`show databases`
To exit:
`\q`

The databases should look like this:
![image](https://github.com/caitepley/SYSLIB2024/assets/148588703/1514370e-f421-4d2c-8ea2-676ad3f0329a)
**Note: If we are logging into the root database account as the root Linux user, we don't need to enter our password.**

### Create & Set Up a Regular User Account
`create user 'opacuser'@'localhost' identified by 'XXXXXXXXX';`
Should return a **Query OK** message.

### Create a Practice Database
```
create database opacdb;
grant all privileges on opacdb.* to 'opacuser'@'localhost';
show databases;
```
To exit the root Linux user account:
```
\q
exit
```
### Logging in as Regular User and Creating Tables
Run:
`mysql -u opacuser -p`
This will prompt you to enter the password set in **Create & Set Up a Regular User Account**

Show the available databases:
```
show databases;
use opacdb;
```
It should return something like this:
![image](https://github.com/caitepley/SYSLIB2024/assets/148588703/f0618fa1-f4df-4ac1-ad2a-3fb468b3c664)

#### Create a table in **opacdb** called **books**
```
create table books (
id int unsigned not null auto_increment,
author varchar(150) not null,
title varchar(150) not null,
copyright date not null,
primary key (id)
);
```

Confirm that the table was created:
```
show tables;
describe books;
```
It should look like this:
![image](https://github.com/caitepley/SYSLIB2024/assets/148588703/e9c82c2b-2c84-465a-bfc7-535fd9cae603)

#### Adding Records into the Table
Use SQL syntax to add records to the table.
Ex:
```
insert into books (author, title, copyright) values
('Jennifer Egan', 'The Candy House', '2022-04-05'),
('Imbolo Mbue', 'How Beautiful We Were', '2021-03-09'),
('Lydia Millet', 'A Children\'s Bible', '2020-05-12'),
('Julia Phillips', 'Disappearing Earth', '2019-05-14');
```
View the records:
`Select * from books;`

#### SQL Commands
**retrieve some records or parts of records:**
Ex: `select title from books;`
Ex: `select title from books where author = 'Stephen King';`

**delete a record:**
Ex: `delete from books where publisher = 'Baker & Taylor';`

**alter the table structure so that it will hold more data**
Ex: `alter table books add publisher varchar(75) after title;`

**add a record:**
Ex: `insert into books
(author, title, publisher, copyright) values
('Emma Donoghue', 'Room', 'Little, Brown \& Company', '2010-08-06');`

### Install PHP and MySQL Support
Install PHP support for MySQL:
`sudo apt install php-mysql php-mysqli`

restart Apache2 and MySql:
```
sudo systemctl restart apache2
sudo systemctl restart mysql
```

#### Create PHP Scripts
Create a login.php file in /var/www/html:
```
cd /var/www/html/
sudo touch login.php
sudo chmod 640 login.php
sudo chown :www-data login.php
ls -l login.php
sudo nano login.php
```
Add the credentials to the file:
```
<?php // login.php
$db_hostname = "localhost";
$db_database = "opacdb";
$db_username = "opacuser";
$db_password = "XXXXXXXXX";
?>
```

Create OPAC file:
`sudo nano opac.php`
Add the code from the class text to the file to display the results of some SQL queries related to the OPAC that was created earlier. Save it and exit nano.

**Test Syntax:**
```
sudo php -f login.php
sudo php -f opac.php
```
This will show the line location of any syntax errors that are caught.
