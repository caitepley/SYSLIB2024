## Managing Software
Package Manager -  handles the installation, upgrades, and uninstalls of the software on a system. Ubuntu uses a package manager called `dpkg` which uses `apt` on the user-end.

`Sudo` - execute a command as another user. Defaults to superuser. Sometimes needed to create and/or modify files and directories or to manage software.
Ex: `sudo mkdir example`

`apt` - advanced package tool. User end of the Ubuntu package manager, `dpkg`.

`sudo apt update` - lets you know if there is any software on your system that can be updated. Good to run before installing/modifying software so that the system is up-to-date.

`sudo apt upgrade` - upgrades any/all software that is not up-to-date to the newest version.

`apt search` - returns all package names with the argument provided in the package name.
Ex: `apt search tldr` returns all packages that have 'tldr' included in their name.

`apt show` - shows more specific information about a package so that you can make sure it's what you need before you install it.
Ex: `apt show tldr` shows the specifics for the 'tldr' package.

`sudo apt install` - installs the specified package 
Ex: `sudo apt install tldr`

`sudo apt remove` - removes the specified package from your system. **Note:** adding --purge to the command will remove the configuration files for the package.
Ex: `sudo apt --purge remove tldr'

`sudo apt autoremove` - uninstalls the dependencies (other software necessary to run a package that is not included in the package) for the package that you are removing. 

`sudo apt clean` - removes extra files to free up space.

### Installing Bat
To search for the `bat` application, I first used the command `apt search bat` to see what all packages exist with 'bat' in the name. I then used `apt show bat` to see a summary of the application to see if it was what I was meaning to install.
Once I confirmed that is was what I wanted, I ran `sudo apt install bat` and installed the package. 

Once the package was installed, the command `batcat example.txt` was used to create this output:
![image](https://github.com/caitepley/SYSLIB2024/assets/148588703/c59c95d4-94dd-4b08-9e6a-5237e6a82303)
This is pretty cool because it shows file contents (like the `cat` command) but with the formatting and line numbers you would see if you opened the file in a text editor. 

## Library Search
