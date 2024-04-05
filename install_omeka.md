## Install Omeka

### Prerequisites

- Install Imagemagick: `sudo apt install imagemagick`
- Enable Apache mod_rewrite: `sudo a2enmod rewrite`
- Restart Apache: `sudo systemctl restart apache2`

### Steps
**Note:** refer to the 'Installing Wordpress' repository notes and class notes. The process is similar

- Create a new user and a new database in MySQL for Omeka
- Use wget from your server to download Omeka Classic as a Zip file and extract it in /var/www/html:
    * https://github.com/omeka/Omeka/releases/download/v3.1.2/omeka-3.1.2.zip
    * unzip it with the unzip command, which you might have to install with the apt command.
- In the extracted directory, find the db.ini file and add your new database credentials
- Use the chown command. The user and owner should be www-data.
- Restart Apache2 and MySQL
    * In your web browser, go to http://your-ip-address/omeka/
    * For admin side, go to http://your-ip-address/omeka/admin/

### Using Omeka
Once the installation is complete, the admin dashboard will allow you to make an account and then start adding items. 
The theme of the public page can also be changed in the admin dashboard. 

Here is my admin dashboard. I added a few items and created a collection:
![image](https://github.com/caitepley/SYSLIB2024/assets/148588703/56297523-1f59-4785-a580-13432aa6d14f)

Here is the public view of the items that I added:
![image](https://github.com/caitepley/SYSLIB2024/assets/148588703/20df166d-5dda-48bb-aeb8-4846c98d98e2)

