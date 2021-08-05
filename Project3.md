# WEB STACK WITH TO-DO IMPLEMENTATION/SOLUTION BASED ON MERN IN AWS CLOUD
### M - Mongo DB ----------- Database
### E - Express JS ---------- Node JS server side framework
### R - React JS ------------ Client side
### N - Node JS ------------- Server side

Spin your EC2 install with Ubuntu 20.04 server

# STEP 1 – BACKEND CONFIGURATION

##### Update ubuntu
```
$ sudo apt update
```
##### Upgrade ubuntu
```
sudo apt upgrade
```
##### Step A - Lets get the location of Node.js software from Ubuntu repositories.
```
$ sudo curl -sL https://deb.nodesource.com/setup_12.x | sudo -E bash -
```
##### Step C - Install Node.js on the server, the command will also install Node.js 12.x and npm
```
$ sudo apt-get install -y nodejs
```
NPM is a package manager for Node like apt for Ubuntu, it is used to install Node modules & packages and to manage dependency conflicts.
After the installation, you can verify the node installation with the command below
```
$ node -v
$ npm -v
```
![image](https://user-images.githubusercontent.com/56724044/128393132-a5bbe16d-bc17-473e-94ce-0e0194a3194b.png)

##### Application Code Setup
Create a new directory for your To-Do project:
```
$ mkdir Todo
```
Run the command below to verify that the Todo directory is created with ls command
```
ls
```
