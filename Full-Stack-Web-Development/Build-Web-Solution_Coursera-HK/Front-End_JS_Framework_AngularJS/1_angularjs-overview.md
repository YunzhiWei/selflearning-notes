# Full-Stack Web Development: The Big Picture

## 1. **阅读: **Objectives and Outcomes

## 2. **视频: **What is Full-Stack Web Development?

## 3. **视频: **Course Overview

## 4. **视频: **How to Use the Learning Resources?

## 5. **阅读: **Full Stack Web Development: Additional Resources

### Useful Links

* [What is a Full Stack developer?](http://www.laurencegellert.com/2012/08/what-is-a-full-stack-developer/)
* [Wait, Wait… What is a Full-stack Web Developer After All?](http://edward-designer.com/web/full-stack-web-developer/)
* [The Myth of the Full-stack Developer](http://andyshora.com/full-stack-developers.html)
* [Multi-tier Architecture](https://en.wikipedia.org/wiki/Multitier_architecture)
* [What is the 3-Tier Architecture?](http://www.tonymarston.net/php-mysql/3-tier-architecture.html)

# Introcution to AngularJS

## 6. **阅读: **Objectives and Outcomes

## 7. **视频: **Front-End JavaScript Frameworks Overview

## 8. **视频: **Introduction to AngularJS

## 9. **视频: **Exercise \(Video\): Introduction to AngularJS

## 10. **阅读: **Exercise \(Instructions\): Introduction to AngularJS

### Objectives and Outcomes

This first exercise introduces you to the basics of AngularJS. In this exercise, you will explore how to use various AngularJS directives within a web application. At the end of this exercise, you will be able to:

* Use Angular directives like ng-app, ng-init, ng-model and ng-repeat
* Use Angular expressions in constructing a web template.

**NOTE: If you are continuing this course from the second course of the specialization about Bootstrap, you would have created a folder named \*\***_conFusion_**** that stored your web site that you were developing for the exercises and assignments. You may wish to save a copy of this folder elsewhere on your computer before you proceed further. You should then delete the existing conFusion folder because we will set up a new ****_conFusion_**\*\* folder that is appropriately configured for this course in the next step.**

### Setting up for the Exercises

* Download the _conFusion.zip_ file \(shown above\) that we provide for you to a convenient location on your computer and unzip it. This will create a folder named _conFusion_ at that location.
* Browse the folder to see the contents therein.

### The Power of Bower

* Open a terminal window and go to the _conFusion_ folder. Then at the prompt type:
  ```
  bower install
  ```


This will result in Bower fetching Bootstrap, JQuery, Font Awesome and Angular files for us and putting them into the _bower\_components_ folder.

* Once Bower completes the installation, your project folder is now all set to go forward with the exercise.

### Examining menu.html

* Open the _conFusion_ folder in your favorite text editor, and then open _menu.html_ file to view its contents.
* You will note that the file is already configured to include the Bootstrap CSS files and other CSS files from the folder. Also the body contains some empty divs. We will introduce the restaurant's menu into these divs.

### Adding Angular to the File

* We will now set up the page to use Angular by including the Angular JavaScript files into the menu.html page by adding the following code to the bottom of the page, just before the closing body tag:
  ```
  <script src="../bower_components/angular/angular.min.js"></script>
  ```


Note that we are using the Angular files that Bower has downloaded for us.

### Configuring the Angular Application

* Next we configure our web page to be an Angular application. Go to the _**&lt;html&gt;**_ tag at the top of the page and then add the _ng-app_ angular directive to it to configure the page to be an Angular application. This will bootstrap the Angular application on the page:

  ```
  <html lang="en" ng-app>
  ```


### Adding Data using ng-init

* Next go to the content row in the body of the page, and add some data to be used within the application, by using the _ng-init_ directive as follows:

  ```
  <div class="row row-content"
    ng-init="
      dish=
      {
        name:'Uthapizza',
        image: 'images/uthapizza.png',
        category: 'mains',
        label:'Hot',
        price:'4.99',
        description:'A unique combination of Indian Uthappam (pancake) and Italian pizza, topped with Cerignola olives, ripe vine cherry tomatoes, Vidalia onion, Guntur chillies and Buffalo Paneer.',
        comment: ''
      }">
  ```


This includes a JavaScript object named dish into the code. Browse the contents of this object.

### Adding Menu Item using Media Object

* We will now make use of the Bootstrap media object to introduce a menu item into the inner column div as follows:

```
<div class="col-xs-12">
  <div class="media">
    <div class="media-left media-middle">
      <a href="#">
        <img class="media-object img-thumbnail" ng-src={{dish.image}} alt="Uthappizza">
      </a>
    </div>
    <div class="media-body">
      <h2 class="media-heading">{{dish.name}}
        <span class="label label-danger">{{dish.label}}</span>
        <span class="badge">{{dish.price | currency}}</span>
      </h2>
      <p>{{dish.description}}</p>
    </div>
  </div>
</div>
```

Note the use of Angular expressions with the curly braces to include various properties of the JavaScript object to construct the menu item.

* Also, in this code, note the use of the Angular \_currency\_ filter to display the price within the badge. We'll deal with Angular filters in a subsequent lesson.

### Examining Two-way Binding

* Note the presence of a property called comment in the dish object. We will use two-way data binding feature of Angular to update this comment from an input box on the page, and see the updated comment immediately reflected to the web page.

* Update the media object in the column div as follows:


```
<div class="col-xs-12">
  <div class="media">
    . . .
    <p>{{dish.description}}</p>
    <p>Comment: {{dish.comment}}</p>
    <p>Type your comment: <input type="text" ng-model="dish.comment"></p>
  </div>
</div>
</div>
```

We are adding three new lines with the _&lt;p&gt;comment: ... &lt;\/p&gt;_ and the _&lt;p&gt;Type your comment: ... &lt;\/p&gt;_ with the input box to the HTML code.

### Object Array and ng-repeat

* We will now update the ng-init to contain an array of JavaScript objects as follows:

```
<div class="row row-content"
  ng-init="
    dishes=[
    {
      name:'Uthapizza',
      image: 'images/uthapizza.png',
      category: 'mains',
      label:'Hot',
      price:'4.99',
      description:'A unique combination of Indian Uthappam (pancake) and Italian pizza, topped with Cerignola olives, ripe vine cherry tomatoes, Vidalia onion, Guntur chillies and Buffalo Paneer.',
      comment: ''
    },
    {
      name:'Zucchipakoda',
      image: 'images/zucchipakoda.png',
      category: 'appetizer',
      label:'',
      price:'1.99',
      description:'Deep fried Zucchini coated with mildly spiced Chickpea flour batter accompanied with a sweet-tangy tamarind sauce',
      comment: ''
    },
    {
      name:'Vadonut',
      image: 'images/vadonut.png',
      category: 'appetizer',
      label:'New',
      price:'1.99',
      description:'A quintessential ConFusion experience, is it a vada or is it a donut?',
      comment: ''
    },
    {
      name:'ElaiCheese Cake',
      image: 'images/elaicheesecake.png',
      category: 'dessert',
      label:'',
      price:'2.99',
      description:'A delectable, semi-sweet New York Style Cheese Cake, with Graham cracker crust and spiced with Indian cardamoms',
      comment: ''
    }
  ]">
```

* Next we will update the code in the column div to create a list of media objects so that the menu can be displayed on the page constructed from the JavaScript object array. We take the help of the _ng-repeat_ directive for this. Update the code as follows:

```
<div class="col-xs-12">
  <ul class="media-list">
    <li class="media" ng-repeat="dish in dishes">
      <div class="media-left media-middle">
        <a href="#"> <img class="media-object img-thumbnail" ng-src={{dish.image}} alt="Uthappizza"> </a>
      </div>
      <div class="media-body">
        <h2 class="media-heading">{{dish.name}}
          <span class="label label-danger">{{dish.label}}</span>
          <span class="badge">{{dish.price | currency}}</span>
        </h2>
        <p>{{dish.description}}</p>
        <p>Comment: {{dish.comment}}</p>
        <p>Type your comment: <input type="text" ng-model="dish.comment"></p>
      </div>
    </li>
  </ul>
</div>
```

### Conclusions

In this exercise, you learnt about configuring an Angular app, and use various ng-\* Angular directives to construct the menu. It is interesting to note that you have not written a single line of JavaScript code for this exercise, but still get a lot of dynamic functionality in the page.

## 11. **练习测验: **Introduction to AngularJS

## 12. **阅读: **Introduction to AngularJS: Additional Resources

### Angular Resources

* [Angular Official Website](https://angularjs.org/)
* [Angular Documentation](https://docs.angularjs.org/guide)
* [What is AngularJS?](https://docs.angularjs.org/guide/introduction)
* [Angular Data Binding](https://docs.angularjs.org/guide/databinding)
* Angular Directives: [ng-app](https://docs.angularjs.org/api/ng/directive/ngApp), [ng-init](https://docs.angularjs.org/api/ng/directive/ngInit), [ng-model](https://docs.angularjs.org/api/ng/directive/ngModel), [ng-repeat](https://docs.angularjs.org/api/ng/directive/ngRepeat)

### Definitions

* [Framework](https://en.wikipedia.org/wiki/Software_framework)
* [Hollywood Principle](https://en.wikipedia.org/wiki/Hollywood_principle)
* [Inversion of Control](https://en.wikipedia.org/wiki/Inversion_of_control)
* [Imperative vs Declarative Programming](https://netguru.co/blog/imperative-vs-declarative)
* [Imperative vs Declarative](http://latentflip.com/imperative-vs-declarative/)

### Blog Articles

* [Most Popular JavaScript Frameworks 2015](http://www.improgrammer.net/most-popular-javascript-frameworks-2015/)
* [JavaScript Frameworks: The Best 10 for Modern Web Apps](http://noeticforce.com/best-Javascript-frameworks-for-single-page-modern-web-applications)
* [A JS framework on every tableA JS framework on every table](http://www.allenpike.com/2015/javascript-framework-fatigue/) \(an interesting viewpoint on JavaScript frameworks\)
* [Choosing the right JavaScript framework for the job](https://www.lullabot.com/articles/choosing-the-right-javascript-framework-for-the-job)
* [Should You Use a JavaScript MVC Framework to Build Your Web Application?](https://www.codementor.io/javascript/tutorial/should-you-build-your-web-application-with-javascript-mvc-frameworks)
* [Comparison of 4 popular JavaScript MV\* frameworks \(part 1\)](http://www.developereconomics.com/feature-comparison-of-4-popular-js-mv-frameworks/)
* [AngularJS Critique](http://tutorials.jenkov.com/angularjs/critique.html) \(a critical view of AngularJS, take it with a grain of salt\)
* [Why you should not use AngularJS](https://medium.com/@mnemon1ck/why-you-should-not-use-angularjs-1df5ddf6fc99#.rkt7pbq0m) \(another viewpoint on Angular, take it with a rock of salt, grains are too tiny\)
* [Declarative vs. Imperative Programming for the Web](http://codenugget.co/2015/03/05/declarative-vs-imperative-programming-web.html)
* [Meteor vs Angular](http://blog.differential.com/meteor-vs-angular/?utm_medium=email&utm_source=other&utm_campaign=opencourse.discourse.web-frameworks%7Eopencourse.discourse.ycQnChn3EeWDtQoum3sFeQ.PfN0mIYyEeWOJwp8z3qGpQ%7EBqJDTIboEeWL6AoNmIctaQ)

# Models, Views and Controllers

## 13. **阅读: **Objectives and Outcomes

## 14. **视频: **The Model View Controller Framework

## 15. **视频: **Angular Modules and Controllers

## 16. **视频: **Exercise \(Video\): Angular Modules and Controllers

## 17. **阅读: **Exercise \(Instructions\): Angular Modules and Controllers

# Exercise \(Instructions\): Angular Modules and Controllers

### Objectives and Outcomes

In this exercise you will learn to use Angular modules and controllers to organize your Angular application and separate the data from the layout of the page. At the end of this exercise, you will be able to:

* Define an Angular module, and initialize the Angular app with the module
* Define a controller within your Angular app and use the controller within your application

### Creating Angular Module

* First, update the ng-app with a name for the module that will define the application as follows:

  ```
  <html lang="en" ng-app="confusionApp">
  ```


This means that we now need to define an Angular module named _confusionApp_. We will do this next.

* We will include the Angular code within the menu.html page for this exercise. It's better to separate out the code into separate code files. We will adopt this in the exercises later.
* First, go to the bottom of the page and add the following code just before the body closing tag, to create the Angular module:

  ```
  <script>
    var app = angular.module('confusionApp',[]);
  </script>
  ```

* Next we will add a controller to this app as follows:

  ```
  <script>
    var app = angular.module('confusionApp',[]);
    app.controller('menuController', function() {
    });
  </script>
  ```


* Then, we will shift the dishes JavaScript object array from the ng-init to the controller. Cut out the ng-init from the div completely, and add the following code to the Controller:

  ```
  var dishes=[
  {
    name:'Uthapizza',
    image: 'images/uthapizza.png',
    category: 'mains',
    label:'Hot',
    price:'4.99',
    description:'A unique combination of Indian Uthappam (pancake) and Italian pizza, topped with Cerignola olives, ripe vine cherry tomatoes, Vidalia onion, Guntur chillies and Buffalo Paneer.',
    comment: ''
  },
  {
    name:'Zucchipakoda',
    image: 'images/zucchipakoda.png',
    category: 'appetizer',
    label:'',
    price:'1.99',
    description:'Deep fried Zucchini coated with mildly spiced Chickpea flour batter accompanied with a sweet-tangy tamarind sauce',
    comment: ''
  },
  {
    name:'Vadonut',
    image: 'images/vadonut.png',
    category: 'appetizer',
    label:'New',
    price:'1.99',
    description:'A quintessential ConFusion experience, is it a vada or is it a donut?',
    comment: ''
  },
  {
    name:'ElaiCheese Cake',
    image: 'images/elaicheesecake.png',
    category: 'dessert',
    label:'',
    price:'2.99',
    description:'A delectable, semi-sweet New York Style Cheese Cake, with Graham cracker crust and spiced with Indian cardamoms',
    comment: ''
  }
  ];
  this.dishes = dishes;
  ```


### Attaching the Controller

* Modify the row class as follows to add the controller to the div:

  ```
  <div class="row row-content" ng-controller="menuController as menuCtrl">
  ```


This adds the menuController as the controller for this div, and also assigns an alias to the controller as menuCtrl.

* Next update, the list tag as follows:

  ```
  <li class="media" ng-repeat="dish in menuCtrl.dishes">
  ```


* The web page itself will show no change, except that the code is now factored out into a controller.

### Conclusions

In this exercise, you learnt about Angular module and controller and how we assign a controller to a div and make the data within the controller accessible within the div.

## 18. **练习测验: **Models, Views and Controllers

## 19. **阅读: **The Model View Controller Framework: Additional Resources

### Angular Resources

* [Angular Concepts](https://docs.angularjs.org/guide/concepts)
* [Angular Module](https://docs.angularjs.org/guide/module)
* [Angular Controllers](https://docs.angularjs.org/guide/controller)

### Additional Resources

* [Software design pattern](https://en.wikipedia.org/wiki/Software_design_pattern)
* [Model–view–controller](https://en.wikipedia.org/wiki/Model-view-controller)
* [Model-View-ViewModel](https://en.wikipedia.org/wiki/Model_View_ViewModel)
* [Model-View-Whatever](http://www.beyondjava.net/blog/model-view-whatever/)
* [Design Patterns: Elements of Reusable Object-Oriented Software](http://c2.com/cgi/wiki?DesignPatternsBook)
* [Web Application](https://en.wikipedia.org/wiki/Web_application)

# Angular Filters

## 20. **阅读: **Objectives and Outcomes

## 21. **视频: **Angular Filters

## 22. **视频: **Exercise \(Video\): Angular Filters

## 23. **阅读: **Exercise \(Instructions\): Angular Filters

### Objectives and Outcomes

This exercise is designed to illustrate to you how Angular filters can be used effectively in an application. In this exercise, you will create a menu that either presents the whole menu, or parts of the menu as selected by the user. At the completion of this exercise, you will be able to:

* Use Angular filters to filter items based on user's selection
* Use Bootstrap navigation tabs in conjunction with AngularJS
* Make use of the ng-class and ng-click Angular directives

### Deleting Comments from Menu Items

* Starting with the \_menu.html \_file from the previous exercise, you will first **delete** the following lines corresponding to the comments in the menu items from the page:

  ```
  <p>Comment: {{dish.comment}}</p>
  <p>Type your comment:
  <input type="text" ng-model="dish.comment"></p>
  ```


### Setting up Tabbed Navigation for the Menu

* We will now take the help of Bootstrap tabs to set up a tabbed navigation for the menu. We will construct four tabs to display all the menu items, appetizers, mains, and Desserts based on user's selection. Add the following code to the column div, just before the &lt;ul&gt; containing the menu items:

  ```
  <ul class="nav nav-tabs" role="tablist">
  <li role="presentation"> <a aria-controls="all menu" role="tab">The Menu</a></li>
  <li role="presentation"> <a aria-controls="appetizers" role="tab">Appetizers</a></li>
  <li role="presentation"> <a aria-controls="mains" role="tab">Mains</a></li>
  <li role="presentation"> <a aria-controls="desserts" role="tab">Desserts</a></li>
  </ul>
  ```


You will see the four tabs set up by the above navigation. However clicking on the tabs does not do anything, since we have not set up the logic to activate the tabs.

* Next, enclose the menu _&lt;ul&gt;_ inside a _&lt;div&gt;_ with class _tab-content_. Also appy the _tab-pane fade in active_ class to the ul as shown below:

  ```
  <div class="tab-content">
  <ul class="media-list tab-pane fade in active">
    . . .
  </ul>
  </div>
  ```


Keep the _&lt;li&gt;_ item in the _&lt;ul&gt;_ as is.

### Activating the Navigation Tabs

* We will now activate the tabs so that the user can select any of the four tabs. We need to do this by adding some functions to the menucontroller and then use the functions to activate the tabs when selected. First we add a variable named tab to the menucontroller code as follows:

  ```
  this.tab = 1;
  ```


Add this as the first statement in the menu controller. Note that the tabs are given indices 1 .. 4. The variable tab will keep track of the currently active tab. By default this will be assigned as the first tab. Obviously, the remaining tabs will be numbered 2 .. 4.

* Whenever the user clicks on a tab, we need to activate that tab. To do this, we take the help of the _ng-click_ Angular directive. This directive will be fired when the user clicks on the tab. To do this, we will add an ng-click directive to every &lt;a&gt; tag within the tabs as follows:

  ```
  <ul class="nav nav-tabs" role="tablist">
    <li role="presentation"> <a ng-click="menuCtrl.select(1) "aria-controls="all menu" role="tab">The Menu</a></li>
    <li role="presentation"> <a ng-click="menuCtrl.select(2) "aria-controls="appetizers" role="tab">Appetizers</a></li>
    <li role="presentation"> <a ng-click="menuCtrl.select(3) "aria-controls="mains" role="tab">Mains</a></li>
    <li role="presentation"> <a ng-click="menuCtrl.select(4) "aria-controls="desserts" role="tab">Desserts</a></li>
  </ul>
  ```


Note that the complete code is given above, just in case you wish to cut and paste the code. Note how the _ng-click\_directives are introduced using \_ng-click="menuCtrl.select\(i\)"._

* Upon clicking of the tab, the ng-click directive will cause the execution of the select\(\) function in the menucontroller. Next, we need to implement the select\(\) function. Add the following code to the menucontroller to implement the select\(\) function:

  ```
  this.select = function(setTab) {
    this.tab = setTab;
  }
  ```


This function will set the tab variable to the selected tab index.

* Next we take the help of the _ng-class_ directive in order to add the Bootstrap _active_ class to the selected tab. To do this modify the _&lt;ul&gt;_ for the tabs as follows, where you can clearly see the ng-class directive being used:

  ```
  <ul class="nav nav-tabs" role="tablist">
    <li role="presentation" ng-class="{active:menuCtrl.isSelected(1)}"> <a ng-click="menuCtrl.select(1) "aria-controls="all menu" role="tab">The Menu</a></li>
    <li role="presentation" ng-class="{active:menuCtrl.isSelected(2)}"> <a ng-click="menuCtrl.select(2) "aria-controls="appetizers" role="tab">Appetizers</a></li>
    <li role="presentation" ng-class="{active:menuCtrl.isSelected(3)}"> <a ng-click="menuCtrl.select(3) "aria-controls="mains" role="tab">Mains</a></li>
    <li role="presentation" ng-class="{active:menuCtrl.isSelected(4)}"> <a ng-click="menuCtrl.select(4) "aria-controls="desserts" role="tab">Desserts</a></li>
  </ul>
  ```


Note that for each of the _&lt;li&gt;_ elements, we introduced the _ng-class="{active:menuCtrl.isSelected\(i\)}"_ directive. This directive will apply the active class to that element, if the function on the right \(that specifies a condition\) evaluates to true.

* Next, we need to implement the isSelected\(\) function in the menucontroller. Add the following code to implement this function in the menucontroller:

  ```
  this.isSelected = function (checkTab) {
    return (this.tab === checkTab);
  }
  ```


This function will return true if the current tab is the same as the tab specified in the function parameter.

* Now the selection of the tabs, and activating the selected tab should work correctly. However no matter which tab is selected, you will still see the list of all menu items.

### Using Angular Filter

* Next we take the help of the Angular filter to select only those items from the menu corresponding to each tab. Note that each dish object already has a property named _category_. We can use this to filter our items.
* We will now set up the filters on the list items in the menu as follows:

  ```
  <li class="media" ng-repeat="dish in menuCtrl.dishes | filter:menuCtrl.filtText">
  ```


The above modification implies that the filter will use the variable filtText from the menucontroller to filter the items from the dishes array.

* Next we need to introduce the filtText variable in the menucontroller and have a way of setting it to the appropriate value when the various tabs are selected. To do this, add the following code to the menucontroller:

  ```
  this.filtText = '';
  ```


We are specifying that initially since the first tab is selected as default, the filtText should not filter out any item from the menu. Hence filtText is set to the empty string.

* Then, whenever a tab is selected, the filtText value should be updated to reflect the selected tab and the corresponding filter value to be applied. To do this, modify the select\(\) function as follows:

  ```
  this.select = function(setTab) {
    this.tab = setTab;

    if (setTab === 2) this.filtText = "appetizer";
    else if (setTab === 3) this.filtText = "mains";
    else if (setTab === 4) this.filtText = "dessert";
    else this.filtText = ""; 
  }
  ```

* Note that using the if statements, we are able to set the filtText to the appropriate value.

* Now the application should show the correctly filtered results from the menu items when the tabs are selected.


### Conclusions

In this exercise we explored the use of Angular filter to select specific items from a JavaScript array object and use them to construct the list of items in the menu. We also explored the use of the _ng-click_ and the _ng-class_ directives.

## 24. **练习测验: **Angular Filters

## 25. **阅读: **Angular Filters: Additional Resources

### Angular Documentation

* [List of Angular Built-in Filters](https://docs.angularjs.org/api/ng/filter)
* [Currency Filter](https://docs.angularjs.org/api/ng/filter/currency)
* [Date Filter](https://docs.angularjs.org/api/ng/filter/date)
* [Filter](https://docs.angularjs.org/api/ng/filter/filter)
* [OrderBy Filter](https://docs.angularjs.org/api/ng/filter/orderBy)

# Assignment 1

## 26. **视频: **Assignment 1 \(Video\): Requirements

## 27. **阅读: **Assignment 1: Additional Resources

### Other Related Resources

* [Bootstrap Media Object](http://getbootstrap.com/components/#media)
* [Bootstrap Blockquote](http://getbootstrap.com/css/#type-blockquotes)
* [Angular Date Filter](https://docs.angularjs.org/api/ng/filter/date)
* [Angular orderBy Filter](https://docs.angularjs.org/api/ng/filter/orderBy)

