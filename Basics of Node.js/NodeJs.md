# NODE JS

Getting started with Node.js. Let's learn vanilla node.js before jumping into framework like express. At the heart of frameworks, same concepts are implemented with many other known issues.

**What is node.js?** -> Node.js is JavaScript runtime which allows us to run JavaScript on server.

**So, what server?** -> Chrome's V8 engine.

**Why?** -> 
* Simple, Light & Same as frontend Javascript. 
* None-blocking. Event Driven.

## 1. Installation

1. Install node.js from nodejs.org.
2. Confirm installation `node -v` & `npm -v`

## 2. Server application

```js
var http = require('http');

function onRequest(request, response){
    response.writeHead(200, {'Content-Type': 'text/plain'});
    response.write('hello-world');
    response.end();
}

http.createServer(onRequest).listen(8000);
```

* `http` -> imports http module.
* `createServer('actionMethod')` -> Creates server and executes the method on request.
* `listen` -> Listens to the port.
* `function onRequest(request, response){..}` -> Function to handle request. 2 arguments passed automatically.
* `response.writeHead(200, {'Content-Type': 'text/plain'});` -> Passed http response headers with content's MIME types.
* Refer https://en.wikipedia.org/wiki/Media_type
* Full documentation: https://nodejs.org/api/http.html

## 3. Node.Js modules

`var http = require('http');` -> built in module.

### 3.1. Custom modules

1. Exporting individual properties

```js
//module1.js
function myFunction(){
    console.log('my-function');
}
var myString = 'My String';

module.exports.myFunction = myFunction;
module.exports.myString = myString;

// server.js
var http = require('http');
var module1 = require('./module1');

function onRequest(request, response){
    response.writeHead(200, {'Content-Type': 'text/plain'});
    response.write('hello-world');
    response.write(module1.myString);
    module1.myFunction();
    response.end();
}

http.createServer(onRequest).listen(8000);
```
2. Exporting all properties

```js
// module2.js
module.exports = {
    myFunction: function(){
        console.log(''fun from module 2');
    },
    myVariable: 'exported variable';
}

//server.js
var http = require('http');
var module1 = require('./module1');
var module2 = require('./module2');

function onRequest(request, response){
    response.writeHead(200, {'Content-Type': 'text/plain'});
    response.write('hello-world');
    response.write(module1.myString);
    response.write(module2.myVariable);
    module1.myFunction();
    module2.myFunction();
    response.end();
}

http.createServer(onRequest).listen(8000);
```

## 4. Rendering HTML

1. Read file from filesystem (Use fs module and readFile functions)
2. Check file existance
3. Set headers
4. write content


```js
// Index.html
<!DOCTYPE html>
<html lang="en">
    <head>
        <title>Test</title>
    </head>
    <body>
        Index page
    </body>
</html>

// server.js
var http = require('http');
var fs = require('fs');

function onRequest(request, response){
    
    fs.readFile('./index.html', null, function(error, data){
        if(error){
            response.writeHead(404);
            response.write("FILE NOT FOUND")
        }
        else{
            response.writeHead(200, {'Content-Type': 'text/html'});
            response.write(data);
        }
        response.end();
    });
}

http.createServer(onRequest).listen(8000);
```

## 5. Routing

1. Use url module and get the path,
2. Check defined routes
3. Read file if route found
4. Write response

```js
// app.js
var url = require('url');
var fs = require('fs');

function renderHTML(file, response) {
    fs.readFile(file, null, function(error, data){
        if(error){
            response.writeHead(404);
            response.write('File not found');
        }
        else{
            response.writeHead(200,{'Content-Type':'text/html'});
            response.write(data);
        }
        response.end();
    }) 
}

module.exports = {
    handleReq: function(request,  response){
        var path = url.parse(request.url).pathname;
        switch (path) {
            case '/':
                renderHTML('index.html', response);
                break;
            case '/login':
                renderHTML('login.html', response);
                break;
            default:
                response.writeHead(404);
                response.write('Route not defined');
                response.end();
        }
    }
}

// server.js
var http = require('http');
var app = require('./app');

http.createServer(app.handleReq).listen(8000);
```

## 6. Express framework.

***Why? :*** To avoid reinventing the wheel. Frameworks already solved the problems which one can face in the day to day functionalities.
* Avoid rewritting code/functinality
* Bigger projects gets complecated if not arranged properly.
* Some problems already soved in the better way, no need t reinvent the wheel.
* It's faster to get started.
* Focus on business logic, not on solving coding issues.

### 6.1. Installation

* Use npm to install express-generator globally on system : `sudo npm install -g  express-generator`
* Help: `express -h`
* Start new express project: `mkdir proj-directory` & `express proj-directory` ->this installs JADE/PugJS templating engine.
* use `express --hbs exp-dir` to use handlebar js as templating engine.
* `cd proj-directory`
* `npm install`
* run: `DEBUG=exp1:* npm start` or `node bin/www` or `npm start`

## 7. Express templating engines

### 7.1 Handlebars

* A handlebars expression is a `{{, some contents, followed by a }}`. e.g.: `{{title}}`
* HTML Escaping : `{{{body}}}`
* Block expression
    ```hbs
    // 1st ex.
    {{#list people}}
    {{firstName}} 
    {{lastName}}
    {{/list}}

    // 2nd ex.
    {{# if condition }}
    ...
    {{ else }}
    ...
    {{/ if}}

    //3rd array ex
    {{# each myarray }}
    {{ this }}
    {{/each}}

    //4th array ex 
    {{# each myarray as |val key }}
    {{ key }}: {{ val }}
    {{/each}}
    ```
* Nested paths: `{{author.name}}`
* Template comments with `{{!-- --}}` or `{{! }}`.

## 8. GET & POST methods

* GET values -> request.params.<-var->
* POST values -> request.body.<-var->

```js
// Route: index.js
router.get('/id/:idval', function(req, res, next) {
    res.render('idvals', {output: req.params.idval})  
});

router.post('/create-id', function(req, res, next) {
  var id = req.body.id;
  res.redirect('/id/'+id);
});

// View
<h1>ID passed from GET {{ output }}</h1>
// ---
<form action="/create-id" method="post">
    <input type="text" name="id" placeholder="Enter ID">
    <button type="submit">Submit</button>
</form>
```
## 9. Validator & sessions.

* Installtion: `npm install --save express-validator`
* Installtion: `npm install --save express-session`
* Import modules 
* `var expressSession = require('express-session');` -> https://github.com/expressjs/session
* `var expressValidator = require('express-validator');` -> https://express-validator.github.io/docs/

* Routes
```js
// Post route
router.post('/create-id', function(req, res, next) {
  req.check('id', 'invalid Email').isEmail();
  var errors = req.validationErrors();
  if(errors){
    req.session.errors = errors;
    res.redirect('/');
  }
  else{
    res.redirect('/id/'+req.body.id);
  }
});

// get route
router.get('/', function(req, res, next) {
  res.render('index', { title: 'Express validator', success:false, errors: req.session.errors, layout: 'layout' });
  req.session.errors = null; // resetting after form loaded
});
```
## 10. Using database

* Install `npm install --save mongodb` -> driver
* Route require:
```js
var mongo = require('mongodb').MongoClient;
var assert = require('assert'); 
// mongo connect
var url = 'mongodb://127.0.0.1:27017/database';

// Insert
var items = {
    id: req.body.id, //Comes from input form
}
mongo.connect(url,{ useNewUrlParser: true }, function(err, client){
    assert.equal(null, err);
    var db = client.db('databasename');
    db.collection('collectionname').insertOne (items, function(err, result){
    assert.equal(null, err);
    console.log('ID inserted');
    client.close();
    });
    res.redirect('/');
});

// Fetch data
// JS
var resArray = [];
mongo.connect(url,{ useNewUrlParser: true }, function(err, client){
    assert.equal(null, err);
    var db = client.db('databasename');
    var cursor = db.collection('collectionname').find();
    
    cursor.forEach(function(doc, err){
      assert.equal(null,err);
      resArray.push(doc);
    },
    function(){
      client.close();
      res.render('index', { items: resArray});
    });
});



// Delete

  mongo.connect(url,{ useNewUrlParser: true }, function(err, client){
    assert.equal(null, err);
    var db = client.db('iddbs');
    db.collection('eids').deleteOne({"_id":objectID(rowid)}, function(err, result){
      assert.equal(null, err);
      res.redirect('/');
      client.close();
    });
  });

// Update
    mongo.connect(url, {useNewUrlParser: true}, function(err, client){
      assert.equal(null, err);
      var db = client.db('iddbs');
      db.collection('eids').updateOne({"_id": objectID(collid)}, {$set:items}, function(err,result){
        assert.equal(null, err);
        console.log('updated');
        client.close();
        res.redirect('/');
      });
    });
    
// HTML
    <ul>
        {{#each items}}
            <li>{{this.id}}</li>
        {{/each}}
    </ul>
```

## 10. Mongoose

* Installation: `npm install --save mongoose`
* Reuire mongoose `var mongoose = require('mongoose');`
* connect and keeping :`mongoose.connect('localhost:27017/emaildb');`
* Create the schema: how the data structured in mongodb.

```js
// Requirements at route
var mongoose = require('mongoose');
mongoose.connect('mongodb://localhost:27017/emaildb');
var Schema = mongoose.Schema;
var userDataSchema = new Schema({
    // emailid: String, ( optional schema validation )
    emailid: {type:String, required: true},
});

var UserData = mongoose.model('UserData', userDataSchema);
// Creates userdatas collection
// ----------------------------------------

// Get all data
router.get('/', function(req, res, next) {
  UserData.find()
    .then(function(doc){
      res.render('index', { items: doc });
    });
});

// Insert
var items = {
    emailid : req.body.emailid,
};
var data = new UserData(items);
data.save();

// Find By ID
UserData.findById(rowid, function(err, data){
    if(err){
        console.error('error');
    }
    else{
        res.render('update', { item: data });
    }
});

// Update
UserData.findById(rowid, function(err, data){
    if(err){
      console.error('Record fetch failed');
    }
    data.emailid = emailid;
    data.save();
    res.redirect('/');
});

// Delete by ID
UserData.findByIdAndDelete(rowid, function(err, data){
    if(err){
    console.error('error');
    }
    else{
    res.redirect('/');
    }
});
```