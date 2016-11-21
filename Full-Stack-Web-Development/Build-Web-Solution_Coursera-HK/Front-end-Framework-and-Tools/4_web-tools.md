# 4. Web Tools

## 4.1 Bootstrap and JQuery

### Bootstrap Resources

* [Bootstrap Carousel Methods](http://getbootstrap.com/javascript/#carousel-methods)

### JQuery

* [JQuery](http://jquery.com/)
* [W3Schools JQuery](http://www.w3schools.com/jquery/default.asp)

### Exercise \(Instructions\): Bootstrap and JQuery

### Objectives and Outcomes

In this exercise we learn about using Bootstrap's JS component methods together with JQuery and JavaScript to write JavaScript code to control the JS component. We will use the Carousel as an example of a component that can be controlled. At the end of this exercise you will be able to:

* Use Bootstrap's JS component methods together with JQuery and Javascript
* Use JS code to control the Bootstrap JS component

#### Adding the Carousel Control Buttons

* We will introduce two new buttons into the carousel component that we already included in the index.html page. To add the two buttons to the carousel, add the following code to the end of the carousel:

```
<div class="btn-group" id="carouselButtons">
  <button class="btn btn-danger btn-xs" id="carousel-pause">
    <span class="glyphicon glyphicon-pause" aria-hidden="true"></span>
  </button>
  <button class="btn btn-danger btn-xs" id="carousel-play">
    <span class="glyphicon glyphicon-play" aria-hidden="true"></span>
  </button>
</div>
```

We are adding the two buttons inside a button group with the ID carouselButtons. The two buttons contain the pause and play glyphicons to indicate their corresponding actions.

#### Adding CSS Class for the Buttons

* Next, we add the following CSS class to mystyles.css file to position the buttons at the bottom-right corner of the carousel:

```
#carouselButtons {
  right:0px;
  position: absolute;
  bottom: 0px;
}
```

#### Adding JavaScript Code

* Finally we add the following JavaScript code to activate the buttons:

```
<script>
  $(document).ready(function(){
    $("#mycarousel").carousel( { interval: 2000 } );
    $("#carousel-pause").click(function(){
      $("#mycarousel").carousel('pause');
    });
    $("#carousel-play").click(function(){
      $("#mycarousel").carousel('cycle');
    });
  });
</script>
```

#### Conclusions

In this exercise we learnt about Bootstrap's JS component methods and how they can be used together with JQuery and JavaScript to control the behavior of a Bootstrap JS component.

## 4.2 Node.js and Node Package Manager

### Node and NPM

* [Nodejs.org](https://nodejs.org/)
* [Npmjs.com](https://www.npmjs.com/)
* [Node API Documentation](https://nodejs.org/api/)
* [NPM Documentation](https://docs.npmjs.com/)

### Exercise \(Instructions\): Setting up Node.js and NPM

#### Objectives and Outcomes

In this exercise, you will learn to set up the Node.js environment, a popular Javascript based server framework, and node package manager \(NPM\) on your machine. To learn more about NodeJS, you can visit [https:\/\/nodejs.org](https://nodejs.org/). For this course, you just need to install Node.js on your machine and make use of it for running some front-end tools. You will learn more about the server-side support through Node.js in a subsequent course. At the end of this exercise, you will be able to:

* Complete the set up of Node.js and NPM on your machine
* Understand the basics of Node.js and NPM

#### Installing Node

* To install Node on your machine, go to [https:\/\/nodejs.org](https://nodejs.org/) and click on the Download button. Depending on your computer's platform \(Windows, MacOS or Linux\), the appropriate installation package is downloaded.As an example, on a Mac, you will see the following web page. Click on the Download button. Follow along the instructions to install Node on your machine. \(Note: Now Node gives you the option of installing a mature and dependable version and a more newer stable version. You can choose to install the mature and dependable version. I will continue to use this version in the course. You can choose to install the newer stable version if you wish. You may not see any perceptible differences between the two as users\).

**Note: On Windows machines, you may also to install \*\***[Git](https://git-scm.com/)**** on your machine if you don't have it already installed. Some of the Node based tools that we use later will need Git to be installed. You can download the installer from ****[here](http://git-scm.com/download)**\*\*.**

**Note: On Windows machines, you may need to configure your PATH environmental variable in case you forgot to turn on the add to PATH during the installation steps.**

#### Verifying the Node Installation

* Open a terminal window on your machine. If you are using a Windows machine, open a cmd window or PowerShell window with **admin** privileges.
* To ensure that your NodeJS setup is working correctly, type the following at the command prompt to check for the version of **Node** and **NPM**

```
node -v
npm -v
```

#### Conclusions

At the end of this exercise, your machine is now ready with the Node installed for further development. We will examine web development tools next.

## 4.3 Less is More: Less and Sass

### Less and Sass Resources

* [Less Getting Started](http://lesscss.org/)
* [Sass Basics](http://sass-lang.com/guide)
* [Getting Started with Less Tutorial](https://scotch.io/tutorials/getting-started-with-less)
* [Getting Started with Sass Tutorial](https://scotch.io/tutorials/getting-started-with-sass)

### Exercise \(Instructions\): Less

#### Objectives and Outcomes

In this exercise you will learn to write Less code and then automatically transform it into the corresponding CSS code. At the end of this exercise you will be able to:

* Write Less code using many of the features of Less
* Automatically convert the Less code into CSS

#### Adding Less Variables

* Open the _conFusion_ project in Brackets or any other text editor of your choice. In the css folder, create a file named_mystyles.less_. We will add the Less code into this file.
* Add the following Less variables into the file:

```
@white: #ffffff;
@off-white: #eeeeee;
@lt-gray: #dddddd;
@indigo: #303f9f;
@dark-indigo: #1a237e;
@light-indigo: #7986CB;

// Height variables
@carousel-height: 300px;
```

We have just added a few color and a height variable. We will make use of these variables while defining the classes.

#### Less Mixins

* Next we add mixing into the file as follows:

```
.zero-margin (@pad-up-dn: 0px, @pad-left-right: 0px) { 
  margin:0px auto; 
  padding: @pad-up-dn @pad-left-right;
}
```

We will make use of this to define several row classes next.

* Using the Mixin class that we defined earlier, add the following row classes to the file:

```
.row-header {
  .zero-margin();
}
.row-content {
  .zero-margin (50px, 0px);
  border-bottom: 1px ridge;
  min-height:400px;
}
.row-footer {
  .zero-margin(20px, 0px);
  background-color: #AfAfAf;
}
.jumbotron {
  .zero-margin(70px, 30px);
  background:@light-indigo;
  color:floralwhite;
}
```

Note the use of the mixin with various parameters in defining the classes.

#### Nesting Selectors

* Next we add a carousel class to illustrate the use of nesting of classes in Less, as follows:

```
.carousel {
  background:@dark-indigo;
  .item {
    height: @carousel-height;
    img {
      left: 0;
      min-height: @carousel-height;
      position: absolute;
      top: 0;
    }
  }
}
```

* Add another group of nesting classes with the navbar-inverse class as follows:

```
.navbar-inverse {
  background: @indigo;
  color:@white;
  .navbar-nav>.active>a {
    background: @dark-indigo;
    color: @white;
    &:hover {
      background: @dark-indigo;
      color: @white;
    }
    &:focus {
      background: @dark-indigo;
      color: @white;
    }
  }
  .navbar-nav>.open>a {
    background: @dark-indigo;
    color: @white;
    &:hover {
      background: @dark-indigo;
      color: @white;
    }
    &:focus {
      background: @dark-indigo;
      color: @white;
    }
  }
  .navbar-nav {
    .open {
      .dropdown-menu>li>a {
        background-color: @indigo;
        color:@off-white;
        &:hover {
          color:#000000;
        }
      }
      .dropdown-menu {
        background-color: @indigo;
        color:@off-white;
     }
    }
  }
}
```

#### Add the remaining CSS classes

* Finally we add in those CSS classes which do not fall into any of the above categories. These still use the Less variables, but do not use nesting or mixins:

```
address {
  color:#0f0f0f;
  font-size:80%;
  margin:0px;
}
body {
  align:center;
  padding:50px 0px 0px 0px;
  z-index:0;
}
.tab-content {
  border-bottom: 1px solid @lt-gray;
  border-left: 1px solid @lt-gray;
  border-right: 1px solid @lt-gray;
  padding: 10px;
}
.affix {
  top:100px;
}
#carouselButtons {
  bottom: 0px;
  position: absolute;
  right:0px;
}
```

#### Installing and using the lessc Compiler

* Now we install the node module to support the compilation of the Less file. To do this, type the following at the command prompt:

```
npm install -g less
```

This will install the _less_ NPM module globally so that it can be used by any project. **Note: if you are executing this on a Mac or Linux machine, you may need to add "sudo" to the beginning of this command**. This will make available the _lessc_ compiler for us so that we can compile Less files.

* Next, go to the CSS folder on your machine and rename the _mystyles.css_ file that you have there as _mystyles-old.css_. This is to save the CSS file that we have been using so far. We will be creating a new _mystyles.css_ file by compiling the Less file.
* Next type the following at the command prompt to compile the Less file into a CSS file:

```
lessc mystyles.less > mystyles.css
```

#### Conclusions

In this exercise you learnt to write Less code and then automatically generating the CSS file by compiling the Less code.

## 4.4 Web Tools: Bower

### Bower Related Information

* [Bower Website](http://bower.io/)
* [Bower 101](https://medium.com/@ZaidHanania/bower-101-c0b57322df8)
* [Node, Grunt, Bower and Yeoman - A Modern web dev's Toolkit](http://juristr.com/blog/2014/08/node-grunt-yeoman-bower/)

### Exercise \(Instructions\): Web Tools: Bower

#### Objectives and Outcomes

In this exercise we will explore Bower to enable us to automatically fetch Bootstrap and Font Awesome files. Then we will make use of the files fetched by Bower in our web page. At the end of this exercise you will be able to:

* Use Bower to fetch web packages and assets from global repositories automatically
* Use the Bower components in your web page

#### Installing Bower

* Install Bower as a global node module. To do this, type the following at the command prompt:

```
npm install -g bower
```

Note: Precede this command with _sudo_ on Mac or Linux

#### Creating bower.json File

* Create and initialize a bower.json file by typing the following at the command prompt:

```
 bower init
```

Bower will ask several questions which you should answer as follows:

Name: conFusion \(the default\)

version: 1.0.0

description: Website for an awesome restaurant

main file: index.html

what type of modules does this package expose? \(leave all unselected, just hit enter\)

keywords: conFusion, Fusion Restaurant

author: \(Your own name\)

license: \(MIT\)

Say yes to the remaining questions except the last one.

Looks Good? Y

* Have a look at the contents of the _bower.json_ file that was created.

#### Installing Bower Components

> You may got ECMDERR when executing the bower install command.
> 
> That's may caused by git configuration.
> 
> So, please try to change the git global configuration with the following command.
> 
> `git config --global url."https://".insteadOf git://`
> 
> [Here ](http://stackoverflow.com/questions/21789683/how-to-fix-bower-ecmderr)is the original article.
> 
> If ECMDERR happen again after you install a component and start to install the 2nd one, you may need to use the following command.
> 
> `npm cache clean`
> `bower cache clean`

* We will first install Bootstrap using Bower. To do this type the following at the command prompt:

```
bower install bootstrap -S
```

This will install Bootstrap to our project, and since Bootstrap depends on jQuery, it will automatically install jQuery. The "-S" flag indicates that Bootstrap should be saved as a dependency for our our project in the _bower.json_ file.

* Next, to install Font Awesome, you need to type the following at the command prompt:

```
bower install font-awsome -S
```

You may want to install angular as well.

```
bower install angular -S
```

> bower.json will not be updated without '-S'  !!!

#### Examining Bower Components

* In the _conFusion_ folder, you will find a _bower\_components_ folder that Bower created. The components that Bower fetched for you are stored in this folder. Browse the folder and the sub-folders therein to see the contents.
* Back in the _conFusion_ folder, examine the contents of the _bower.json_ file to see that Bower has added in new information about dependencies. This specifies that the current project is dependent on Bootstrap and Font Awesome.

#### Using Bower Components

* To make use of the Bower components, we will update the CSS and JS links in our web pages to use the files in the Bower components folder. Update the CSS links in the index.html, aboutus.html and contacts.html page as follows:

```
<link href="bower_components/bootstrap/dist/css/bootstrap.min.css" rel="stylesheet">
<link href="bower_components/bootstrap/dist/css/bootstrap-theme.min.css" rel="stylesheet">
<link href="bower_components/font-awesome/css/font-awesome.min.css" rel="stylesheet">
```

* Similarly, update the JS links in the files as follows:

```
<script src="bower_components/jquery/dist/jquery.min.js"></script>
<!-- Include all compiled plugins (below), or include individual files as needed -->
<script src="bower_components/bootstrap/dist/js/bootstrap.min.js"></script>
```

* The project now makes use of the files fetched by Bower in the web pages.

#### Conclusions

In this project we learnt about Bower and how we can make use of Bower to fetch the web components. Thereafter we learnt how to make use of the web components in our project.

### Why use Bower?

With _**bower**_, you do not need to include the _**bower\_components**_ folder in you version control system \(git\).

In a new development environment, after clone the project folder from the version control system, you just need to fetch all bower components with the following command:

```
bower install
```

This command will fetch all bower components based on the file of _**bower.json**_.



## 4.5 Assignment 4: Additional Resources

### Bootstrap Resources

* [Bootstrap Modal Methods](http://getbootstrap.com/javascript/#modals-methods)

