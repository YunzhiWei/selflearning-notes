# Client-Server Communication

## 1. **阅读: **Objectives and Outcomes

## 2. **视频: **Networking Essentials

## 3. **视频: **Exercise \(Video\): Setting up a Server using json-server

## 4. **阅读: **Exercise \(Instructions\): Setting up a Server using json-server

### Objectives and Outcomes

The Node module, _json-server_, provides a very simple way to set up a web server that supports a full-fledged REST API server. We will talk about REST API in the next lesson. It can also serve up static web content from a folder. This lesson will leverage these two features to provide the back-end for your Angular application. In this exercise, you will configure and start a server using _json-server_ to enable serving your application data to your Angular application. At the end of this exercise, you will be able to:

* Configure and start a simple server using the json-server module
* Configure your server to serve up static web content stored in a folder named _public_.

### Installing json-server

* json-server is a node module, and hence can be installed globally by typing the following at the command prompt:

  ```
  npm install json-server -g
  ```


If you are using OSX or Linux, use **sudo** at the front of the command. This will install json-server that can be started from the command line from any folder on your computer.

### Configuring Server Folder

* At any convenient location on your computer, create a new folder named **json-server**, and move to this folder.
* Download the db.json file provided above to this folder.
* Move to this folder in your terminal window, and type the following at the command prompt to start the server:

  ```
  json-server --watch db.json
  ```


* This should start up a server at port number 3000 on your machine. The data from this server can be accessed by typing the following addresses into your **browser address bar**:

  ```
  http://localhost:3000/dishes
  http://localhost:3000/promotions
  http://localhost:3000/leadership
  http://localhost:3000/feedback
  ```


* Type these addresses into the browser address and see the JSON data being served up by the server. This data is obtained from the db.json file

* The json-server also provides a static web server. Any resources that you put in a folder named **public** in the **json-server** folder above, will be served by the server at the following address:

  ```
  http://localhost:3000/
  ```


* Shut down the server by typing **ctrl-C** in the terminal window.

### Configuring gulpfile.js to Generate Dist Folder

* In the previous exercises, you configured the **gulpfile.js** to generate the dist folder from the configuration provided in the **menu.html** file. You will now update the **gulpfile.js** to use the **index.html** file for configuration. Update the usemin task in your **gulpfile.js** as follows:

  ```
  gulp.task('usemin',['jshint'], function () {
    return gulp.src('./app/**/*.html')
      .pipe(usemin({
        css:[minifycss(),rev()],
        js: [ngannotate(),uglify(),rev()]
      }))
      .pipe(gulp.dest('dist/'));});
  ```


* Also, for the browser-sync task, update the configuration as follows:

  ```
  browserSync.init(files, {
    server: {
      baseDir: "dist",
      index: "index.html"
    }
  });
  ```


* Now if you run gulp at the command prompt, it creates the dist folder containing the distribution files.
* Copy the entire contents of the **dist** folder to the **public** folder that you created above.
* Restart the server. Now you can access the website being served up by your server by typing [http:\/\/localhost:3000\/](http://localhost:3000/)in the browser address bar.

### Conclusions

In this exercise, you learnt how to configure and start a simple server using the** json-server** node module. You also learnt how the server can serve up static web content.

## 5. **练习测验: **Client-Server Communication

## 6. **阅读: **Client-Server Communication: Additional Resources

### Other Resources

* [json-server](https://github.com/typicode/json-server)
* [Creating Demo APIs with json-server](https://egghead.io/lessons/nodejs-creating-demo-apis-with-json-server)
* [JSON](http://www.json.org/)

# Angular http Service

## 7. **阅读: **Objectives and Outcomes

## 8. **视频: **Client-Server Communication using $http

## 9. **视频: **Exercise \(Video\): Client-Server Communication using $http

## 10. **阅读: **Exercise \(Instructions\): Client-Server Communication using $http

### Objectives and Outcomes

In this exercise, you will learn about how to use the built-in Angular $http service to communicate with the server and retrieve the data from the server. At the end of this exercise, you will be able to:

* Use the $http service to retrieve data from a server using the $http.get\(\) method
* Use the retrieved data to render the page in your web application

### Updating Services

* Open _services.js_ to update it to retrieve data from the server. First add a constant to the Angular module as follows:

  ```
  angular.module('confusionApp')
  .constant("baseURL","http://localhost:3000/")
  ```


* Next you will do dependency injection into the menuFactory service of the $http service and baseURL constant as follows:

  ```
  .service('menuFactory', ['$http', 'baseURL', function($http,baseURL) {
    . . .
  }])
  ```


Make sure to put the closing \] at the end of the service function, to close the dependency array.

* Then, you will go into the _menuFactory_ service and delete the _dishes_ object from there. You will download the dishes information from the server.
* Next, update the two method in the _menuFactory_ service to use the $http service as follows:

  ```
  this.getDishes = function(){
    return $http.get(baseURL+"dishes");
  };
  this.getDish = function (index) {
    return $http.get(baseURL+"dishes/"+index);
  };
  ```


* Save the _services.js_ file and then open _controllers.js_ file.

### Updating the Controllers

* Update the code in the _MenuController_ to retrieve the data from the service as follows:

  ```
  $scope.dishes= [];
  menuFactory.getDishes()
  .then( function(response) {
    $scope.dishes = response.data;
  }
  );
  ```


* Similarly update the _DishDetailController_ as follows:

  ```
  $scope.dish = {};
  menuFactory.getDish(parseInt($stateParams.id,10))
  .then(function(response) {
    $scope.dish = response.data;
    $scope.showDish=true;
  }
  );
  ```


* Also update the IndexController to retrieve the data for the dish from the server as follows:

  ```
  $scope.dish = {};
  menuFactory.getDish(0)
  .then(function(response) {
    $scope.dish = response.data;
    $scope.showDish = true;
  }
  );
  ```


* Save _controllers.js_ and then open _menu.html_
* Update the following code in menu.html as shown below to remove the \_ from the id:

  ```
  <a ui-sref="app.dishdetails({id: dish.id})">
  ```


* Save the changes in _menu.html_ and then view the web page in the browser.

### Conclusions

In this exercise, we updated the app to retrieve the data from the server using the $http.get\(\) request.

## 11. **视频: **Exercise \(Video\): Handling Errors in Client-Server Communication using $http

## 12. **阅读: **Exercise \(Instructions\): Handling Errors in Client-Server Communication using $http

### Objectives and Outcomes

In this exercise, we will update the code in the controllers to be able to handle errors that might be caused when errors occur while retrieving data from the server. At the end of this exercise, you will be able to:

* Handling errors in communication between the client and the server.
* Ensure that the user is delivered meaningful message on the web page to indicate error in communicating with the server.

### Updating the Controllers

* Open _controllers.js_ to update the code to handle errors. Update the code in the _MenuController_ as follows:

  ```
  $scope.showMenu = false;
  $scope.message = "Loading ...";
  $scope.dishes= {};
  menuFactory.getDishes()
  .then(
  function(response) {
    $scope.dishes = response.data;
    $scope.showMenu = true;
  },
  function(response) {
    $scope.message = "Error: "+response.status + " " + response.statusText;
  }
  );
  ```

* Now, open \_menu.html \_and update the code as follows:

  ```
  <div class="row row-content" ng-controller="MenuController">
  <div class="col-xs-12" ng-if="!showMenu">
    <h3>{{message}}</h3>
  </div>
  <div class="col-xs-12" ng-if="showMenu">
  ```


Note the use of the _ngIf_ directive in order to add\/delete the div from the DOM.

* Next, update _DishDetailController_ in _controllers.js_ as follows:

  ```
  $scope.dish = {};
  $scope.showDish = false;
  $scope.message="Loading ...";
  menuFactory.getDish(parseInt($stateParams.id,10))
  .then(
  function(response){
    $scope.dish = response.data;
    $scope.showDish=true;
  },
  function(response) {
    $scope.message = "Error: "+response.status + " " + response.statusText;
  }
  );
  ```


* Also, update _IndexController_ as follows:

  ```
  $scope.dish = {};
  $scope.showDish = false;
  $scope.message="Loading ...";
  menuFactory.getDish(0)
  then(
  function(response){
    $scope.dish = response.data;
    $scope.showDish = true;
  },
  function(response) {
    $scope.message = "Error: "+response.status + " " + response.statusText;
  }
  );
  ```

* Then, update the _dishdetail.html_ as follows:

  ```
  <div class="row row-content" ng-controller="DishDetailController">
    <div class="col-xs-12" ng-if="!showDish">
      <h3>{{message}}</h3>
    </div>
  <div class="col-xs-12" ng-if="showDish">
  ```

* Also update _home.html_ as follows:

  ```
  <div class="col-xs-12 col-sm-9 col-sm-pull-3">
    <div ng-if="!showDish">
      <h3>{{message}}</h3>
    </div>
  <div class="media" ng-if="showDish">
  ```


* Save all the changes and then have a look at the web page.

### Conclusions

In this exercise, we extended the previous exercise to handle errors that result during access to the server.

## 13. **练习测验: **Client-Server Communication with $http

## 14. **阅读: **Client-Server Communication using $http: Additional Resources

### Angular Resources

* [$http](https://docs.angularjs.org/api/ng/service/$http)
* [ngIf](https://docs.angularjs.org/api/ng/directive/ngIf)
* [Angular's promise service: $q](https://docs.angularjs.org/api/ng/service/$q)

### Other Resources

* [Making API Calls in AngularJS using Angular’s $http service](http://www.sitepoint.com/api-calls-angularjs-http-service/)

# RESTful Services and Angular $resource

## 15. **阅读: **Objectives and Outcomes

## 16. **视频: **Brief Representational State Transfer \(REST\)

## 17. **视频: **Client-Server Communication using $resource

## 18. **视频: **Exercise \(Video\):Client-Server Communication using $resource

## 19. **阅读: **Exercise \(Instructions\): Client-Server Communication using $resource

### Objectives and Outcomes

In this exercise, you will make use of the Angular ngResource module and Angular $resource to access the data from a server that supports REST API. At the end of this exercise, you will be able to:

* Install and use Angular _ngResource_ module
* Use Angular $resource to access the server that exports a REST API.

### Installing ngResource

* First, you will install the Angular _ngResource_ module in your conFusion project by typing the following at the command prompt when you are in the conFusion folder:

  ```
  bower install angular-resource -S
  ```


* Remember to add angular-resource.min.js to the index.html file by including the following in the scripts section of the page, right after including angular-ui-router:

  ```
  <script src="../bower_components/angular-resource/angular-resource.min.js"></script>
  ```


* Inject the _ngResource_ module into the Angular module by updating the angular.module\(\) in _app.js_ as follows:

  ```
  angular.module('confusionApp', ['ui.router','ngResource'])
  ```


Updating Services

* Next, open _services.js_ and update the code in _menuFactory_ as follows to use Angular $resource:

  ```
  .service('menuFactory', ['$resource', 'baseURL', function($resource,baseURL) {
  ```


* Then update the _getDishes\(\)_ function as follows:

  ```
  this.getDishes = function(){
  return $resource(baseURL+"dishes/:id",null, {'update':{method:'PUT' }});
  };
  ```


* Delete the _getDish\(index\)_ function as we no longer need it. Save _services.js_.

### Updating Controllers

* Open _controllers.js_ and update the code in _MenuController_ as follows:

  ```
  $scope.showMenu = true;
  $scope.message = "Loading ...";
  $scope.dishes = menuFactory.getDishes().query();
  ```


* Similarly update the _DishDetailController_ as follows:

  ```
  $scope.showDish = true;
  $scope.message="Loading ...";
  $scope.dish = menuFactory.getDishes().get({id:parseInt($stateParams.id,10)});
  ```


* Finally, update the code in _IndexController_ as follows:

  ```
  $scope.showDish = true;
  $scope.message="Loading ...";
  $scope.dish = menuFactory.getDishes().get({id:0});
  ```


* Save the changes and have a look at the web application in the browser.

### Conclusions

In this exercise you used the Angular ngResource module and Angular $resource to access a RESTful server.

## 20. **视频: **Exercise \(Video\): Handling Errors in Client-Server Communication using $resource

## 21. **阅读: **Exercise \(Instructions\): Handling Errors in Client-Server Communication using $resource

### Objectives and Outcomes

In this exercise, you will be updating the previous exercise to handle errors that might result while accessing the server. Also you will be able to save the user's comments about a dish submitted through the form in dishdetail.html. At the end of this exercise, you will be able to:

* Handle errors caused during communication with a server using Angular $resource
* Submit user's comments about a dish to the server by updating the information on the server.

### Updating Controllers

* Open _controllers.js_ and update the MenuController as follows:

  ```
  $scope.showMenu = false;
  $scope.message = "Loading ...";
  menuFactory.getDishes().query(
  function(response) {
    $scope.dishes = response;
    $scope.showMenu = true;
  },
  function(response) {
    $scope.message = "Error: "+response.status + " " + response.statusText;
  });
  ```


* Similarly update the DishDetailController as follows:

  ```
  $scope.showDish = false;
  $scope.message="Loading ...";
  $scope.dish = menuFactory.getDishes().get({id:parseInt($stateParams.id,10)})
  .$promise.then(
    function(response){
  $scope.dish = response;
  $scope.showDish = true;
  },
  function(response) {
    $scope.message = "Error: "+response.status + " " + response.statusText;
  }
  );
  ```


* Finally update the IndexController as follows:

  ```
  $scope.showDish = false;
  $scope.message="Loading ...";
  $scope.dish = menuFactory.getDishes().get({id:0})
  .$promise.then(
  function(response){
    $scope.dish = response;
    $scope.showDish = true;
  },
  function(response) {
    $scope.message = "Error: "+response.status + " " + response.statusText;
  }
  );
  ```


Updating Information on the Server

* Now you will update the DishCommentController as follows in order to submit the user's comments about a dish to the server. Inject the _menuFactory_ to the _DishCommentController_:

  ```
  .controller('DishCommentController', ['$scope', 'menuFactory', function($scope,menuFactory) {
  ```


* Also, update the submitComment\(\) function as follows:

  ```
  $scope.submitComment = function () {
  $scope.mycomment.date = new Date().toISOString();
  console.log($scope.mycomment);
  $scope.dish.comments.push($scope.mycomment);
  menuFactory.getDishes().update({id:$scope.dish.id},$scope.dish);
  $scope.commentForm.$setPristine();
  $scope.mycomment = {rating:5, comment:"", author:"", date:""};
  }
  ```


* Save the changes and see the updated web application.

### Conclusions

In this exercise you learnt to handle errors that might be caused while accessing the server using Angular $resource. In addition, you were able to update the information on the server when the user submits a comment about a dish through the comment form.

## 22. **练习测验: **RESTful Services and Angular $resource

## 23. **阅读: **RESTful Services and Angular $resource: Additional Resources

### Angular Resources

* [Angular $resource](https://docs.angularjs.org/api/ngResource/service/$resource)
* [Angular ngResource](https://docs.angularjs.org/api/ngResource)

### Other Resources

* [Representational State Transfer \(Wikipedia\)](https://en.wikipedia.org/wiki/Representational_state_transfer)
* [Create, read, update and delete \(Wikipedia\)](https://en.wikipedia.org/wiki/Create,_read,_update_and_delete)
* [Web Service \(Wikipedia\)](https://en.wikipedia.org/wiki/Web_service)
* [Creating a CRUD App in Minutes with Angular’s $resource](http://www.sitepoint.com/creating-crud-app-minutes-angulars-resource/)
* [Consuming RESTful APIs](http://fdietz.github.io/recipes-with-angular-js/consuming-external-services/consuming-restful-apis.html)
* [How to Improve Your REST Calls in Angular With ngResource](http://devdactic.com/improving-rest-with-ngresource/)

# Angular Testing

## 24. **阅读: **Objectives and Outcomes

## 25. **视频: **Angular Testing

## 26. **视频: **Exercise \(Video\): Unit Testing Angular Applications

## 27. **阅读: **Exercise \(Instructions\): Unit Testing Angular Applications

### Objectives and Outcomes

In this exercise, you will learn about unit testing in your Angular applications. You will learn about Angular mocks, Karma, and Jasmine and learn how to use them to carry out unit testing and e2e testing. At the end of this exercise, you should be able to:

* Configure a Karma configuration file
* Set up unit tests using Jasmine and carry out the unit test automatically

### Setting up the Unit Test Environment

* First, set up Jasmine core to be available for use within your project:

  ```
  npm install jasmine-core --save-dev
  ```


* Then, set up the Karma command line tools globally as follows:

  ```
  npm install karma-cli -g
  ```


Remember to use sudo if you are in OSX or Linux environments.

* Then set up karma-jasmine plugin to make use of Jasmine with Karma:

  ```
  npm install karma-jasmine --save-dev
  ```


* In order to set up browser environments to carry out the tests, set up PhantomJS, and Karma launchers for PhantomJS and Chrome as follows:

  ```
  npm install phantomjs karma-phantomjs-launcher karma-chrome-launcher --save-dev
  ```


You can also set up for Firefox, IE and Safari if you use these browsers.

### Setting up Angular Mocks

* You should also install the ngMock module as follows:

  ```
  bower install angular-mocks -S
  ```


### Unit Testing of MenuController

* Next, we will configure Karma to conduct the unit test. First, create a folder in _conFusion_ folder, named _test_.
* Move to the _test_ folder, and create a file named _karma.conf.js_ there. This file will contain the configuration information for the Karma tests. Add the following configuration to the file:

  ```
  // Karma configuration
  module.exports = function(config) {
    config.set({
      // base path that will be used to resolve all patterns (eg. files, exclude)
      basePath: '../',
      // frameworks to use
      // available frameworks: https://npmjs.org/browse/keyword/karma-adapter
      frameworks: ['jasmine'],
    })
  }
  ```


* Next, add the list of files to be included, and those to be excluded into the config as follows:

  ```
  // list of files / patterns to load in the browser
  files: [
    'bower_components/angular/angular.js',
    'bower_components/angular-resource/angular-resource.js',
    'bower_components/angular-ui-router/release/angular-ui-router.js',
    'bower_components/angular-mocks/angular-mocks.js',
    'app/scripts/*.js',
    'test/unit/**/*.js'
  ],
  // list of files to exclude
  exclude: [
    'test/protractor.conf.js',
    'test/e2e/*.js'
  ],
  ```


* The add some configuration information as follows. See the comments for details:

  ```
  // preprocess matching files before serving them to the browser
  // available preprocessors: https://npmjs.org/browse/keyword/karma-preprocessor
  preprocessors: {
  },
  // test results reporter to use
  // possible values: 'dots', 'progress'
  // available reporters: https://npmjs.org/browse/keyword/karma-reporter
  reporters: ['progress'],
  // web server port
  port: 9876,
  // enable / disable colors in the output (reporters and logs)
  colors: true,
  // level of logging
  // possible values: config.LOG_DISABLE || config.LOG_ERROR || config.LOG_WARN || config.LOG_INFO || config.LOG_DEBUG
  logLevel: config.LOG_INFO,
  // enable / disable watching file and executing tests whenever any file changes
  autoWatch: true,
  ```


* Next, let us configure the browsers to use for testing as follows:

  ```
  // start these browsers
  // available browser launchers: https://npmjs.org/browse/keyword/karma-launcher
  browsers: ['Chrome','PhantomJS', 'PhantomJS_custom'],
  // you can define custom flags
  customLaunchers: {
    'PhantomJS_custom': {
      base: 'PhantomJS',
      options: {
        windowName: 'my-window',
        settings: {
          webSecurityEnabled: false
        },
      },
      flags: ['--load-images=true'],
      debug: true
    }
  },
  phantomjsLauncher: {
    // Have phantomjs exit if a ResourceError is encountered (useful if karma exits without killing phantom)
    exitOnResourceError: true
  },
  // Continuous Integration mode
  // if true, Karma captures browsers, runs the tests and exits
  singleRun: false,
  // Concurrency level
  // how many browser should be started simultaneous
  concurrency: Infinity
  ```


* Save the changes. Now the Karma configuration is ready for launching the test. Next we create a test for MenuController.
* Create a folder named _unit_ in the _test_ folder. Move to the _unit_ folder and then create a folder there named _controllers_. Then move to the _controllers_ folder. We will store the tests for the controllers here.
* Create a file named _menucontroller.js_ and start the configuration of the test as follows:

  ```
  describe('Controller: MenuController', function () {
    // load the controller's module
    beforeEach(module('confusionApp'));
    var MenuController, scope, $httpBackend;
  });
  ```


* Now we will inject the mock dependencies as follows:

  ```
  // Initialize the controller and a mock scope
  beforeEach(inject(function ($controller, _$httpBackend_, $rootScope, menuFactory) {
    // place here mocked dependencies
    $httpBackend = _$httpBackend_;
    $httpBackend.expectGET("http://localhost:3000/dishes").respond([
      {
        "id": 0,
        "name": "Uthapizza", 
        "image": "images/uthapizza.png",
        "category": "mains",
        "label": "Hot",
        "price": "4.99",
        "description": "A",
        "comments":[{}]
      },
      {
        "id": 1,
        "name": "Zucchipakoda",
        "image": "images/zucchipakoda.png",
        "category": "mains",
        "label": "New",
        "price": "4.99",
        "description": "A",
        "comments":[{}]
      }
    ]);
    scope = $rootScope.$new();
    MenuController = $controller('MenuController', {
      $scope: scope, menuFactory: menuFactory
    });
    $httpBackend.flush();
  }));
  ```


* Finally, set up all the tests in the file as follows:

  ```
  it('should have showDetails as false', function () {
    expect(scope.showDetails).toBeFalsy();
  });
  it('should create "dishes" with 2 dishes fetched from xhr', function(){
    expect(scope.showMenu).toBeTruthy();
    expect(scope.dishes).toBeDefined();
    expect(scope.dishes.length).toBe(2);
  });
  it('should have the correct data order in the dishes', function() {
    expect(scope.dishes[0].name).toBe("Uthapizza");
    expect(scope.dishes[1].label).toBe("New");
  });
  it('should change the tab selected based on tab clicked', function(){
    expect(scope.tab).toEqual(1);
    scope.select(3);
    expect(scope.tab).toEqual(3);
    expect(scope.filtText).toEqual('mains');
  });
  ```


* Save the changes. Now the test is ready to be executed.
* Move back to the _test_ folder and then type the following at the prompt to execute the test:

  ```
  karma start karma.conf.js
  ```


* All the tests should successfully complete. You can edit some of the test values to cause some of the tests to fail.

### Conclusions

In this exercise, you learnt about using Karma and Jasmine to carry out unit tests on Angular application components.

## 28. **视频: **End-to-end Testing Angular Applications

## 29. **视频: **Exercise \(Video\): End-to-End Testing Angular Applications

## 30. **阅读: **Exercise \(Instructions\): End-to-End Testing Angular Applications

### Objectives and Outcomes

In this exercise, you will learn about end-to-end \(e2e\) testing in your Angular applications. You will learn about Protractor and learn how to use them to carry out e2e testing. At the end of this exercise, you should be able to:

* Configure a protractor configuration file
* Set up e2e tests using Jasmine and carry out the e2e test automatically

**Note**: You should have completed the previous exercise on unit testing before proceeding with this exercise. Some of the set up is common for both unit tests and e2e tests. These were already done in the previous exercise.

### Setting up the E2E Test Environment

* Set up the protractor tool globally for use in e2e testing:

  ```
  npm install protractor -g
  ```


Remember to use sudo if you are in OSX or Linux environments.

* The above also installs webdriver-manager. Then, update your web drivers by typing:

  ```
  webdriver-manager update
  ```


Remember to use sudo if you are in OSX or Linux environments.

* Make sure that you are running the json-server to serve up the REST API for accessing the JSON data by your Angular application.
* Next, you need to start a server to serve up the Angular application. Fortunately, Gulp is already set up to do that. Make sure you are in the _conFusion_ folder. At the command prompt, type:

  ```
  gulp watch
  ```


This will start the server and serve the page at [http:\/\/localhost:3001\/.](http://localhost:3001/) Make sure about the port number \(3001\) where your server is serving up the web page.

### Configuring Protractor

* Next, move to the _test_ folder and create a file named _protractor.conf.js_ and add the following configuration code to it:

  ```
  exports.config = {
    allScriptsTimeout: 11000,
    specs: [
      'e2e/*.js'
    ],
    capabilities: {
      'browserName': 'chrome'
    },
    baseUrl: 'http://localhost:3001/',
    framework: 'jasmine',
    directConnect: true,
    jasmineNodeOpts: {
      defaultTimeoutInterval: 30000
    }
  };
  ```


Here we are using the directConnect option to directly connect to the browser to conduct the tests, rather than through the Selenium web server.

* Next, create a folder named _e2e_ in the _test_ folder, and move to the _e2e_ folder.
* Create a file named _scenarios.js_. This fill will contain all the e2e tests that we will execute on the application.
* Add the following code to the file:

  ```
  'use strict';
  describe('conFusion App E2E Testing', function() {
  });
  ```


* Now we will introduce the tests into this file. First check to make sure that you are redirected to the index.html file:

  ```
  it('should automatically redirect to / when location hash/fragment is empty', function() {
    browser.get('index.html');
    expect(browser.getLocationAbsUrl()).toMatch("/");
  });
  ```


* Next, we will set up a simple test for the index file to check if the page title is set correctly:

  ```
  describe('index', function() {
    beforeEach(function() {
      browser.get('index.html#/');
    });
    it('should have a title', function() {
      expect(browser.getTitle()).
      toEqual('Ristorante Con Fusion');
    });
  });
  ```


* Next, we will navigate to the first menu item, and test a few properties there:

  ```
  describe('menu 0 item', function() {
    beforeEach(function() {
    browser.get('index.html#/menu/0');
  });
  it('should have a name', function() {
    var name = element(by.binding('dish.name'));
    expect(name.getText()).
    toEqual('Uthapizza Hot $4.99');
  });
  it('should show the number of comments as', function() {
    expect(element.all(by.repeater('comment in dish.comments'))
    .count()).toEqual(5);
  });
  it('should show the first comment author as', function() {
    element(by.model('orderText')).sendKeys('author');
    expect(element.all(by.repeater('comment in dish.comments'))
    .count()).toEqual(5);
    var author = element.all(by.repeater('comment in dish.comments'))
    .first().element(by.binding('comment.author'));
    expect(author.getText()).toContain('25 Cent');
  });
  });
  ```


* Save the changes and then move back to the _test_ folder.
* At the command prompt, type the following to execute the e2e tests:

  ```
  protractor protractor.conf.js
  ```


* All the tests should pass successfully. You can modify some of the inputs to the text to see them fail.

### Conclusions

In this exercise, you used Protractor together with Jasmine to carry out several e2e tests on your Angular application.

## 31. **练习测验: **Angular Testing

## 32. **阅读: **Angular Testing: Additional Resources

### Angular Resources

* [Unit Testing](https://docs.angularjs.org/guide/unit-testing)
* [End-to-End Testing](https://docs.angularjs.org/guide/e2e-testing)
* [Angular Mocks: ngMock](https://docs.angularjs.org/api/ngMock)
* [$controller](https://docs.angularjs.org/api/ngMock/service/$controller)
* [$httpBackend ](https://docs.angularjs.org/api/ngMock/service/$httpBackend)\(for unit testing\)
* [angular.mock.inject](https://docs.angularjs.org/api/ngMock/function/angular.mock.inject)
* [angular.mock.module](https://docs.angularjs.org/api/ngMock/function/angular.mock.module)
* [Angular Mocks: ngMockE2E](https://docs.angularjs.org/api/ngMockE2E)
* [$httpBackend](https://docs.angularjs.org/api/ngMockE2E/service/$httpBackend) \(for E2E\)

### Testing Tools and Environments

* [Jasmine 2.3](http://jasmine.github.io/2.3/introduction.html)
* [Karma](http://karma-runner.github.io/0.13/index.html)
* [Protractor](https://angular.github.io/protractor/#/)
* [Selenium](http://www.seleniumhq.org/)

### Articles and Blogs

* [Test-Driven Development](https://en.wikipedia.org/wiki/Test-driven_development)
* [Unit testing with Karma and Jasmine for AngularJS](https://blog.logentries.com/2015/01/unit-testing-with-karma-and-jasmine-for-angularjs/)
* [Unit Testing in AngularJS applications with Karma and Jasmine](http://blog.mwaysolutions.com/2015/04/02/unit-testing-in-angularjs-applications-with-karma-and-jasmine/)
* [AngularJS Testing with Karma and Jasmine](http://www.tuesdaydeveloper.com/2013/06/angularjs-testing-with-karma-and-jasmine/)
* [An Introduction To Unit Testing In AngularJS Applications](http://www.smashingmagazine.com/2014/10/introduction-to-unit-testing-in-angularjs/)
* [Testing AngularJS apps with Protractor](https://www.thoughtworks.com/insights/blog/testing-angularjs-apps-protractor)
* [Practical End-to-End Testing with Protractor](http://www.ng-newsletter.com/posts/practical-protractor.html)
* [Testing AngularJS With Protractor and Karma - Part 1](http://mherman.org/blog/2015/04/09/testing-angularjs-with-protractor-and-karma-part-1/#.VllJz5J94vo)
* [Testing AngularJS With Protractor and Karma - Part 2](http://mherman.org/blog/2015/04/26/testing-angularjs-with-protractor-and-karma-part-2/#.VllJipJ94vo)

# Web Tools: Yo and Yeoman

## 33. **阅读: **Objectives and Outcomes

## 34. **视频: **Web Tools: Yo and Yeoman

### Install yo

```
npm install yo -g
```

Or you may try this command


```
npm install -g yo --ignore-scripts
```

### Install generators

There are many generators  in [yeoman.io](http://yeoman.io/generators/)

Here we just install generator for angular.

```
npm install generator-angular -g
```

### Scaffold a project by yo

Create a folder for the new project. And then go into that folder.

Create the project by the following command

```
yo angular
```

## 35. **阅读: **Web Tools: Yo and Yeoman: Additional Resources

### Useful Links

* [The Yeoman workflow](http://yeoman.io/)
* [Yeoman Generators](http://yeoman.io/generators/)
* [generator-angular](https://github.com/yeoman/generator-angular#readme)
* [Yeoman: Learning Resources](http://yeoman.io/learning/resources.html)

# Assignment 4

## 36. **视频: **Assignment 4 \(Video\): Requirements

## 37. **阅读: **Assignment 4: Additional Resources

### Angular Resources

* [Angular ngResource](https://docs.angularjs.org/api/ngResource)
* [Angular $resource](https://docs.angularjs.org/api/ngResource/service/$resource)
* [ngIf directive](https://docs.angularjs.org/api/ng/directive/ngIf)

# Conclusions

## 38. **视频: **Conclusions

## 39. **阅读: **Conclusions: Additional Resources

