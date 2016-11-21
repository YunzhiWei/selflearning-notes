# Web Tools: Grunt and Gulp

## 1. **阅读: **Objectives and Outcomes

## 2. **视频: **Web Tools: Task Runners

## 3. **视频: **Web Tools: Grunt

## 4. **视频: **Exercise \(Video\): Web Tools: Grunt

## 5. **阅读: **Exercise \(Instructions\): Web Tools: Grunt

### Objectives and Outcomes

In this exercise, you will learn to use Grunt, the task runner. You will install Grunt CLI and install Grunt packages using NPM. Thereafter you will configure a Grunt file with a set of tasks to build and serve your web project. At the end of this exercise, you will be able to:

* Install Grunt CLI and Grunt packages in your project
* Configure a Grunt file with a set of tasks to build a web project from a source, and serve the built project using a server.

### Installing Grunt

**Note**: You should already have [Node](http://nodejs.org/) and NPM installed on your computer before you proceed further. Also, those using OSX or Linux should use **sudo** while installing **global** packages in node \(when you use the **-g** flag\).

* At the command prompt, type the following to install Grunt command-line interface \(CLI\):

  ```
  npm install -g grunt-cli
  ```


This will install the Grunt CLI globally so that you can use them in all projects.

* Next, create the _package.json_ file in the _conFusion_ folder with the following content:

  ```
  {
    "name": "conFusion",
    "private": true,
    "devDependencies": {},
    "engines": {
      "node": ">=0.10.0" 
    }
  }
  ```


* Next install Grunt to use within your project. To do this, go to the _conFusion_ folder and type the following at the prompt:

  ```
  npm install grunt --save-dev
  ```


This will install local per-project Grunt to use within your project.

### Creating a Grunt File

* Next you need to create a Grunt file containing the configuration for all the tasks to be run when you use Grunt. To do this, create a file named _Gruntfile.js_ in the _conFusion_ folder.
* Next, add the following code to Gruntfile.js to set up the file to configure Grunt tasks:

  ```
  'use strict';
  module.exports = function (grunt) {
    // Define the configuration for all the tasks 
    grunt.initConfig({
    });
  };
  ```


This sets up the Grunt module ready for including the grunt tasks inside the function above.

### Configuring the Project

* Next, we need to configure the menu.html file for this exercise. Open the menu.html file and update the CSS import lines in the head of the page as follows:

  ```
  <!-- Bootstrap -->
  <!-- build:css styles/main.css --> 
    <link href="../bower_components/bootstrap/dist/css/bootstrap.min.css" rel="stylesheet"> 
    <link href="../bower_components/bootstrap/dist/css/bootstrap-theme.min.css" rel="stylesheet"> 
    <link href="../bower_components/font-awesome/css/font-awesome.min.css" rel="stylesheet"> 
    <link href="styles/bootstrap-social.css" rel="stylesheet"> <link href="styles/mystyles.css" rel="stylesheet">
  <!-- endbuild -->
  ```


We are surrounding the links with some specially formatted comment lines, the purpose of which will become clear in a later step.

* Similarly, replace all the script at the bottom of the page with the following code. We will be moving all the Angular script to a separate _app.js_ file in the next step.

  ```
  <!-- build:js scripts/main.js -->
    <script src="../bower_components/angular/angular.min.js"></script>
    <script src="scripts/app.js"></script>
  <!-- endbuild -->
  ```


* Next, in the app\/scripts folder, create a file named _app.js_ and include the following code in this file:

  ```
  'use strict';

  angular.module('confusionApp', []).controller('menuController', function() {
    this.tab = 1;
    this.filtText = '';

    var dishes = [
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
        category: 'dessert', label:'',
        price:'2.99',
        description:'A delectable, semi-sweet New York Style Cheese Cake, with Graham cracker crust and spiced with Indian cardamoms',
        comment: ''
      }
    ];

    this.dishes = dishes;
    this.select = function(setTab) {
      this.tab = setTab;
      if (setTab === 2) {
        this.filtText = "appetizer";
      }
      else if (setTab === 3) {
        this.filtText = "mains";
      }
      else if (setTab === 4) {
        this.filtText = "dessert";
      }
      else {
        this.filtText = "";
      }
    };
    this.isSelected = function (checkTab) {
      return (this.tab === checkTab);
    };
  });
  ```


With this change we have moved all the JavaScript code into a separate file. This is the normal way that you configure Angular projects.

### The JSHint Task

* Next, we are going to set up our first Grunt task. The JSHint task validates our JavaScript code and points out errors and gives warnings about minor violations. To do this, you need to include some Grunt modules that help us with the tasks. Install the following modules by typing the following at the prompt:

  ```
  npm install grunt-contrib-jshint --save-dev
  npm install jshint-stylish --save-dev
  npm install time-grunt --save-dev
  npm install jit-grunt --save-dev
  ```


The first one installs the Grunt module for JSHint, and the second one adds further to print out the messages from JSHint in a better format. The time-grunt module generates time statistics about how much time each task consumes, and jit-grunt enables us to include the necessary downloaded Grunt modules when needed for the tasks.

* Now, configure the JSHint task in the Gruntfile as follows, by including the code inside the function in _Gruntfile.js_:

```
// Time how long tasks take. Can help when optimizing build times
require('time-grunt')(grunt);

// Automatically load required Grunt tasks
require('jit-grunt')(grunt);

// Define the configuration for all the tasks
grunt.initConfig({
  pkg: grunt.file.readJSON('package.json'),

  // Make sure code styles are up to par and there are no obvious mistakes
  jshint: {
    options: {
      jshintrc: '.jshintrc',
      reporter: require('jshint-stylish') 
    },
    all: {
      src: [
        'Gruntfile.js',
        'app/scripts/{,*/}*.js'
      ]
    }
  }
});
grunt.registerTask('build', [
  'jshint'
]);
grunt.registerTask('default',['build']);
```

In the above, we have set up time-grunt and jit-grunt to time the tasks, and load Grunt modules when needed. The JSHint task is set to examine all the JavaScript files in the app\/scripts folder, and the Gruntfile.js and generate any reports of JS errors or warnings. We have set up a Grunt task named build, that runs the jshint task and the build task is also registered as the default task.

* Next, create a file named _.jshintrc_ \(Don't forget the . in front of jshintrc\) in the conFusion folder, and include the following in the file:

```
{
  "bitwise": true,
  "browser": true,
  "curly": true,
  "eqeqeq": true,
  "esnext": true,
  "latedef": true,
  "noarg": true,
  "node": true,
  "strict": true,
  "undef": true,
  "unused": true,
  "globals": {
    "angular": false
  }
}
```

* Now you can run the grunt task by typing the following at the prompt:

```
grunt
```

### Copying the Files and Cleaning Up the Dist Folder

* Next you will install the Grunt modules to copy over files to a distribution folder named dist, and clean up the dist folder when needed. To do this, install the following Grunt modules:

```
npm install grunt-contrib-copy --save-dev
npm install grunt-contrib-clean --save-dev
```

You will now add the code to perform the copying of files to the dist folder, and cleaning up the dist folder. To do this, add the following code to _Gruntfile.js_. This should be added right after the configuration of the JSHint task.:

```
},

copy: {
  dist: {
    cwd: 'app',
    src: [ '**','!styles/**/*.css','!scripts/**/*.js' ],
    dest: 'dist',
    expand: true
  },
  fonts: {
    files: [
      {
        //for bootstrap fonts
        expand: true,
        dot: true,
        cwd: 'bower_components/bootstrap/dist',
        src: ['fonts/*.*'],
        dest: 'dist' 
      },
      {
        //for font-awesome
        expand: true,
        dot: true,
        cwd: 'bower_components/font-awesome',
        src: ['fonts/*.*'],
        dest: 'dist'
      }
    ] 
  }
},
clean: {
  build: {
    src: [ 'dist/']
  }
}
```

* Then, update the Grunt build task in the file as follows:

```
grunt.registerTask('build', [
  'clean',
  'jshint',
  'copy'
]);
```

You can run Grunt and see what it generates.

### Preparing the Distribution Folder and Files

* We are now going to use the Grunt _usemin_ module together with _concat_, _cssmin_, _uglify_ and _filerev_ to prepare the distribution folder. To do this, install the following Grunt modules:

```
npm install grunt-contrib-concat --save-dev 
npm install grunt-contrib-cssmin --save-dev 
npm install grunt-contrib-uglify --save-dev 
npm install grunt-filerev --save-dev 
npm install grunt-usemin --save-dev
```

* Next, update the task configuration within the Gruntfile.js with the following additional code to introduce the new tasks:

```
  },
  useminPrepare: {
    html: 'app/menu.htm'},

useminPrepare: {
  html: 'app/menu.html',
  options: {
    dest: 'dist'
  }
},

// Concat
concat: {
  options: {
    separator: ';' 
  }, 
  // dist configuration is provided by useminPrepare
  dist: {}
},

// Uglifyuglify: {
  // dist configuration is provided by useminPrepare
  dist: {}
},

cssmin: {
  dist: {}
},

// Filerev
filerev: {
  options: {
    encoding: 'utf8',
    algorithm: 'md5',
    length: 20 
  },
  release: {
    // filerev:release hashes(md5) all assets (images, js and css )
    // in dist directory
    files: [{
      src: [
        'dist/scripts/*.js',
        'dist/styles/*.css',
      ]
    }]
  }
},

// Usemin
// Replaces all assets with their revved version in html and css files.
// options.assetDirs contains the directories for finding the assets
// according to their relative path
susemin: {
  html: ['dist/*.html'],
  css: ['dist/styles/*.css'],
  options: { 
    assetsDirs: ['dist', 'dist/styles']
  }
},
```

* Next, update the jit-grunt configuration as follows, to inform it that useminPrepare task depends on the usemin package:

```
require('jit-grunt')(grunt, {
  useminPrepare: 'grunt-usemin'
});
```

* Next, update the Grunt build task as follows:

```
runt.registerTask('build', [
  'clean',
  'jshint',
  'useminPrepare',
  'concat',
  'cssmin',
  'uglify',
  'copy',
  'filerev',
  'usemin'
]);
```

* Now if you run Grunt, it will create a dist folder with the files structured correctly to be distributed to a server to host your website.

### Watch, Connect and Serve Tasks

* The final step is to use the Grunt modules watch, connect and watch, to spin up a web server and keep a watch on the files and automatically reload the browser when any of the watched files are updated. To do this, install the following grunt modules:

```
npm install grunt-contrib-watch --save-dev
npm install grunt-contrib-connect --save-dev
```

* After this, we will configure the connect and watch tasks by adding the following code to the Grunt file:

```
watch: {
  copy: {
    files: [ 'app/**', '!app/**/*.css', '!app/**/*.js'],
    tasks: [ 'build' ]
  },
  scripts: {
    files: ['app/scripts/app.js'],
    tasks:[ 'build']
  },
  styles: {
    files: ['app/styles/mystyles.css'],
    tasks:['build']
  },
  livereload: {
    options: {
      livereload: '<%= connect.options.livereload %>'
    },
    files: [
      'app/{,*/}*.html',
      '.tmp/styles/{,*/}*.css',
      'app/images/{,*/}*.{png,jpg,jpeg,gif,webp,svg}'
    ]
  }
},
connect: {
  options: {
    port: 9000,
    // Change this to '0.0.0.0' to access the server from outside.
    hostname: 'localhost',
    livereload: 35729
  },
  dist: {
    options: {
      open: true,
      base:{
        path: 'dist',
        options: {
          index: 'menu.html',
          maxAge: 300000
        }
      }
    }
  }
},
```

* Then add the following task to the Grunt file:

  ```
  grunt.registerTask('serve',['build','connect:dist','watch']);
  ```

* Now if you type the following at the command prompt, it will build the project, and open the web page in your default browser. It will also keep a watch on the files in the app folder, and if you update any of them, it will rebuild the project and load the updated page into the browser \(livereload\)

  ```
  grunt serve
  ```


### Conclusions

In this exercise you have learnt how to configure a Grunt file to perform several tasks. You were able to build a distribution folder and start a server with livereload to serve the web page.

## 6. **视频: **Web Tools: Gulp

## 7. **视频: **Exercise \(Video\): Web Tools: Gulp

## 8. **阅读: **Exercise \(Instructions\): Web Tools: Gulp

### Objectives and Outcomes

In this exercise, you will learn to use Gulp, the task runner. You will install Gulp CLI and install Gulp plugins using NPM. Thereafter you will configure a Gulp file with a set of tasks to build and serve your web project. At the end of this exercise, you will be able to:

* Install Gulp CLI and Gulp plugins in your project
* Configure a Gulp file with a set of tasks to build a web project from a source, and serve the built project using a server.

### Clean node\_modules Folder

* Go to the _node\_modules_ folder in _conFusion_, and delete all the folders\/files there. We will not be using the Grunt modules existing there for this exercise.

### Initialize package.json File

* Next, update the _package.json_ file in the _conFusion_ folder with the following content:

  ```
  {
    "name": "conFusion",
    "private": true,
    "devDependencies": {
    },
    "engines": {
      "node": ">=0.10.0"
    }
  }
  ```


### Installing Gulp

**Note**: You should already have [Node](http://nodejs.org/) and NPM installed on your computer before you proceed further. Also, those using OSX or Linux should use **sudo** while installing **global** packages in node \(when you use the **-g** flag\).

* At the command prompt, type the following to install Gulp command-line interface \(CLI\) globally:

  ```
  npm install -g gulp
  ```


This will install the Gulp globally so that you can use it in all projects.

* Next install Gulp to use within your project. To do this, go to the _conFusion_ folder and type the following at the prompt:

  ```
  npm install gulp --save-dev
  ```


This will install local per-project Gulp to use within your project.

### Install Gulp Plugins

* Install all the Gulp plugins that you will need for this exercise. To do this, type the following at the command prompt:

  ```
  npm install jshint gulp-jshint jshint-stylish gulp-imagemin gulp-concat gulp-uglify gulp-minify-css gulp-usemin gulp-cache gulp-changed gulp-rev gulp-rename gulp-notify browser-sync del --save-dev
  ```


### Creating a Gulp File

* Next you need to create a Gulp file containing the tasks to be run when you use Gulp. To do this, create a file named _gulpfile.js_ in the _conFusion_ folder.

### Loading Gulp Plugins

* Load in all the Gulp plugins by including the following code in the Gulp file:

  ```
  var gulp = require('gulp'),
    minifycss = require('gulp-minify-css'),
    jshint = require('gulp-jshint'),
    stylish = require('jshint-stylish'),
    uglify = require('gulp-uglify'),
    usemin = require('gulp-usemin'),
    imagemin = require('gulp-imagemin'),
    rename = require('gulp-rename'),
    concat = require('gulp-concat'),
    notify = require('gulp-notify'),
    cache = require('gulp-cache'),
    changed = require('gulp-changed'),
    rev = require('gulp-rev'),
    browserSync = require('browser-sync'),
    del = require('del');
  ```


### Adding Gulp Tasks

* Next, we will add the code for the JSHint task, the Clean task and the default task as follows:

  ```
  gulp.task('jshint', function() {
    return gulp.src('app/scripts/**/*.js')
    .pipe(jshint())
    .pipe(jshint.reporter(stylish));
  });

  // Clean
  gulp.task('clean', function() {
    return del(['dist']);
  });

  // Default task
  gulp.task('default', ['clean'], function() {
    gulp.start('usemin', 'imagemin','copyfonts');
  });
  ```

* Next, paste in the code for the usemin, imagemin and copyfonts tasks:

  ```
  gulp.task('usemin',['jshint'], function () {
    return gulp.src('./app/menu.html')
    .pipe(usemin({
      css:[minifycss(),rev()],
      js: [uglify(),rev()] 
    }))
    .pipe(gulp.dest('dist/'));
  });

  // Images
  gulp.task('imagemin', function() {
    return del(['dist/images']), gulp.src('app/images/**/*')
      .pipe(cache(imagemin({ optimizationLevel: 3, progressive: true, interlaced: true })))
      .pipe(gulp.dest('dist/images'))
      .pipe(notify({ message: 'Images task complete' }));
  });

  gulp.task('copyfonts', ['clean'], function() {
    gulp.src('./bower_components/font-awesome/fonts/**/*.{ttf,woff,eof,svg}*')
      .pipe(gulp.dest('./dist/fonts'));
    gulp.src('./bower_components/bootstrap/dist/fonts/**/*.{ttf,woff,eof,svg}*')
      .pipe(gulp.dest('./dist/fonts'));});
  ```


* Finally, we add the code for the watch and browserSync tasks:

  ```
  // Watch
  gulp.task('watch', ['browser-sync'], function() {
    // Watch .js files
    gulp.watch('{app/scripts/**/*.js,app/styles/**/*.css,app/**/*.html}', ['usemin']);
    // Watch image files
    gulp.watch('app/images/**/*', ['imagemin']);
  });
  gulp.task('browser-sync', ['default'], function () {
    var files = [
      'app/**/*.html',
      'app/styles/**/*.css',
      'app/images/**/*.png',
      'app/scripts/**/*.js',
      'dist/**/*'
    ];
    browserSync.init(files, {
      server: {
        baseDir: "dist",
        index: "menu.html"
      }
    });
    // Watch any files in dist/, reload on change
    gulp.watch(['dist/**']).on('change', browserSync.reload);
  });
  ```


* Save the Gulp file

### Running the Gulp Tasks

* At the command prompt, if you type _gulp_ it will run the default task:

```
gulp
```

### Using BrowserSync and Watch

* We configured the BrowserSync and the Watch tasks in the Gulp file. To use them, type the following at the command prompt:

```
gulp watch
```

You may need to reload the page in the browser.

* You can edit the _menu.html_ file in the app folder and see the watch task and BrowserSync action in reloading the updated page.

### Conclusions

In this exercise, you learnt to use Gulp, install Gulp plugins, configure the gulpfile.js and then use Gulp to automate the web development tasks.

## 9. **练习测验: **Task Runners

## 10. **阅读: **Web Tools: Grunt and Gulp: Additional Resources

### Grunt Resources

* [Grunt](http://gruntjs.com/)
* [Writing an Awesome Build Script with Grunt](http://www.sitepoint.com/writing-awesome-build-script-grunt/)
* [Clean Grunt](http://anders.janmyr.com/2014/01/clean-grunt.html)
* [File Globbing](http://gruntjs.com/configuring-tasks#globbing-patterns)
* [grunt-contrib-jshint](https://github.com/gruntjs/grunt-contrib-jshint)
* [jshint-stylish](https://github.com/sindresorhus/jshint-stylish)
* [grunt-contrib-copy](https://github.com/gruntjs/grunt-contrib-copy)
* [grunt-contrib-clean](https://github.com/gruntjs/grunt-contrib-clean)
* [grunt-usemin](https://github.com/yeoman/grunt-usemin)
* [grunt-contrib-concat](https://github.com/gruntjs/grunt-contrib-concat)
* [grunt-contrib-cssmin](https://github.com/gruntjs/grunt-contrib-cssmin)
* [grunt-contrib-uglify](https://github.com/gruntjs/grunt-contrib-uglify)
* [grunt-filerev](https://github.com/yeoman/grunt-filerev)

### Gulp Resources

* [Gulp](http://gulpjs.com/)
* [An Introduction to Gulp.js](http://www.sitepoint.com/introduction-gulp-js/)
* [Getting started with gulp](https://markgoodyear.com/2014/01/getting-started-with-gulp/)
* [Building with Gulp](http://www.smashingmagazine.com/2014/06/building-with-gulp/)

### Tasks

* [Minification](https://en.wikipedia.org/wiki/Minification_(programming)\)
* [UglifyJS](http://lisperator.net/uglifyjs/)
* [JSHint](http://jshint.com/)

### General Resources

* [Node, Grunt, Bower and Yeoman - A Modern web dev's Toolkit](http://juristr.com/blog/2014/08/node-grunt-yeoman-bower/)
* [The Advantages of Using Task Runners](https://www.dbswebsite.com/blog/2015/02/24/the-advantages-of-using-task-runners/)
* [Gulp vs Grunt. Why one? Why the Other?](https://medium.com/@preslavrachev/gulp-vs-grunt-why-one-why-the-other-f5d3b398edc4)
* [Why we should stop using Grunt & Gulp](http://blog.keithcirkel.co.uk/why-we-should-stop-using-grunt/)

# Angular Scope

## 11. **阅读: **Objectives and Outcomes

## 12. **视频: **Angular Scope

* **ng-controller** create a new scope

* **ng-include** create a new scope

## 13. **视频: **Exercise \(Video\): Angular Scope

## 14. **阅读: **Exercise \(Instructions\): Angular Scope

### Objectives and Outcomes

In this exercise, you will explore Angular scope and the use of scope as a glue between the view and controller. You will also learn about the _ngShow_ directive. At the end of this exercise, you will be able to:

* Understand the use of Angular Scope.
* Use scope to connect the view and the controller.
* Make use of the ngShow directive.

### Modifying the Gulp File

* Since Angular involves writing a lot of JavaScript, once we introduce the $scope, we need to make sure that when the uglify task runs, it does not end up mangling the $scope. Otherwise the JavaScript code will not work. Fortunately, we have an gulp plugin named gulp-ng-annotate, which ensures the mangling does not cause any problems. We now need to add this plugin and update the gulpfile.js to include this plugin.
* First install the gulp-ng-annotate plugin:

  ```
  npm install gulp-ng-annotate --save-dev
  ```


* Then require this in gulpfile.js.

  ```
  var ngannotate = require('gulp-ng-annotate');
  ```


* Next, add the ngannotate\(\) to the usemin task for the JavaScript part, by updating the usemin task as follows:

  ```
  gulp.task('usemin',['jshint'], function () {
  return gulp.src('./app/menu.html')
  .pipe(usemin({
    css:[minifycss(),rev()],
    js: [ngannotate(),uglify(),rev()]
  }))
  .pipe(gulp.dest('dist/'));
  });
  ```


### Using Angular $Scope

* Open the _app.js_ file. Update the Angular controller's name to MenuController, changing the small letter "m" to capital letter "M", to conform to the accepted Angular convention of naming the controllers starting with a Capital letter.
* Next, update the controller to use the scope as follows:

  ```
  .controller('MenuController', ['$scope', function($scope) {
  . . .
  }]);
  ```


* Next, you need to update all references to "_this._" with "_$scope._" in the JavaScript code in the controller.
* **Remove** the following statement from the controller code:

  ```
  this.dishes = dishes;
  ```


* In its place, substitute the following statement:

  ```
  $scope.dishes = dishes;
  ```


* Save the _app.js_ file, and then open _menu.html_ file. In the HTML code, we no longer need to use the _menuCtrl_ alias for the _MenuController_. The JavaScript variables and functions in the _MenuController_ code can be accessed within HTML by directly using their names without the _menuCtrl._ prefix. So, remove the _menuCtrl._ prefix from all the HTML code. Also remove the _menuCtrl_ alias from the ng-controller directive. Also, update the _menuController_ to _MenuController_ in the directive.

### Using the _ngShow_ Directive

* In the _menu.html_ page, right before the &lt;ul&gt; for the tabs, introduce a button using the following code:

  ```
  <button ng-click="toggleDetails()" class="btn btn-xs btn-primary pull-right" type="button">
  {{showDetails ? 'Hide Details':'Show Details'}}
  </button>
  ```


* Update the &lt;p&gt; containing the dish description as follows:

  ```
  <p ng-show="showDetails">{{dish.description}}</p>
  ```


* Save the _menu.html_ page, and then switch to _app.js_ file to introduce the JavaScript code. Add the following code to the _MenuController_:

  ```
  $scope.showDetails = false;
  . . .
  $scope.toggleDetails = function() {
  $scope.showDetails = !$scope.showDetails;
  };
  ```


* Save_ app.js_ and then check the behavior of the web page.

### Conclusions

In this exercise, you learnt more about the use of Angular $Scope. You also learnt about the _ngShow_ directive.

## 15. **练习测验: **Angular $scope

## 16. **阅读: **Angular Scope: Additional Resources

### Angular Resources

* [Angular Scope](https://docs.angularjs.org/guide/scope)
* [Scope](https://docs.angularjs.org/api/ng/type/$rootScope.Scope)
* [$rootScope](https://docs.angularjs.org/api/ng/service/$rootScope)
* [ngShow](https://docs.angularjs.org/api/ng/directive/ngShow) and [ngHide](https://docs.angularjs.org/api/ng/directive/ngHide)

### Other Interesting Articles

* [AngularJS Scopes: An Introduction](http://blog.carbonfive.com/2014/02/11/angularjs-scopes-an-introduction/)

# Angular Forms and Form Validation

## 17. **阅读: **Objectives and Outcomes

## 18. **视频: **Angular Forms and Form Validation

## 19. **视频: **Exercise \(Video\): Angular Forms and Form Validation

## 20. **阅读: **Exercise \(Instructions\): Angular Forms and Form Validation

### Objectives and Outcomes

In this exercise, you will learn more about Angular support for forms and form validation. You will also learn to use JavaScript to perform form validation. At the end of this exercise, you will be able to:

* Use Angular support for HTML forms
* Establish two-way data binding between form fields and JavaScript variables and object properties.
* Use Angular's support for form validation
* Use JavaScript to perform form validation in Angular.

### Setting up the Exercise

* Download contactus.html given above and put it in your _conFusion\/app_ folder. Open the page for editing.

### Adding Angular Forms Support

* Update the &lt;html&gt; tag to turn the page into an Angular app as follows:

  ```
  <html lang="en" ng-app="confusionApp">
  ```


* Next, go to the body of the page, update the container div as follows:

  ```
  <div class="container" ng-controller="ContactController">
  ```


* Next, go to the form, and update the enclosing div as follows:

  ```
  <div class="col-xs-12 col-sm-9" ng-controller="FeedbackController">
  ```


### Adding Controllers

* Open _app.js_ and at the bottom of this page, add the two new controllers that we used in the page by inserting the following code:

  ```
  .controller('ContactController', ['$scope', function($scope) {
  $scope.feedback = {mychannel:"", firstName:"", lastName:"", agree:false, email:"" };
  }])
  .controller('FeedbackController', ['$scope', function($scope) {
  }]);
  ```


### Establishing Two-Way Data Binding

* Update the firstName input field as follows:

  ```
  <div class="form-group">
  <label for="firstname" class="col-sm-2 control-label">First Name</label>
  <div class="col-sm-10">
    <input type="text" class="form-control" id="firstname" name="firstname" placeholder="Enter First Name" ng-model="feedback.firstName" required>
  </div>
  </div>
  ```


* Update the lastName input field as follows:

  ```
  <div class="form-group">
  <label for="lastname" class="col-sm-2 control-label">Last Name</label>
  <div class="col-sm-10">
    <input type="text" class="form-control" id="lastname" name="lastname" placeholder="Enter Last Name" ng-model="feedback.lastName" required>
  </div>
  </div>
  ```


* Update the telephone number fields as follows:

  ```
  <div class="form-group">
  <label for="telnum" class="col-sm-2 control-label">Contact Tel.</label>
  <div class="col-xs-5 col-sm-4 col-md-3">
    <div class="input-group">
      <div class="input-group-addon">(</div>
      <input type="tel" class="form-control" placeholder="Area code" ng-model="feedback.tel.areaCode">
      <div class="input-group-addon">)</div>
    </div>
  </div>
  <div class="col-xs-7 col-sm-6 col-md-7">
    <input type="tel" class="form-control" id="telnum" name="telnum" placeholder="Tel. number" ng-model="feedback.tel.number">
  </div>
  </div>
  ```


* Update the Email field as follows:

  ```
  <div class="form-group">
  <label for="emailid" class="col-sm-2 control-label">Email</label>
  <div class="col-sm-10">
    <input type="email" class="form-control" id="emailid" name="emailid" placeholder="Email" ng-model="feedback.email" required>
  </div>
  </div>
  ```


* Update the check box as follows:

  ```
  <div class="checkbox col-sm-5 col-sm-offset-2">
  <label class="checkbox-inline">
    <input type="checkbox" ng-model="feedback.agree">
    <strong>May we contact you?</strong>
  </label>
  </div>
  ```


* Update the textarea as follows:

  ```
  <div class="form-group">
  <label for="feedback" class="col-sm-2 control-label">Your Feedback</label>
  <div class="col-sm-10">
    <textarea class="form-control" rows="12" ng-model="feedback.comments"></textarea>
  </div>
  </div>
  ```


* Update the small column to the right of the feedback form as follows:

  ```
  <div class="col-xs-12 col-sm-3">
  <h3>Your Current Feedback:</h3>
  <p>{{feedback.firstName}} {{feedback.lastName | uppercase }}</p>
  <p>Contact Tel.: ({{feedback.tel.areaCode}}) {{feedback.tel.number}}</p>
  <p>Contact Email: {{feedback.email}}</p>
  <p ng-show="feedback.agree">Contact by: {{feedback.mychannel}}</p>
  <p>Comments: {{feedback.comments}}</p>
  </div>
  ```


### Angular Form Validation

* Update the &lt;form&gt; tag as follows:

  ```
  <form class="form-horizontal" name="feedbackForm" ng-submit="sendFeedback()" novalidate>
  ```


* Next, update the firstName form group as follows:

  ```
  <div class="form-group" ng-class="{ 'has-error' : feedbackForm.firstname.$error.required && !feedbackForm.firstname.$pristine }">
  . . .
  <span ng-show="feedbackForm.firstname.$error.required && !feedbackForm.firstname.$pristine" class="help-block">Your First name is required.</span>
  </div>
  </div>
  ```


* Update the lastname form group as follows:

  ```
  <div class="form-group" ng-class="{ 'has-error' : feedbackForm.lastname.$error.required && !feedbackForm.lastname.$pristine }">
  . . .
  <span ng-show="feedbackForm.lastname.$error.required && !feedbackForm.lastname.$pristine" class="help-block">Your Last name is required.</span>
  </div>
  </div>
  ```


* Then, update the emailid field as follows:

  ```
  <div class="form-group" ng-class="{ 'has-error has-feedback' : feedbackForm.emailid.$invalid && !feedbackForm.emailid.$pristine }">
  . . .
    <span ng-show="feedbackForm.emailid.$invalid && !feedbackForm.emailid.$pristine" class="glyphicon glyphicon-remove form-control-feedback" aria-hidden="true"></span>
    <span ng-show="(feedbackForm.emailid.$invalid || feedbackForm.emailid.$error.required) && !feedbackForm.emailid.$pristine" class="help-block">Enter a valid email address.</span>
  </div>
  </div>
  ```


* Update the checkbox and select form group as follows:

  ```
  <div class="form-group" ng-class="{ 'has-error' : invalidChannelSelection }">
  <div class="checkbox col-sm-5 col-sm-offset-2">
    <label class="checkbox-inline">
      <input type="checkbox" ng-model="feedback.agree">
      <strong>May we contact you?</strong>
    </label>
  </div>
  <div class="col-sm-3 col-sm-offset-1" ng-show="feedback.agree">
    <select class="form-control" ng-model="feedback.mychannel" ng-options="channel.value as channel.label for channel in channels">
      <option value="">Tel. or Email?</option>
    </select>
    <span ng-show="invalidChannelSelection" class="help-block">Select an option.</span>
  </div>
  </div>
  ```


* Update the button in the form as follows:

  ```
  <button type="submit" class="btn btn-primary" ng-disabled="feedbackForm.$invalid">Send Feedback</button>
  ```


* Save the_ contactus.html_ file, and then open the _app.js_ file. Update the controller code as follows:

  ```
  .controller('ContactController', ['$scope', function($scope) {
  $scope.feedback = {mychannel:"", firstName:"", lastName:"", agree:false, email:"" };
  var channels = [{value:"tel", label:"Tel."}, {value:"Email",label:"Email"}];
  $scope.channels = channels;
  $scope.invalidChannelSelection = false;
  }])
  .controller('FeedbackController', ['$scope', function($scope) {
  $scope.sendFeedback = function() {
    console.log($scope.feedback);
    if ($scope.feedback.agree && ($scope.feedback.mychannel == "")&& !$scope.feedback.mychannel) {
      $scope.invalidChannelSelection = true;
      console.log('incorrect');
    }
    else {
      $scope.invalidChannelSelection = false;
      $scope.feedback = {mychannel:"", firstName:"", lastName:"", agree:false, email:"" };
      $scope.feedback.mychannel="";
      $scope.feedbackForm.$setPristine();
      console.log($scope.feedback);
    }
  };
  }]);
  ```


* Save the file and then go and see the behavior of the web page.

### Conclusions

In this exercise, you learnt about Angular support for forms and form validation. You also learnt about doing form validation in the controller code using JavaScript.

## 21. **练习测验: **Angular Forms and Form Validation

## 22. **阅读: **Angular Forms and Form Validation: Additional Resources

### Angular Resources

* [Angular Forms](https://docs.angularjs.org/guide/forms)
* [Angular Form Directive](https://docs.angularjs.org/api/ng/directive/form)
* [Angular Select](https://docs.angularjs.org/api/ng/directive/select)

### Bootstrap

. [Bootstrap form validation states](http://getbootstrap.com/css/#forms-control-validation)

### Other Resources

* [AngularJS Forms](http://tutorials.jenkov.com/angularjs/forms.html)
* [AngularJS Form Validation](https://scotch.io/tutorials/angularjs-form-validation)
* [AngularJS Form Validation with ngMessages](https://scotch.io/tutorials/angularjs-form-validation-with-ngmessages)
* [Bootstrap Form Validation Done Right in AngularJS](http://blog.yodersolutions.com/bootstrap-form-validation-done-right-in-angularjs/)

# Assignment 2

## 23. **视频: **Assignment 2 \(Video\): Requirements

## 24. **阅读: **Assignment 2: Additional Resources

### Bootstrap Resources

* [Radio](http://getbootstrap.com/css/#checkboxes-and-radios)

### JavaScript Resources

* [JavaScript Array push\(\) method](http://www.w3schools.com/jsref/jsref_push.asp)
* [JavaScript Date](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_Objects/Date)

