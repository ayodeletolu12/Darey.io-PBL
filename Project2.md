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



