# What is Node.js Exactly? - a beginners introduction to Nodejs

> LearnCode.academy

## [Video](https://www.youtube.com/watch?v=pU9Q6oiQNd0&t=18s)

## Agenda

  - what is Nodejs
  - what do you do with it
    + utilities on your machine
    + a web server (express, koa)
  - Gimme some super-basics
    + how modules work
    + npm modules
    + make a basic webserver

## Hands on lab

### interactive mode

* To check the nodejs version

  ```
  > node -v
  v6.9.1
  ```

* Start an interactive mode

  ```
  > node
  >
  ```

* Interact in interactive mode

  ```
  > var a=1;
  undefined
  > a
  1
  ```

  > You can type the above code and see the same result in chrome console, and get the same result.
  > The difference is that, in chrome, the 'var a' belongs to window, and in node, the 'var a' belongs to global
  > You can print the value a in chrome by 'window.a', and print the value a in node by 'global.a'.
  > Similiar, you have the 'document' object in chrome and 'process' object in node.

### module mode

* create a module file named as 'module1.js', add the following code

  ```
  console.log("hi");
  var a = 1;
  console.log(a);
  ```

* type the following command in os console

  ```
  > node module1
  ```

### use one module from another one

* require module (put the following code in module1.js, and create a new empty file named 'module2.js')

  ```
  var m2 = require('./module2');
  console.log(m2);
  ```

  run the following command in os console

  ```
  > node module1
  ```

* put the following code in module2.js

  ```
  var a = 1;
  module.exports.a = a;
  module.exports.b = 2;
  ```

  and run the following command again

  ```
  > node module1
  ```

* the following code in module2.js will have the same result (without 'module')

  ```
  var a = 1;
  exports.a = a;
  exports.b = 2;
  ```

* put the following code in module2.js

  ```
  var a = 1;
  module.exports = function() {
    console.log('module 2!')
  };
  ```

  invoke module 2 function in module 1

  ```
  var m2 = require('./module2');
  console.log(m2);
  m2();
  ```

### use npm to install public modules

* install

  ```
  npm install underscore
  ```

* invoke (put following code in module1)

  ```
  var _ = require('underscore');
  var m2= require('./module2');
  console.log(_);
  ```

### npm init and package.json

* run the following command

  ```
  > npm init
  ```

  > This utility will walk you through creating a package.json file.

* npm install <package name> and npm install <package name> -S

  > npm install <package name> will install npm package
  > npm install <package name> -S will install package and update package.json as well

* npm install

  > npm install will install all dependencies npm packages in package.json

### http module

* use http to response to http request

  ```
  var http = require('http');
  var server = http.createServer(function(request, response) {
    console.log('got a request');
    response.write('hi');
    response.end();
  });
  server.listen(3000);
  ```

# Node.js tutorial for beginners 2014 - an introduction to Node.js with Express.js

> LearnCode.academy

## [Video](https://www.youtube.com/watch?v=FqMIyTH9wSg)

## Agenda

## Hands-on lab

### install node, npm and check version

```
> node -v
> npm -v
```

### install express

```
> npm install -g express-generator
```

### generate express project

```
> express <app name>
```

### check the package.json

```
... ...
"jade": "~1.3.0"
... ...
```

### generate express project again to use another framework, instead of jade

```
> express exp2016 --hogan -c less
```

### install dependencies packages

```
> cd exp2016
> npm install
```

### start the server

* for mac

```
DEBUG=my-application ./bin/www
```

* for windows

```
> set DEBUG=app
> node ./bin/www
```

* open chrome to browse the web app

### nodemon

* install

```
> npm install -g nodemon
```

* start web server with nodemon

```
> nodemon ./bin/www
```

### review the project

* ./bin/www

* app.js

* views

  - folder
  - source file

```
app.set('views', path.join(__dirname, 'views'));
```

### prepare Hands-on lab

* comments out the following two lines in app.js

```
var users = require('./routes/users');
```

```
app.use('/users', users);
```

* comments out the following code in ./routes/index.js

```
router.get('/', function(req, res, next) {
  res.render('index', { title: 'Express' });
});
```

### response to request

* replace the above code with the following

```
router.get('/', function(req, res) {
  res.send('ok');
});
```

and

```
router.get('/', function(req, res) {
  res.send(200);  // or 400, or 404
});
```

and

```
router.get('/', function(req, res) {
  res.send({
    users: ['Will', 'Laura']
  });
});
```

### data between view and controller

* index.js (controller)

  ```
  router.get('/', function(req, res) {
    res.render('index', {
      title: 'My node app',
      age: 33
    });
  });
  ```

* index.hjs (view)

  ```
  <body>
    <h1>{{ title }}</h1>
    <p>My age is {{ age }}</p>
  </body>
  ```

### get url query parameters

```
router.get('/', function(req, res) {
  console.log(req.query);
});
```

> chrome browser url: localhost:3000?age=33&name=Chris

### response to different url path

```
router.get('/users', function(req, res) {
  res.send(200);
});
```

> chrome browser url: localhost:3000/users

### url path id: request params

```
router.get('/users/:id', function(req, res) {
  console.log(req.params);
  res.send(req.params.id, 200);
});
```

> chrome browser url: localhost:3000/users/30

### router

* app.js: replace the following

```
app.use('/', index);
```

with

```
app.use('/users', index);
```

* index.js: replace the following

```
router.get('/users/:id', function(req, res) {
```

with

```
router.get('/:id', function(req, res) {
```
