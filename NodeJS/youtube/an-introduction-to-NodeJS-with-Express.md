
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
