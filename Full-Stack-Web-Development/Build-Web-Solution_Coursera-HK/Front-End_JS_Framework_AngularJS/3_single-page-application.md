# Angular Factory, Service and Dependency Injection

## 1. **阅读: **Objectives and Outcomes

## 2. **视频: **Dependency Injection

## 3. **视频: **Angular Factory and Service

## 4. **视频: **Exercise \(Video\): Angular Factory and Service

## 5. **阅读: **Exercise \(Instructions\): Angular Factory and Service

### Objectives and Outcomes

In this exercise you will explore dependency injection in Angular. You will also learn about designing custom services using the factory and the service approaches. At the end of this exercise, you will be able to:

* Use dependency injection to enable the use of custom services in Angular modules and controllers
* Design custom services using the Angular factory and service approaches

### Creating controllers.js and services.js

* In the _scripts_ sub-folder of the _app_ folder, create two new files named _controllers.js_ and _services.js_.
* Open _app.js_ and copy the entire code there and copy it into _controllers.js_.
* Next, we will edit the code as follows. Remove the square brackets from the angular.module\( \), so that it us updated as shown below:

  ```
  angular.module('confusionApp')
  ```


* Next, go to _app.js_ and delete all the controller code from it, so that your _app.js_ file will contain only the following code:

  ```
  'use strict';
  angular.module('confusionApp', []);
  ```


* Next, open _menu.html_ and at then include _controller.js_ and _services.js_ using &lt;script&gt; tag.

  ```
  <script src="scripts/controllers.js"></script>
  <script src="scripts/services.js"></script>
  ```


* Open services.js and add the following code:

  ```
  'use strict';
  angular.module('confusionApp')
    .factory('menuFactory', function() {
  });
  ```


* Next, add the following JavaScript array into the factory code above:

  ```
  var dishes=[
  {
  name:'Uthapizza',
  image: 'images/uthapizza.png',
  category: 'mains',
  label:'Hot',
  price:'4.99',
  description:'A unique combination of Indian Uthappam (pancake) and Italian pizza, topped with Cerignola olives, ripe vine cherry tomatoes, Vidalia onion, Guntur chillies and Buffalo Paneer.',
  comments: [
  {
  rating:5,
  comment:"Imagine all the eatables, living in conFusion!",
  author:"John Lemon",
  date:"2012-10-16T17:57:28.556094Z"
  },
  {
  rating:4,
  comment:"Sends anyone to heaven, I wish I could get my mother-in-law to eat it!",
  author:"Paul McVites",
  date:"2014-09-05T17:57:28.556094Z"
  },
  {
  rating:3,
  comment:"Eat it, just eat it!",
  author:"Michael Jaikishan",
  date:"2015-02-13T17:57:28.556094Z"
  },
  {
  rating:4,
  comment:"Ultimate, Reaching for the stars!",
  author:"Ringo Starry",
  date:"2013-12-02T17:57:28.556094Z"
  },
  {
  rating:2,
  comment:"It's your birthday, we're gonna party!",
  author:"25 Cent",
  date:"2011-12-02T17:57:28.556094Z"
  } ]
  },
  {
  name:'Zucchipakoda',
  image: 'images/zucchipakoda.png',
  category: 'appetizer',
  label:'',
  price:'1.99',
  description:'Deep fried Zucchini coated with mildly spiced Chickpea flour batter accompanied with a sweet-tangy tamarind sauce',
  comments: [
  {
  rating:5,
  comment:"Imagine all the eatables, living in conFusion!",
  author:"John Lemon",
  date:"2012-10-16T17:57:28.556094Z"
  },
  {
  rating:4,
  comment:"Sends anyone to heaven, I wish I could get my mother-in-law to eat it!",
  author:"Paul McVites",
  date:"2014-09-05T17:57:28.556094Z"
  },
  {
  rating:3,
  comment:"Eat it, just eat it!",
  author:"Michael Jaikishan",
  date:"2015-02-13T17:57:28.556094Z"
  },
  {
  rating:4,
  comment:"Ultimate, Reaching for the stars!",
  author:"Ringo Starry",
  date:"2013-12-02T17:57:28.556094Z"
  },
  {
  rating:2,
  comment:"It's your birthday, we're gonna party!",
  author:"25 Cent",
  date:"2011-12-02T17:57:28.556094Z"
  } ]
  },
  {
  name:'Vadonut',
  image: 'images/vadonut.png',
  category: 'appetizer',
  label:'New',
  price:'1.99',
  description:'A quintessential ConFusion experience, is it a vada or is it a donut?',
  comments: [
  {
  rating:5,
  comment:"Imagine all the eatables, living in conFusion!",
  author:"John Lemon",
  date:"2012-10-16T17:57:28.556094Z"
  },
  {
  rating:4,
  comment:"Sends anyone to heaven, I wish I could get my mother-in-law to eat it!",
  author:"Paul McVites",
  date:"2014-09-05T17:57:28.556094Z"
  },
  {
  rating:3,
  comment:"Eat it, just eat it!",
  author:"Michael Jaikishan",
  date:"2015-02-13T17:57:28.556094Z"
  },
  {
  rating:4,
  comment:"Ultimate, Reaching for the stars!",
  author:"Ringo Starry",
  date:"2013-12-02T17:57:28.556094Z"
  },
  {
  rating:2,
  comment:"It's your birthday, we're gonna party!",
  author:"25 Cent",
  date:"2011-12-02T17:57:28.556094Z"
  }
  ]
  },
  {
  name:'ElaiCheese Cake',
  image: 'images/elaicheesecake.png',
  category: 'dessert',
  label:'',
  price:'2.99',
  description:'A delectable, semi-sweet New York Style Cheese Cake, with Graham cracker crust and spiced with Indian cardamoms',
  comments: [
  {
  rating:5,
  comment:"Imagine all the eatables, living in conFusion!",
  author:"John Lemon",
  date:"2012-10-16T17:57:28.556094Z"
  },
  {
  rating:4,
  comment:"Sends anyone to heaven, I wish I could get my mother-in-law to eat it!",
  author:"Paul McVites",
  date:"2014-09-05T17:57:28.556094Z"
  },
  {
  rating:3,
  comment:"Eat it, just eat it!",
  author:"Michael Jaikishan",
  date:"2015-02-13T17:57:28.556094Z"
  },
  {
  rating:4,
  comment:"Ultimate, Reaching for the stars!",
  author:"Ringo Starry",
  date:"2013-12-02T17:57:28.556094Z"
  },
  {
  rating:2,
  comment:"It's your birthday, we're gonna party!",
  author:"25 Cent",
  date:"2011-12-02T17:57:28.556094Z"
  } ]
  }
  ];
  ```


* Next, introduce an empty JavaScript object into the factory as follows:

  ```
  var menufac = {};
  ```


* Finally, add the following code to the factory to define the function and return the object:

  ```
  menufac.getDishes = function(){
    return dishes;
  };
  menufac.getDish = function (index) {
    return dishes[index];
  };
  return menufac;
  ```


* Now, open _controllers.js_ and then from the _MenuController_ delete the dishes object. Then, add the following statement in its place:

  ```
  $scope.dishes= menuFactory.getDishes();
  ```


* Now we do dependency injection to introduce the _menuFactory_ service into _MenuController_:

  ```
  .controller('MenuController', ['$scope', 'menuFactory', function($scope, menuFactory) {
  ```


* Next, we move to the DishDetailController and remove the dish object from it and replace it with the following:

  ```
  $scope.dish= menuFactory.getDish(3);
  ```


* Then, we do dependency injection into the DishDetailController as follows

  ```
  .controller('DishDetailController', ['$scope', 'menuFactory', function($scope, menuFactory) {
  ```


* After saving the changes, move to dishdetail.html and add in the following code to include the JS files:

  ```
  <script src="scripts/controllers.js"></script>
  <script src="scripts/services.js"></script>
  ```


### Using Service instead of Factory

* Go to services.js and remove the following two statements from the code:

  ```
  var menufac = {};
  . . .
  return menufac;
  ```


* Then change the function code as follows, replacing _menufac_ with _this_:

  ```
  this.getDishes = function(){
    return dishes;
  };
  his.getDish = function (index) {
    return dishes[index];
  };
  ```


* Then, change the _factory_ to _service_ as follows:

  ```
  .service('menuFactory', function() {
  ```


* Save the changes and see the result.

### Conclusions

In this exercise we explored dependency injection and the use of Angular services and defining custom services using the factory or the service approach.

## 6. **练习测验: **Angular Factory, Service and Dependency Injection

## 7. **阅读: **Angular Factory, Service and Dependency Injection: Additional Resources

### Angular Resources

* [Dependency Injection](https://docs.angularjs.org/guide/di)
* [Angular Services](https://docs.angularjs.org/guide/services)
* [Angular List of Built-in Services](https://docs.angularjs.org/api/ng/service)

### Other Resources

* [Dependency Injection \(Wikipedia\)](https://en.wikipedia.org/wiki/Dependency_injection)
* [AngularJS : Service vs provider vs factory](http://stackoverflow.com/questions/15666048/angularjs-service-vs-provider-vs-factory)
* [AngularJS: Factory vs Service vs Provider](http://tylermcginnis.com/angularjs-factory-vs-service-vs-provider/)
* [AngularJS Service \/ Factory Tutorial with Example](http://viralpatel.net/blogs/angularjs-service-factory-tutorial/)
* [AngularJS 1.x WGW \(What Goes Where\) guide](http://demisx.github.io/angularjs/2014/09/14/angular-what-goes-where.html)

# Angular Templates

## 8. **阅读: **Objectives and Outcomes

## 9. **视频: **Angular Templates

### The ng-include Directive

* Directive used to fetch, compile and include an external HTML fragment

* Usage

  ```
  <div ng-include="'menu.html'"></div>
  ```

  ```
  <ng-include src="'menu.html'"></ng-include>
  ```

* Creates a new scope


## 10. **视频: **Exercise \(Video\): Angular Templates

## 11. **阅读: **Exercise \(Instructions\): Angular Templates

### Objectives and Outcomes

In this exercise, you will explore Angular templates and how they are constructed using HTML. You will then use the ngInclude directive to include an Angular template within a page. At the end of this exercise, you will be able to:

* Construct Angular templates using HTML
* Include Angular templates in a page using the ngInclude directive

### The index.html File

* Download the _index.html_ page provided above and put it in the app folder.
* Next, go to the head of the page and make sure that the &lt;html&gt; tag includes the ngApp directive:

  ```
  <html lang="en" ng-app="confusionApp">
  ```


* Next, edit _menu.html,_ _contactus.html_ and _dishdetail.html_ pages and remove the header information and the scripts from the bottom of the page. Retain only the content enclosed within and including the container div.
* Now go to index.html and include the following between the header and the footer in the page:

  ```
  <ng-include src="'menu.html'"></ng-include>
  ```


Now you can see the resulting web page.

* You can replace the _menu.html_ in the _ngInclude_ above with _dishdetail.html_ and _contactus.html_ to see the result.

### Conclusions

In this exercise we explored Angular templates and the use of the ngInclude directive to include Angular templates within a page.

## 12. **练习测验: **Angular Templates

## 13. **阅读: **Angular Templates: Additional Resources

### Angular Resources

* [Angular Templates](https://docs.angularjs.org/guide/templates)
* [ngInclude](https://docs.angularjs.org/api/ng/directive/ngInclude)

### Other Resources

* [AngularJS–Part 6, Templates](https://lostechies.com/gabrielschenker/2013/12/28/angularjspart-6-templates/)
* [AngularJS Dynamic Templates – Yes We Can!](http://onehungrymind.com/angularjs-dynamic-templates/)

# Angular ngRoute and Single Page Application

## 14. **阅读: **Objectives and Outcomes

## 15. **视频: **Single Page Applications

## 16. **视频: **Angular ngRoute and Single Page Applications

## 17. **视频: **Exercise \(Video\): Angular ngRoute and SPAs

### Deep Linking

* Hyperlink that specifies a link to a searchable or indexed piece of web content

* Example: http:\/\/www.conFusion.food\/index.html\#\/menu\/0

  * The part after \#:  \#\/menu\/0
  * Browser will not reload the page, the browser will think the url part after \# is located within the same page
  * Any chnage to the hash portion does not trigger the page reload


### $location service

* url\(\)

* path\(\)

* search\(\)

* hash\(\)


### Angular ngRoute Module

* Installing

* Manages the interaction between the $location service and the rendered view

* Dependency injection into the module


### $routeProvider

* Enables mapping from the routes to handlers

* Handlers are an object that defines:

  * template URL
  * controller


### ngView Directive

works together with $route service

```
<ng-view></ng-view>
```

```
<div ng-view></div>
```

## 18. **阅读: **Exercise \(Instructions\): Angular ngRoute and SPAs

### Objectives and Outcome

In this exercise, you will explore single page applications and Angular's support for SPA with the ngRoute module. At the end of this exercise, you will be able to:

* Design SPA using Angular support for SPA
* Use the ngRoute module to support SPA

### Set up angular-route

* Use Bower to install angular-route by typing the following at the command prompt:

  ```
  bower install angular-route -S
  ```


Configuring index.html

* Add angular-route.js to the index.html file as follows:

  ```
  <script src="../bower_components/angular-route/angular-route.min.js"></script>
  ```


* Next, replace the ngInclude directive with the ngView directive as follows:

  ```
  <ng-view></ng-view>
  ```


Save _index.html_

### Configuring ngRoute in app.js

* Open app.js and use the dependency injection to include ngRoute as follows:

  ```
  angular.module('confusionApp', ['ngRoute'])
  ```


* Then, add the following code to config the router:

  ```
  .config(function($routeProvider) {
  $routeProvider
  // route for the contactus page
  .when('/contactus', {
    templateUrl : 'contactus.html',
    controller : 'ContactController'
  })
  // route for the menu page
  .when('/menu', {
    templateUrl : 'menu.html',
    controller : 'MenuController'
  })
  // route for the dish details page
  .when('/menu/:id', {
    templateUrl : 'dishdetail.html',
    controller : 'DishDetailController'
  })
  .otherwise('/contactus');
  })
  ```


### Updating services.js

* Open _services.js_ file and configure the dishes object to include an id for each dish object. For each of the dish objects, introduce an id as follows:

  `var dishes=[
  {
    _id:0,
    name:'Uthapizza',
    . . .
  },
  {
    _id:1,
    name:'Zucchipakoda',
    . . .
  }
  ];`


### Configuring menu.html

* Next open _menu.html_ and update the href for the image as follows:

  ```
  <div class="media-left media-middle">
  <a ng-href="#/menu/{{dish._id}}">
   <img class="media-object img-thumbnail" ng-src={{dish.image}} alt="Uthappizza">
  </a>
  </div>
  ```


### Configuring DishDetailController

* Open _controllers.js_ file and update the DishDetailController as follows:

  ```
  .controller('DishDetailController', ['$scope', '$routeParams', 'menuFactory', function($scope, $routeParams, menuFactory) {
  var dish= menuFactory.getDish(parseInt($routeParams.id,10)); 
  $scope.dish = dish;
  }])
  ```


* Save and view the web page.

### Conclusions

In this exercise you explored SPA and used the ngRoute module to design a SPA.

## 19. **练习测验: **Angular ngRoute and SPA

## 20. **阅读: **Angular ngRoute and Single Page Applications: Additional Resources

### Angular Resources

* [Angular ngRoute](https://docs.angularjs.org/api/ngRoute)
* [ngView](https://docs.angularjs.org/api/ngRoute/directive/ngView)
* [$routeProvider](https://docs.angularjs.org/api/ngRoute/provider/$routeProvider)
* [$routeParams](https://docs.angularjs.org/api/ngRoute/service/$routeParams)
* [$location](https://docs.angularjs.org/api/ng/service/$location)

### Other Resources

* [JavaScript parseInt\(\)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/parseInt)
* [Single Page Applications \(Wikipedia\)](https://en.wikipedia.org/wiki/Single-page_application)
* [Deep linking](https://en.wikipedia.org/wiki/Deep_linking)
* [Single Page Apps in depth](http://singlepageappbook.com/)
* [SPA and the Single Page Myth](http://www.johnpapa.net/pageinspa/)
* [Single Page Apps with AngularJS Routing and Templating](https://scotch.io/tutorials/single-page-apps-with-angularjs-routing-and-templating)
* [Pretty URLs in AngularJS: Removing the \#](https://scotch.io/quick-tips/pretty-urls-in-angularjs-removing-the-hashtag)

# Angular UI-Router for Single Page Applications

## 21. **阅读: **Objectives and Outcomes

## 22. **视频: **Angular UI-Router for Single Page Applications

## 23. **视频: **Exercise \(Video\): Angular UI Router and SPAs

## 24. **阅读: **Exercise \(Instructions\): Angular UI-Router for Single Page Applications

### Objectives and Outcomes

In this exercise, you will use the Angular UI-router to design a SPA that makes use of multiple views and nested views in a page. At the end of this exercise, you will be able to:

* Use the Angular UI-Router to design a SPA with multiple and nested views
* Reogranize the application and complete the SPA in a modular manner

### Installing Angular UI-Router

* Use Bower to install angular-ui-router by typing the following at the command prompt:

  ```
  bower install angular-ui-router -S
  ```


### Configuring UI Router

* Open app.js and configure it to use the UI Router. Replace the config function that we had for the ngRoute with the new config for the UI router.
* First, inject the UI router into the module:

  ```
  angular.module('confusionApp', ['ui.router'])
  ```


* Next introduce the config for the UI router:

  ```
  .config(function($stateProvider, $urlRouterProvider) {
    $stateProvider
    // route for the home page
    .state('app', {
      url:'/',
      views: {
        'header': {
        templateUrl : 'views/header.html'
      },
      'content': {
        template : '<h1>To be Completed</h1>',
        controller : 'IndexController'
      },
      'footer': {
        templateUrl : 'views/footer.html'
      }
    }
  })
  // route for the aboutus page
  .state('app.aboutus', {
    url:'aboutus',
    views: {
      'content@': {
        template: '<h1>To be Completed</h1>'
      }
    }
  })
  // route for the contactus page
  .state('app.contactus', {
    url:'contactus',
    views: {
      'content@': {
        templateUrl : 'views/contactus.html',
        controller : 'ContactController'
      }
    }
  })
  // route for the menu page
  .state('app.menu', {
    url: 'menu',
    views: {
      'content@': {
        templateUrl : 'views/menu.html',
        controller : 'MenuController'
      }
    }
  })
  // route for the dishdetail page
  .state('app.dishdetails', {
  url: 'menu/:id',
    views: {
      'content@': {
        templateUrl : 'views/dishdetail.html',
        controller : 'DishDetailController'
      }
    }
  });
  $urlRouterProvider.otherwise('/');
  })
  ```


Updating the DishDetailController

* Update the DishDetailController to use $stateParams as follows:

  ```
  .controller('DishDetailController', [
    '$scope',
    '$stateParams',
    'menuFactory',
    function($scope, $stateParams, menuFactory) { 
      var dish= menuFactory.getDish(parseInt($stateParams.id,10));
      $scope.dish = dish;
    }
  ])
  ```


### Creating View Templates

* In the _app_ folder, create a sub-folder named _views_, and move all the templates into this folder.
* In the views folder, create two new files named _header.html_ and _footer.html_.
* From the _index.html_ page, cut out the _&lt;nav&gt;_ and the _&lt;header&gt;_ part of the page and move it to _header.html_.
* Also, from _index.html_ page, move all the code in the _&lt;footer&gt;_ tag over to footer.html file.
* In _index.html_, replace the _ngView_ with uiView as follows:

  ```
  <div ui-view="header"></div>
  <div ui-view="content"></div>
  <div ui-view="footer"></div>
  ```


* Also, update the &lt;scripts&gt; tag to use angular-ui-router.min.js instead of angular-route.js as follows:

  ```
  <script src="../bower_components/angular-ui-router/release/angular-ui-router.min.js"></script>
  ```


* Open _header.html_ and update the hrefs using ui-srefs as follows:

  ```
    <a class="navbar-brand" ui-sref="app">
      <img src="images/logo.png" height=30 width=41>
    </a>
  </div>
  <div id="navbar" class="navbar-collapse collapse">
    <ul class="nav navbar-nav">
      <li><a ui-sref="app"><span class="glyphicon glyphicon-home" aria-hidden="true"></span> Home</a></li>
      <li><a ui-sref="app.aboutus"><span class="glyphicon glyphicon-info-sign" aria-hidden="true"></span> About</a></li>
      <li><a ui-sref="app.menu"><span class="glyphicon glyphicon-list-alt" aria-hidden="true"></span>Menu</a></li>
      <li><a ui-sref="app.contactus"><i class="fa fa-envelope-o"></i> Contact</a></li>
    </ul>
  </div>
  ```


* Next, update the hrefs in the footer to use ui-srefs as follows:

  ```
  <ul class="list-unstyled">
    <li><a ui-sref="app">Home</a></li>
    <li><a ui-sref="app.aboutus">About</a></li>
    <li><a ui-sref="app.menu">Menu</a></li>
    <li><a ui-sref="app.contactus">Contact</a></li>
  </ul>
  ```


* Make sure you moved _menu.html_, _contactus.html_ and _dishdetail.html_ to the _views_ folder.
* Then, edit _menu.html_ to update the href there to use the ui-sref as follows:

  ```
  <a ui-sref="app.dishdetails({id: dish._id})">
    <img class="media-object img-thumbnail" ng-src={{dish.image}} alt="Uthappizza">
  </a>
  ```


* Finally, edit _dishdetail.html_ file to include a button so that we can click it to return the menu as follows:

  ```
  <div class="col-xs-12">
    <button class="btn btn-xs btn-primary pull-right" type="button" ui-sref="app.menu">Back to Menu</button>
  <div class="media">
  ```


* Save all the files and have a look at the completed SPA

### Conclusions

In this exercise, you used Angular UI-router to design a SPA with multiple and nested views. You saw the powerful features provided by the UI-router.

## 25. **练习测验: **Angular UI-Router and SPAs

## 26. **阅读: **Angular UI-Router and SPAs: Additional Resources

### UI Router Resources

* [Angular UI Router](https://github.com/angular-ui/ui-router)
* [Angular UI Router Guide](https://github.com/angular-ui/ui-router/wiki)
* [Sample App](http://angular-ui.github.io/ui-router/sample/#/)

### Other Resources

* [AngularJS Routing Using UI-Router](https://scotch.io/tutorials/angular-routing-using-ui-router)
* [UI-Router: Why many developers don’t use AngularJS’s built-in router](http://www.funnyant.com/angularjs-ui-router/)

# Assignment 3

## 27. **视频: **Assignment 3 \(Video\): Requirements

## 28. **阅读: **Assignment 3: Additional Resources

### Bootstrap Resources

* [Media Object](http://getbootstrap.com/components/#media)
* [Media List](http://getbootstrap.com/components/#media-list)

