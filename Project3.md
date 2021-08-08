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
![image](https://user-images.githubusercontent.com/56724044/128412286-33c0e037-e548-4a62-90d7-484802929eaf.png)

Now it is time to start our server to see if it works. Open your terminal in the same directory as your index.js file and type:
Go to the directory where you have your index.js and run this command
```
$ node index.js
```
![image](https://user-images.githubusercontent.com/56724044/128412901-2b63212c-4822-47e3-b388-2fbf30756476.png)

##### Now that our server is running on port 5000, we need to open this port in EC2 Security Groups.
Once the port 5000 is now opened in the security group, Open up your browser and try to access your server’s Public IP or Public DNS name followed by port 5000:
```
http://<PublicIP-or-PublicDNS>:5000
```
![image](https://user-images.githubusercontent.com/56724044/128414048-fac70065-383a-40cf-acec-6f515f7c3d50.png)

# ROUTES
There are three actions that our To-Do application needs to be able to do:

1. Create a new task
1. Display list of all tasks
1. Delete a completed task
Each task will be associated with some particular endpoint and will use different standard HTTP request methods: POST, GET, DELETE.

For each task, we need to create routes that will define various endpoints that the To-do app will depend on. So let us create a folder routes
```
$ mkdir routes
```
Change directory to routes folder.
```
$ cd routes
```
Now, create a file api.js with the command below
```
$ touch api.js
```
Open the file with the command below
```
$ vim api.js
```
![image](https://user-images.githubusercontent.com/56724044/128415668-f23140fa-e9c2-4e7e-970d-9da4f2611f8c.png)

# MODELS
Since the application will make sue of MongoDB which is NoSQL database, we need to create a model.
**A model** is at the heart of JavaScript based applications, and it is what makes it interactive.

We will also **use models to define the database schema** . This is important so that we will be able to define the fields stored in each Mongodb document.
In essence, **the Schema is a blueprint of how the database will be constructed,** including other data fields that may not be required to be stored in the database. These are known as virtual properties

##### To create a Schema and a model, install mongoose which is a Node.js package that makes working with mongodb easier.
Change directory back Todo folder with cd .. and install Mongoose
```
$ npm install mongoose
```
![image](https://user-images.githubusercontent.com/56724044/128416510-a81f8288-e6ae-4b7c-8959-50813ddeb12e.png)
##### Create a new folder with mkdir models command
```
$ mkdir models
```
Change directory into the newly created ‘models’ folder with cd models.
```
$ cd models
```
Inside the models folder, create a file and name it todo.js
```
$ touch todo.js
```
You can also run the 3 consecutive commands together with && command
```
$ mkdir models && cd models && touch todo.js
```
Open the file created with vim todo.js then paste the code below in the file:
```
$ vim touch todo.js
```
![image](https://user-images.githubusercontent.com/56724044/128417489-76e512c1-ae0b-45b5-97f2-28ac5e5d7614.png)

Now we need to update our routes from the file api.js in ‘routes’ directory to make use of the new model.

In Routes directory, open api.js with vim api.js, delete the code inside with :%d command and paste there code below into it then save and exit
```
$ vim api.js
```
![image](https://user-images.githubusercontent.com/56724044/128418002-1f343bd2-2fbc-489d-9d14-625ad86205b1.png)

# Next is MONGODB DATABASE
In order to get the full functionality of our ToDO app, we need a database where we will store our data. For this we will use mLab.
To sign up for MondoDB: https://www.mongodb.com/atlas-signup-from-mlab
While setting up the DB, ensure that you allow access to the MongoDB database from anywhere. This is for testing purpose but in a real life production, you will not allow all access
![image](https://user-images.githubusercontent.com/56724044/128625319-9ceb34d4-df43-4146-ad7c-97880fea6887.png)

##### Create a MongoDB database and collection inside mLab
![image](https://user-images.githubusercontent.com/56724044/128625368-86924f20-ad38-456f-b09b-288a8a08be51.png)

In the **index.js file**, we specified **process.env** to access **environment variables**, but we have not yet created this file. So we need to do that now.

##### Create a file in my Todo directory and name it **.env**
```
touch .env
vim .env
```
In the text editor, paste the connection string to access the database in it. mongodb+srv://tolulopeolorunfemi:<password>@cluster0.achb3.mongodb.net/myFirstDatabase?retryWrites=true&w=majority
  Make sure you change the password and myFirstDatabase to your password and name of your database cluster
  
How to get the MongoDB connection string
Click Database > Connect > Connect your Application
![image](https://user-images.githubusercontent.com/56724044/128625505-79f57e82-2a09-49c1-97b0-5010aedff5a2.png)
![image](https://user-images.githubusercontent.com/56724044/128625522-7c8b0a99-6ac8-4915-8321-57a686e018e5.png)
![image](https://user-images.githubusercontent.com/56724044/128625541-b4247294-77cc-4889-9482-7b3bb44a75c6.png)

Now we need to update the **index.js** to reflect the use of **.env** so that Node.js can connect to the database.

```
  vim index.js
```








