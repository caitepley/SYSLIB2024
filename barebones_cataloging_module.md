## Creating a Bare Bones Cataloging Module

The goal here is to add a page that expands on the work done in the past couple of modules (see barebones_OPAC.md). The page added here adds a cataloging form to the OPAC created previously. 

**It will look like this:** 

 ![image](https://github.com/caitepley/SYSLIB2024/assets/148588703/a89972dd-2c94-411a-9233-7f203618a1e8)

 ### Creating the HTML Page and a PHP Cataloging Page
 To create the cataloging form page, start by making a directory to hold the files:
 ```
cd /var/www/html
sudo mkdir cataloging
```
then add a file to the directory:
```
cd cataloging
sudo nano index.html
```
**The code to add to 'index.html' is available in the class notes under 'Creating a Bare Bones Cataloging Module'**

To create the .php script to insert new items into the database, a file named `insert.php` needs to be created in the `cataloging` directory. **The code to add to 'insert.php' is also available in the class notes.**

### Adding Security 
To prevent unauthorized users from making changes to the OPAC, a password is needed to give authorized users access.
To create a password for the user 'libcat':
```sudo htpasswd -c /etc/apache2/.htpasswd libcat```

The Apache2 configuration file also needs to be updated to allow password protection. In the `apache2.conf` file, these lines (around line 172) need to be updated to resemble this:
```
<Directory /var/www/>
  Options Indexes FollowSymLinks
  AllowOverride ALL
  Require all granted
</Directory>
```
Create a file called `.htaccess`
```
cd /var/www/html/cataloging
sudo nano .htaccess
```
Add this code to it:
```
AuthType Basic
AuthName "Authorization Required"
AuthUserFile /etc/apache2/.htpasswd
Require valid-user
```
Make sure nothing is broken:
```
apachectl configtest
```
If you get `Syntax OK` you are good to restart it:
```
sudo systemctl restart apache2
systemctl status apache2
```
## Permissions and Ownership
The Apache2 server has a user account on the Linux server. The account name is www-data, which is stored in the /etc/passwd file.
```
grep "www-data" /etc/passwd
www-data:x:33:33:www-data:/var/www:/usr/sbin/nologin
```
Because Apache2 is a user it's file permissions and ownership can be limited.

General guidelines:
- Static files (like HTML, CSS, JS) might not need to be writable by the Apache server, so they could be owned by a different user (like your own user account) but be readable by www-data.
- Directories where Apache needs to write data (like upload directories) or applications that need write access should be owned by www-data.
- Configuration files (incl. files like login.php) should be readable by www-data but not writable, to prevent unauthorized modifications.

How to implement it:
1. Change the group ownership of /var/www/html to www-data:
 ```sudo chown :www-data /var/www/html```

2. Set the setgid bit on /var/www/html. This command makes it so that any new files and directories created within /var/www/html will inherit the group ownership of the parent directory (www-data, in this case). 
 ```sudo chmod -R g+s /var/www/html```

# Now, the system should function as a cataloging module
- opac.php: shows information from the OPAC database
![image](https://github.com/caitepley/SYSLIB2024/assets/148588703/f59ae187-652e-4bab-b343-f4af1a6daa67)

- cataloging/: the form to add new items to the OPAC
![image](https://github.com/caitepley/SYSLIB2024/assets/148588703/79b9bb43-eaf7-4c9a-8167-2e6691cf85bb)

- search.php: form to search for items available in the OPAC
![image](https://github.com/caitepley/SYSLIB2024/assets/148588703/6c74bca6-12dd-4675-afed-8861e5b28042)

![image](https://github.com/caitepley/SYSLIB2024/assets/148588703/0ea0a020-a443-40c8-a7e2-accf8a52e35d)

**The opacdb MySQL database can still be used to search, add to, edit, and delete from the database. 
![image](https://github.com/caitepley/SYSLIB2024/assets/148588703/3aedd2c3-1c56-400d-9d8c-e3674b1ca29b)
