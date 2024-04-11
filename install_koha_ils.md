# Installing Koha ILS

### Create a Firewall in Gcloud
- Click on the ☰ icon at the top left.
- Click on VPN Network
- Click on Firewall
- Choose Create a firewall rule
    * Add name: koha
    * Add description: open port 8080
- Next to Targets, click on All instances in the network
- In the Source IPv4 ranges, add 0.0.0.0/0
- Click on Specified protocols and ports
    * Click on TCP
    * Add 8080 in the Ports box
- Click on Create

### Install Koha Repo
#### Server setup 
Run:
```
Server setup
sudo apt upgrade
sudo apt autoremove -y && sudo apt clean
sudo apt install gnupg2
```
Restart:
```
sudo reboot now
```

### Add Koha Repository
Log in as root user:
```
sudo su
```
Add the Koha repository to server:
```
echo 'deb http://debian.koha-community.org/koha stable main' | sudo tee /etc/apt/sources.list.d/koha.list
```
Add the digital signature that verifies the above repo:
```
wget -q -O- https://debian.koha-community.org/koha/gpg.asc | sudo apt-key add -
```

### Install Koha
```
apt update
apt show koha-common
apt install koha-common
```

### Configure Koha
Edit some configuration files for Koha:
```
nano /etc/koha/koha-sites.conf
```
Change `INTRAPORT="80"` to `INTRAPORT="8080"`

Install and setup mysql-server:
```
sudo apt install default-mysql-server
mysqladmin -u root password bibliolib1
a2enmod rewrite
a2enmod cgi 
```
Restart Apache2:
```
systemctl restart apache2
```
Create a database for Koha:
```
koha-create --create-db bibliolib
```
Tell Apache to listen on port 8080:
```
nano /etc/apache2/ports.conf 
```
then
```
Listen 8080
```
Test for validity:
```
apachectl configtest
```
Restart:
```
systemctl restart apache2
```
Disable the default Apache2 setup, enable traffic compression using deflate, enable the bibliolib site, and then reload Apache2's configurations and restart again:
```
a2dissite 000-default
a2enmod deflate
a2ensite bibliolib
systemctl reload apache2
systemctl restart apache2
```
### Koha Web Installer
```
nano /etc/koha/sites/bibliolib/koha-conf.xml
```
then:
```
http://IP-ADDRESS:8080
```

### Public OPAC
To make a public facing OPAC:
- Click on More in the top drop down box
- Click on Administration
- Click on Global System Preferences
- Click on OPAC in the left hand side bar
- Scroll down to OPACBaseURL 
- Enter the IP address of the server: http://IP-ADDRESS
- Save all OPAC Preferences
Once this has been done, the public facing OPAC should be available at the server's IP address.
