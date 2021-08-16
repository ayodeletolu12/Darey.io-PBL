# MEAN WEB STACK DEPLOYEMENT TO UBUNTU SERVER IN AZURE
# MEAN STACK is a combination of the following components
1. MongoDB(Document database)
2. Express (Backend application framework) - makes requests to Database for Reads and Write
3. Angular (Frontend application framework) - Handles Client and Server Requests
4. Node.js (Javascript runtime environment)- Accepts requests and displays result to the end user

# : LAUNCH MY AZURE VIRTUAL MACHINE ON UBUNTU SERVER 20.4

##### Update your Ubuntu server repository
```
  $ sudo apt update
  $ sudo apt upgrade
```  
### TASK: We are going to implement a simple Book Register web form using MEAN stack.

# STEP 1: Install Node JS, Node.js is a javascript runtime built on Chrome's V8 Javascript engine. In this project Node.js is used to set up the Express route and Angular JS controllers
```
 sudo apt install -y nodejs
```
# STEP 2: Install MongoDB
```
sudo apt install -y mongodb
```
#### Start the Server so that the daemon, the services that need to run from the background to make the app works fine is started
```
sudo systemctl start mongodb
```
#### Verify that the service is up and running
```
sudo systemctl status mongodb
```
![Screenshot from 2021-08-16 19-43-43](https://user-images.githubusercontent.com/56724044/129620662-1fd0743f-077a-471a-9268-43b232993faf.png)

#### Install some dependencies, that our application will depend on to work fine. Install Node Package Manager(NPM) npm is used to install packages for Node js
```
sudo apt install -y npm
```
#### Install "body-parser package: we need "body-parser" package to help us process JSON files passed in requests to the server.
```
sudo npm install body-parser
```
### Create a root directory where we are going to build our Application, we are going to make directory called Books
```
mkdir Books && cd Books
```
#### In the Books directory, we will initialize npm project
```
npm init
```
#### Add a file to it named server.js
```
vim server.js
```


