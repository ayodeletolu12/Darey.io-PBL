# Darey.io-PBL
Darey.io PBL Projects implementation


# PROJECT 1: WEB STACK IMPLEMENTATION (LAMP STACK) IN AZURE 

## STEP 1 INSTALL APACHE WEB SERVER ON A LINUX UBUNTU SERVER

   ##### STEP A — Connect from my Linux terminal to the Linux Ubuntu 20.4 remote server using SSH : 
```
~$ ssh tolulope@remote_IP_Address

```

##### STEP B - Ensure that the ubuntu server repository is updated and packages upgraded

```
~$ sudo apt update
~$ sudo apt upgrade

```

##### STEP C — INSTALLING APACHE AND UPDATING THE FIREWALL
Install and upgrade Apache on the remote server
$ sudo apt install apache2
$ sudo apt upgrade apache2

##### Step D - Check that Apache2 is running on your server
$ sudo systemctl status apache2
![image](https://user-images.githubusercontent.com/56724044/127899991-f6ffa41f-405d-49b3-80ea-657da17d5a8c.png)

##### Step E - Check that the installation is successful
	Go to the browser and enter the the localhost or server IP address
Once the Apache home page displays, thats show that the whole installation is successful on the remote server
![image](https://user-images.githubusercontent.com/56724044/127900667-9f2836af-bd99-4889-ac6a-eddbf5b21046.png)


## STEP 2 — INSTALLING MYSQL

##### STEP A - Install the mysql-server on your linux remote server as one of the component of LAMP stack
$ sudo apt install mysql-server

##### Step C - After the installation, run a security script that comes pre-installed with Mysql
	$ sudo mysql_secure_installation
##### Step D - After installing the security script, check that mysql is successfully installed on the server
	$ sudo mysql
![image](https://user-images.githubusercontent.com/56724044/127902121-de3b75de-fe54-4c8a-b71c-60755b3b9467.png)

## STEP 3 — INSTALLING PHP
**PHP** is the component of the **LAMP setup** that will process code to display dynamic content to the end user. In addition to the php package, we will need **php-mysql**, a PHP module that allows PHP to communicate with MySQL-based databases. and **libapache2-mod-php** to enable Apache to handle PHP files. Core PHP packages will automatically be installed as dependencies.

##### Step A: To install this 3 packages/modules at once
$ sudo apt install php php-mysql libapache2-mod-php

##### Once the installation is finished, you can run the following command to confirm your PHP version:
$ php -v
![image](https://user-images.githubusercontent.com/56724044/127903387-5320fa22-3297-4b66-870c-4b82d1d95e68.png)

At this point, my LAMP stack is completely installed and fully operational on my ubuntu remote server.


# TESTING MY SET UP WITH A PHP SCRIPTS.
This will be set up by creating a Apache Virtual Host, this enables me to create multiple websites to hold websites files and folders on a single machine.

# STEP 4 — CREATING A VIRTUAL HOST FOR MY WEBSITE USING APACHE
Apache web server has a default server block enabled to serve documents in **_/var/www/html directory_**. For me to add multiple websites, I will create multiple directories in the /var/www/directory
I will set up a domain called **tolulopeinfotech.com**

##### Step A: Create a directory for my domain / website in the root directory /var/www/
$ sudo mkdir -p /var/www/tolulopeinfotech

##### Step B: Assign ownership permission to the user that might want to access the directory i.e. Next, assign ownership of the directory with your current system user:
sudo chown -R $USER:$USER /var/www/tolulopeinfotech

##### Step C: Step 3: Create configuration file to serve the website in the root directory
I need to create a configuration file in **Apache’s sites-available directory** using any text editor of my choice. 
Go back to the root directory, inside the /etc/apache2/sites-available directory, you will see the default config 000-default.conf. this default serves the default apache webpage after installation. We need to create a new config file for the website (tolulopeinfotech) 
$ cd /
$ sudo cd /etc/apache2/sites-available
$ sudo vim tolulopeinfotech.conf    OR
$ sudo vim  /etc/apache/sites-available/tolulopeinfotech.conf
![image](https://user-images.githubusercontent.com/56724044/127907360-40442155-e280-496b-b2ff-c4543e9f2b56.png)

##### Step D: to be sure that the .conf file is in the right directory, You can use the ls command to show the new file in the sites-available directory
sudo ls /etc/apache2/sites-available
![image](https://user-images.githubusercontent.com/56724044/127907696-9e473297-2e7f-4f6d-8124-5da3c267cbb0.png)

With this my VirtualHost configuration, I am telling Apache to serve tolulopeinfotech using /var/www/tolulopeinfotech as its web root directory. If you would like to test Apache without a domain name, you can remove or comment out the options ServerName and ServerAlias by adding a # character in the beginning of each option’s lines. Adding the # character there will tell the program to skip processing the instructions on those lines.

##### Step E: Now that our .conf file is fine, we need to disable the default apache config file 000-default.conf and enable my tolulopeinfotech.conf so that Apache will not go and pick the default config. Apache’s default configuration would overwrite your virtual host. To disable Apache’s default website use a2dissite command 
$ sudo a2dissite 000-default

##### Step F: I can now enable my custom config file
_$ sudo a2ensite tolulopeinfotech
![image](https://user-images.githubusercontent.com/56724044/127908423-cfef08ad-d5b9-42a3-b5b3-a4d06bcda485.png)

##### Step G: Next thing is to reload my Apache web server. The reload will reload the config file
_$ sudo systemctl reload apache2

##### Create a new index.html for my website
My new website is now active, but the web root /var/www/tolulopeinfotech is still empty. I will create an index.html file in that location so that I can test that the virtual host works as expected:
_$ sudo echo "Hello LAMP STACK from hostname" > /var/www/tolulopeinfotech/index.html
check the browser and again, the Apache default page shouldn't be showing again.

# STEP 5 — ENABLE PHP ON THE WEBSITE
With the default DirectoryIndex settings on Apache, a file named index.html will always take precedence over an index.php file

This is useful for setting up maintenance pages in PHP applications, by creating a temporary index.html file containing an informative message to visitors. Because this page will take precedence over the index.php page, it will then become the landing page for the application. Once maintenance is over, the index.html is renamed or removed from the document root, bringing back the regular application page.

In case you want to change this behavior, you’ll need to edit the default configuration file **/etc/apache2/mods-enabled/dir.conf** file and change the order in which the index.php file is listed within the DirectoryIndex directive:
This can be achieved from the etc/apache2/mods-enabled directory, edit the dir.conf

**_$ sudo vim /etc/apache2/mods-enabled/dir.conf**
You are simply going to change the precedence. index.php before index.html
![image](https://user-images.githubusercontent.com/56724044/127913052-d94f2ef7-b752-444a-87e6-9f57357a3904.png)


Reload the Apache for the config to take effect
**_$ sudo systemctl reload apache2**

Finally, I will create a PHP script to test that PHP is correctly installed and configured on my server.

Now that I have a custom location to host your website’s files and folders, I will create a PHP test script to confirm that Apache is able to handle and process requests for PHP files.

##### Step A Create a new file named index.php inside your custom web root folder: /var/www/tolulopeinfotech/index.php
$ sudo vim /var/www/tolulopeinfotech/index.php
This will open a blank file. Add the following text, which is valid PHP code, inside the file:
```
<?php
phpinfo();

```






