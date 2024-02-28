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
Use the server's public IP address from the gcloud console (the VM's IP address) to be able to show the web page in a web browser.
Like above, run `w3m <IP address>`


## Part 2: Installing & Configuring PHP

## Part 3: Installing & Configuring MySQL
