# Darey.io-PBL
Darey.io PBL Projects implementation


# PROJECT 1: WEB STACK IMPLEMENTATION (LAMP STACK) IN AZURE 

## STEP 1 INSTALL APACHE WEB SERVER ON A LINUX UBUNTU SERVER

   ##### STEP A — Connect from my Linux terminal to the Linux Ubuntu 20.4 remote server using SSH : 
~$ ssh tolulope@remote_IP_Address

##### STEP B - Ensure that the ubuntu server repository is updated and packages upgraded
~$ sudo apt update
~$ sudo apt upgrade

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









