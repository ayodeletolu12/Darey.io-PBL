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
#### In the Books directory, we will initialize npm project. When you initialize, it contains the info in json format of our project called package.json
```
npm init
```
#### Add a file to it named server.js. That will be our entry point instead of using index.js
```
vim server.js
```
Copy and paste the web server code below into the ```server.js``` file
```
var express = require('express');
var bodyParser = require('body-parser');
var app = express();
app.use(express.static(_dirname + '/public'));
app.use(bodyParser.json());
require('./apps/routes')(app);
app.set('port', 3300);
app.listen(app.get('port'), function() {
    console.log('Server up: http://localhost:' + app.get('port'));
});
```
### Install Express and set up routes to the server
Express is a minimal and flexible Node.js web application framework that providesfeatures for web and mobile applications.

``` We will use Express in to pass book information to and from our MongoDB database ```
### We will also use Mongoose package which provides a straight-forward, schema-based solution to model your application data. We will use mongoose to establish a schema for the database to store data of our book register.
To install the 2 packages

```
sudo npm install express mongoose
```
##### In Books folder, create a folder named ```apps``` and cd into the apps directory
```
mkdir apps && cd apps
```
Create a file names ```routes.js```
```
vim routes.js
```
Copy and paste the code in the routes.js
```
var Book = require('./models/book');
module.exports = function(app) {
  app.get('/book', function(req, res) {
    Book.find({}, function(err, result) {
      if (err) throw err;
      res.json(result);
    });
  });
  app.post('/book', function (req, res) {
    var book = new Book( {
      name:req.body .name,
      isbn:req.body.isbn,
      author:req.body.author,
      pages:req.body.pages
    });
  });
  book.save(function(err, result) {
    if ( err ) throw err;
    res.json( {
      message:"Successfully added book",
      book:result
    });
  });
});  
app.delete("/book/:isbn", function(req, res) {
  Book.findOneAndRemove(req.query, function(err, result) {
    if ( err ) throw err;
    res.json( {
      message: "Successfully deleted the book",
      book: result
    });
  });
});
var path = require('path');
app.get('*', function(req, res) {
  res.sendfile(path.join(_dirname + '/public', 'index.html')};
});
};
```
In the 'apps' folder, create a folder named ```models```
```
mkdir models && cd models
```
##### Create a file named ```book.js```
```
vim book.js
```
##### Copy and paste the code below into 'book.js'
```
var mongoose
