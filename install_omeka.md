## Install Omeka

### Prerequisites

- Install Imagemagick: `sudo apt install imagemagick`
- Enable Apache mod_rewrite: `sudo a2enmod rewrite`
- Restart Apache: `sudo systemctl restart apache2`

### Steps
**Note:** refer to the 'Installing Wordpress' repository notes and class notes. The process is similar

- Create a new user and a new database in MySQL for Omeka
- Use wget from your server to download Omeka Classic as a Zip file and extract it in /var/www/html:
        - https://github.com/omeka/Omeka/releases/download/v3.1.2/omeka-3.1.2.zip
        - unzip it with the unzip command, which you might have to install with the apt command.
- In the extracted directory, find the db.ini file and add your new database credentials
- Use the chown command. The user and owner should be www-data.
- Restart Apache2 and MySQL
    In your web browser, go to http://your-ip-address/omeka/ and complete the setup via the web form, just like you did with WordPress.

