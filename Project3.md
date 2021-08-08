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

Now we need to update the **index.js** in the ToDo dir to reflect the use of **.env** so that Node.js can connect to the database.

```
  vim index.js
```
![image](https://user-images.githubusercontent.com/56724044/128625859-ebf2d51e-701b-4931-a47f-f2fd6e212364.png)
```
Using environment variables to store information is considered more secure and best practice to separate configuration and secret data from the application, instead of writing connection strings directly inside the index.js application file.
```
Start your server using the command:
```
  node index.js  
 ``` 
### I MET A BLOCKER WHEN STARTING MY SERVER
```
  Error: Cannot find module 'mongoose'
```
![Error loading node index js](https://user-images.githubusercontent.com/56724044/128625935-02caac1f-d88e-4e4d-8492-0188634cc08a.png)

# How it was resolved.
I installed the npm package mongoose and now link it to the Todo dir so that index.js can load the package
```
  $ sudo npm install mongoose -g
  $ cd Todo
  $ sudo npm link mongoose
  $ node index.js
```
![install the module-g and link with app dir](https://user-images.githubusercontent.com/56724044/128626052-6d6b5d31-6878-4055-978e-0f266b0e18e8.png)
  
When you see ‘Database connected successfully’, if so – we have our backend configured. Now we are going to test it.  
#### Another Blocker
When I tried to run the node index.js again, i recieved an error  
```
  Emitted 'error' event on Server instance at: at emitErrorNT (net.js:1340:8) at processTicksAndRejections (internal/process/task_queues.js:84:21) { code: 'EADDRINUSE', errno: 'EADDRINUSE', syscall: 'listen', address: '::', port: 5000
```  
#### How I resolved it
  I check the processes running, and I kill the process id of node index.js
![image](https://user-images.githubusercontent.com/56724044/128626641-120afb79-06e5-4411-a03a-48952737b085.png)

### Testing Backend Code without Frontend using RESTful API
  
  So far we have written backend part of our To-Do application, and configured a database, but we do not have a frontend UI yet. We need ReactJS code to achieve that. But during development, we will need a way to test our code using RESTfulL API. Therefore, we will need to make use of some API development client to test our code.
  
  In this project, we will use [Postman](https://www.getpostman.com/downloads/) to test our API.
  Click [Install Postman](http://www.getpostman.com/downloads/) to download and install postman on your machine
Click [Here](https://www.youtube.com/watch?v=FjgYtQK_zLE) to learn how perform [CRUD Operations](https://en.wikipedia.org/wiki/Create,_read,_update_and_delete) on Postman
  
You should test all the API endpoints and make sure they are working. For the endpoints that require body, you should send JSON back with the necessary fields since it’s what we setup in our code.  

Now open your Postman, create a POST request to the API http://<PublicIP-or-PublicDNS>:5000/api/todos. This request sends a new task to our To-Do list so the application could store it in the database.

Note: make sure your set header key Content-Type as application/json  
![image](https://user-images.githubusercontent.com/56724044/128628632-3db5e9fb-18f5-410e-b488-79753c90d5ef.png)

  When you create a POST request
  ![image](https://user-images.githubusercontent.com/56724044/128628697-fd9d8574-5905-46cc-b0f6-1de530331800.png)

Create a **GET request to your API on http://<PublicIP-or-PublicDNS>:5000/api/todos**. This request retrieves all existing records from out To-do application (backend requests these records from the database and sends it us back as a response to GET request).
![image](https://user-images.githubusercontent.com/56724044/128628772-01661acf-383b-4f12-8624-59d1525f53a7.png)
  
Optional task: Try to figure out how to send a DELETE request to delete a task from out To-Do list.

Hint: To delete a task – you need to send its ID as a part of DELETE request.

By now you have tested backend part of our To-Do application and have made sure that it supports all three operations we wanted:

1. Display a list of tasks – HTTP GET request
2. Add a new task to the list – HTTP POST request
3. Delete an existing task from the list – HTTP DELETE request
  
We have successfully created our Backend, now let go create the Frontend.
  
#  FRONTEND CREATION
Since we are done with the functionality we want from our backend and API, it is time to create a user interface for a Web client (browser) to interact with the application via API. To start out with the frontend of the To-do app, we will use the create-react-app command to scaffold our app.

In the same root directory as your backend code, which is the Todo directory, run:
```
   npx create-react-app client
```
This will create a new folder in your Todo directory called client, where you will add all the react code.
![image](https://user-images.githubusercontent.com/56724044/128629419-fa628a90-39cc-488b-af9f-17c850641d37.png)

### Running a React App
Before testing the react app, there are some dependencies that need to be installed.

1. Install concurrently. It is used to run more than one command simultaneously from the same terminal window.
```
  npm install concurrently --save-dev
```  
1. Install nodemon. It is used to run and monitor the server. If there is any change in the server code, nodemon will restart it automatically and load the new changes.
```
  npm install nodemon --save-dev
```
1. In Todo folder open the **package.json file**. Change the highlighted part of the below screenshot and replace with the code below.
```
"scripts": {
"start": "node index.js",
"start-watch": "nodemon index.js",
"dev": "concurrently \"npm run start-watch\" \"cd client && npm start\""
},
```
![image](https://user-images.githubusercontent.com/56724044/128629613-d6401e95-c006-4b37-a1c9-b1543a195f7b.png)

After replacing the script, it should look like this
![image](https://user-images.githubusercontent.com/56724044/128629852-5a17945f-b6c1-47c2-a03c-7f27d54a0872.png)

#### Configure Proxy in package.json
Change directory to ‘client’ from Todo dir
````
 $ cd client
```  
#### Open the package.json file
$ vim package.json
Add the key value pair in the package.json file "proxy": "http://localhost:5000".
**"proxy": "http://localhost:5000"**.
  
The whole purpose of adding the proxy configuration in number 3 above is to make it possible to access the application directly from the browser by simply calling the server url like http://localhost:5000 rather than always including the entire path like http://localhost:5000/api/todos

Now, ensure you are inside the Todo directory, and simply do:
```
  npm run dev
```  
Your app should open and start running on localhost:3000

  
  
  
  
  
npm install nodemon --save-dev  

  
  
  




