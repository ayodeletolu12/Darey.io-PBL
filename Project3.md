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
![image](https://user-images.githubusercontent.com/56724044/128394208-30dae36c-e9ea-404a-a4b4-bc2e97ad1eb3.png)

Now I will change current directory to the newly created one:
```
$ cd Todo
```
##### Step D - It is important you initialize the application project with npm init, this will actually create a file named package.json. This package.json will normally contain information about the application and the dependencies that it needs to run.
```
$ npm init
```
![image](https://user-images.githubusercontent.com/56724044/128399534-799ae92d-258a-4582-99ec-4a48b2b7c317.png)

##### You need to check that package.json is now in the directory after initializing the project directory
still within the Todo directory, run this command
```
ls
```
![image](https://user-images.githubusercontent.com/56724044/128409027-7be6b576-cb8b-4e59-b6f6-06c964fe427e.png)

# STEP 2 - INSTALL EXPRESSJS
Expressjs is a framework for Node.js, therefore a lot of things developers would have programmed is already taken care of out of the box.
To use express js, install it using npm. Remember that is the package manager for Node js.
```
$ npm install express
```
![image](https://user-images.githubusercontent.com/56724044/128410870-91d16d5f-3df8-44c2-b233-d6b0674a6887.png)

##### Step A - Now create a file index.js with the command below
```
$ touch index.js
```
##### Step B - Install dotenv module
```
$ npm install dotenv
```
Open the index.js file with the command below
```
$ vim index.js
```