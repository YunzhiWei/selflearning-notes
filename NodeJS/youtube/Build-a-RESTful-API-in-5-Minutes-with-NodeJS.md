# Build a RESTful API in 5 Minutes with NodeJS - Updated

## [Video](https://www.youtube.com/watch?v=p-x6WdwaJco)

## Hands-on lab

### Check intallation

```
> node -v
> npm -v
> mongo
```

### build new project

```
> mkdir rest
> cd rest
> npm init
```

### install packages

* local packages

```
> npm install -S express
> npm install -S mongoose
> npm install -S node-restfull body-parser
```

* global packages

```
> npm install -g nodemon
```

### create server.js (in app root directory)

* server.js

```
var express = require('express');
var app = express();

app.get('/', function(req, res){
  res.send('working');
});

app.listen(3000);
console.log('API is running on port 3000');
```

* run server in os console with node

```
> node server.js
```

* run server in os console with nodemon

```
> nodemon server.js
```

### more code for API route

* server.js

```
// Dependencies
var express = require('express');
var mongoose = require('mongoose');
var bodyParse = require('body-parser');

// MongoDB
mongoose.connect('mongodb://localhost/rest_test');

// Express
var app = express();
app.use(bodyParse.urlencoded({ extended: true }));
app.use(bodyParse.json());

// Routes
app.use('/api', require('./routes/api'));

// Start server
app.listen(3000);
console.log('API is running on port 3000');
```

* new file: ./routes/api.js

```
// Dependencies
var express = require('express');
var router = express.Router();

// Routes
router.get('/products', function (req, res) {
  res.send('API is working');
});

// Return router
module.exports = router;
```

* try in chrome: url: http://localhost:3000/api/products

### model

> find more details in github for node-restful

* new file in ./model/product.js

```
// Dependencies
var restful = require('node-restful');
var mongoose = restful.mongoose;

// Schema
var productSchema = new mongoose.Schema({
  name: String,
  sku: String,
  price: Number
});

// Return model
module.exports = restful.model('Products', productSchema);
```

* api.js

```
// Dependencies
var express = require('express');
var router = express.Router();

// Model

var Product = require('../models/product')

// Routes
Product.methods(['get', 'put', 'post', 'delete']);
Product.register(router, '/products');

// Return router
module.exports = router;
```

* test with PostMan (Get, Post, Put)

  - Get
  browser url: localhost:3000/api/products

  - Post with PostMan
  url: localhost:3000/api/products
  body:
  {
	"name": "Product 1",
	"sku": "XYZ12345",
	"price": 125.00
  }

  - Put
  url: localhost:3000/api/products/584f48d013b1f92dd88aeb75
  body:
  {
	"name": "Cool Product",
  }

  - Delete
  url: localhost:3000/api/products/584f48d013b1f92dd88aeb75
