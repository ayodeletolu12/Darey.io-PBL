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



