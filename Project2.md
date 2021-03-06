# WEB STACK IMPLEMENTATION (LEMP STACK) USING AWS

##### Enusre you SSH to the remote server from the Linux terminal

##### Once you have securely connected to the remote server on AWS
**Ensure that your Ubuntu server repository is updated and upgraded**
```
$ sudo apt install
$ sudo apt upgrade
```
# STEP 1 INSTALL NGINX WEB SERVER ON A LINUX UBUNTU SERVER ON AWS

##### STEP A — INSTALLING NGINX WEB SERVER ON THE UBUNTU SERVER
Install nginx web server on the remote server
```
$ sudo apt install nginx
```
##### STEP B — Confirm that Nginx is installed, active and running
```
$ sudo systemctl status nginx
```
![image](https://user-images.githubusercontent.com/56724044/128054587-98100c84-976a-4b7b-906c-d0d3e024bfb9.png)

##### Ensure from the security group in AWS that port 80 is allowed in order to receive traffic from the web browser
![image](https://user-images.githubusercontent.com/56724044/128057324-72ffa1b9-d238-4ce4-a5c8-2036265663dc.png)

##### STEP C - Go to the broswer enter your server IP Address to access the Nginx web page
![image](https://user-images.githubusercontent.com/56724044/128057659-8d001870-3e45-47f4-ab3a-365df8dddeb7.png)

# STEP 2 — INSTALLING MYSQL AS PART OF THE LEMP STACK COMPONENT
##### STEP A - Install the mysql-server on your linux remote server as one of the component of LAMP stack
```
$ sudo apt install mysql-server
```
##### Step C - After the installation, run a security script that comes pre-installed with Mysql

```
$ sudo mysql_secure_installation
```

Step D - After installing the security script, check that mysql is successfully installed on the server
```
$ sudo mysql
```
# STEP 3 – INSTALLING PHP
##### Installing php the last component of the lemp stack web technology
I have Nginx installed to serve my contents and MySQL installed to store and manage your data. Now the next component to be installed is the PHP to process code and generate dynamic content for the web server.

While Apache embeds the PHP interpreter in each request, **Nginx** requires an external program to handle PHP processing and act as a bridge between the PHP interpreter itself and the web server. **This allows for a better overall performance in most PHP-based websites,** but it requires additional configuration. I will need to install `php-fpm`, which stands for **“PHP fastCGI process manager”**, and tell Nginx to pass PHP requests to this software for processing. Additionally, I will need php-mysql, a PHP module that allows PHP to communicate with MySQL-based databases. Core PHP packages will automatically be installed as dependencies.

##### To install these 2 packages at once, run:
```
sudo apt install php-fpm php-mysql
```
# A BLOCKER WAS MET AFTER COMPLETE INSTALLATION
After the installation of PHP and the external program php-fpm, Apache2 default home page was now overriding NGINX without installing Apache on the server.
Despite uninstalling the PHP program from the server, the webpage was still showing the default Apache2 webpage instead of NGINX

#### Resolution
It appears that the PHP-fpm also installs Apache2 unto the server automatically hence Nginx listening on the same port with apache2 by default

Uninstall Apache from the server
```
$ sudo service apache2 stop
$ sudo apt-get purge apache2 apache2-utils apache2-bin apache2.2-common
$ sudo apt-get autoremove
$ whereis apache2
apache2: /etc/apache2ml
$ sudo rm -rf /etc/apache
```
After removing Apache from the server. Nginx was now showing as thge default web page on the browser

# STEP 4 — CONFIGURING NGINX TO USE PHP PROCESSOR
On Ubuntu 20.04, Nginx has one server block enabled by default and is configured to serve documents out of a directory at **web root /var/www/html.** While this works well for a single site, it can become difficult to manage if you are hosting multiple sites. Instead of modifying **/var/www/html**, we’ll create a directory structure within /var/www for the my domain website,I will be using projectlemp leaving /var/www/html in place as the default directory to be served if a client request does not match any other sites.

##### Step A - Create the web root directoy that will serve the domain web files and folder
```
$ sudo mkdir -p /var/www/projectlemp
```
##### Step B - Assign ownership permission to the domain web root directory with the $USER environment variable. This will reference your current system user
```
$ sudo chown -R $USER:$USER /var/www/projectlemp
```
##### Step C - Create a new configuration file in Nginx's sites-available
Nginx has default configuration in sites-available directory
```
$ sudo ls /etc/nginx/sites-available ------- You will see the nginx default config file
```
# You need to create a new config file for the website: 
#https://www.nginx.com/resources/wiki/start/
#https://www.nginx.com/resources/wiki/start/topics/tutorials/config_pitfalls/
#https://wiki.debian.org/Nginx/DirectoryStructure
#Please see /usr/share/doc/nginx-doc/examples/ for more detailed examples.

```
$ sudo nano /etc/nginx/sites-available/projectLEMP
```
![image](https://user-images.githubusercontent.com/56724044/128130796-04179e5a-250f-4568-8030-c8523d451079.png)

##### Step D - Ensure the newly created config file is activated, this is done by linking the config to Nginx sites-enabled directory in etc
Activate your configuration by linking to the config file from Nginx’s sites-enabled directory:
```
sudo ln -s /etc/nginx/sites-available/projectLEMP /etc/nginx/sites-enabled/
```
before linking the new config file,you will only see the Nginx default config in the site-enabled directory because its enabled by default /etc/nginx/sites-enabled/default.
After linking the new config file to the sites-enabled directory, the new config file will now show in sites-enabled directory
![image](https://user-images.githubusercontent.com/56724044/128132125-bf7a0c65-fe9d-4dbc-a511-fb1ea9fc462a.png)
**Test that the configuration syntax is okay.** ``` sudo nginx -t ```
![image](https://user-images.githubusercontent.com/56724044/128132452-424ac09e-43d8-4e72-b350-8865ff12116a.png)

##### Step E - We need to disable the default config so that Nginx can serve our website config
We also need to disable default Nginx host that is currently configured to listen on port 80, for this we will run:
```
$ sudo unlink /etc/nginx/sites-enabled/default
```
You can check that the default nginx config file is no longer in the site-enabled directory
```
$ sudo ls /etc/nginx/sites-enabled
```
##### Step F - When everything looks fine, reload Nginx to apply the changes made in the configuration directory
```
$ sudo system reload nginx
```
My new website is now active, but the web root /var/www/projectLEMP is still empty. I will create an index.html file in that location so that we can test that my new server block works as expected:
```
sudo echo 'Hello LEMP from hostname' $(curl -s http://169.254.169.254/latest/meta-data/public-hostname) 'with public IP' $(curl -s http://169.254.169.254/latest/meta-data/public-ipv4) > /var/www/projectLEMP/index.html
```
# STEP 5 – TESTING PHP WITH NGINX
By now my LEMP stack is completely set up. I need to confirm that Nginx can handle php files to php processor.
Let's create a php file
```
$ sudo nano /var/www/projectLEMP/info.php
```
```
<?php
phpinfo();
```
In order to confirm that nginx is serving php file to the preprocessor, go back to the browser and enter ipaddress/info.php
or you change the preference in the nginx config file for the domain website

# STEP 6 – RETRIEVING DATA FROM MYSQL DATABASE WITH PHP (CONTINUED)
Here I will create a test database (DB) with simple "To do list" and configure access to it, so the Nginx website would be able to query data from the DB and display it.

We will create a new user with the **mysql_native_password authentication method** in order to be able to connect to the MySQL database from PHP.

We will create a database named **myfirst_database and a user named tolulope**.

##### Step A - First, connect to the MySQL console using the root account:
```
sudo mysql
```
##### Step B - To create a new database, run the following command from your MySQL console:
```
mysql> CREATE DATABASE `myfirst_database`;
```
##### Step C - Now you can create a new user using mysql_native_password as default authentication method. and grant him full privileges on the database you have just created.
```
mysql>  CREATE USER 'tolulope'@'%' IDENTIFIED WITH mysql_native_password BY 'password';
```
##### Step D - Now we need to give this user permission over the myfirst_database database:
```
mysql> GRANT ALL ON myfirst_database.* TO 'tolulope'@'%';
```
This will give user **tolulope** full privileges over the myfirst_database database, while preventing this user from creating or modifying other databases on your server.

Now exit the MySQL shell with:
```
mysql> exit
```
You can test if the new user has the proper permissions by logging in to the MySQL console again, this time using the custom user credentials:
```
mysql -u tolulope -p
```
Notice the -p flag in this command, which will prompt you for the password used when creating the tolulope user. After logging in to the MySQL console, confirm that you have access to the myfirst_database database:
```
mysql> SHOW DATABASES;
```
![image](https://user-images.githubusercontent.com/56724044/128232755-4345af13-23ae-4ecb-85f4-a3ae2f83c3b9.png)
