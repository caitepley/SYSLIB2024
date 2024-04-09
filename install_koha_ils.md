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
