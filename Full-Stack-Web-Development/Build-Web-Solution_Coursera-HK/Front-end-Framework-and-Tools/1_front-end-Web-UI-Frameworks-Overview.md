# 1. Front-end Web UI Frameworks Overview: Bootstrap

## 1.1 Full Stack Web Development: The Big Picture

### Useful Links

* [What is a Full Stack developer?](http://www.laurencegellert.com/2012/08/what-is-a-full-stack-developer/)
* [Wait, Wait… What is a Full-stack Web Developer After All?](http://edward-designer.com/web/full-stack-web-developer/)
* [The Myth of the Full-stack Developer](http://andyshora.com/full-stack-developers.html)
* [Multi-tier Architecture](https://en.wikipedia.org/wiki/Multitier_architecture)
* [What is the 3-Tier Architecture?](http://www.tonymarston.net/php-mysql/3-tier-architecture.html)

## 1.2 Introduction to Bootstrap

### Bootstrap Official Resources

* [Bootstrap Home Page](http://getbootstrap.com/)
* [Bootstrap typography](http://getbootstrap.com/css/#type)

### Front-end Frameworks

* [The 5 Most Popular Frontend Frameworks of 2014 Compared](http://www.sitepoint.com/5-most-popular-frontend-frameworks-compared/) \(a recent opinion piece comparing the most popular front-end UI frameworks\)
* [Front-end Frameworks v2.5](http://usablica.github.io/front-end-frameworks/) and [comparison](http://usablica.github.io/front-end-frameworks/compare.html) \(yet another recent comparison of front-end frameworks\)

### Exercise: Getting Started with Bootstrap

#### Objectives and Outcomes

This exercise introduces you to the basic features and some classes of Bootstrap. At the end of this exercise, you will be able to:

* Understand how to set up a web project to use Bootstrap
* Include the Bootstrap CSS and JS classes into a web page
* Design a web page structure using a few basic Bootstrap classes

Note: Please remember to retain the folder and all the files that you create in this exercise. Further exercises will build upon the files that you create in this exercise. DO NOT DELETE the files at the end of the exercise.

#### Setting up the Project Folder

* Go to a convenient folder on your computer and create a folder named _conFusion_. This will be the name of the project that we will implement in the set of exercises to follow.

#### Downloading Bootstrap

* Go to the Bootstrap website [http:\/\/getbootstrap.com](http://www.getbootstrap.com/) and click on the download button to download the zip file containing Bootstrap files.
* Move the _bootstrap-3.3.5-dist.zip_ file to the _conFusion_ folder you created above and unzip it. You should now see a folder named _bootstrap-3.3.5-dist_. Go to this folder and move the three folders there \(_css_, _fonts_ and js\) to_conFusion_ folder above. You can now delete the zip file and _bootstrap-3.3.5-dist_ folder. Now you are all set to use Bootstrap to design your web project.

#### Download index.html file

* Download [_index.html_](https://d396qusza40orc.cloudfront.net/phoenixassets/web-frameworks/index.html) file to the _conFusion_ folder. This is your starting web page for the project. We have already created the web page with some content to get you started. We will use Bootstrap to style this web page, and learn Bootstrap features, classes and components along the way.

#### Getting your Web page Bootstrap ready

* Open the _index.html_ file in your favourite text editor. If you are using **Brackets**, you can open the _conFusion_ folder from within Brackets and then open the _index.html_ file as a working file. You can do the same with **Sublime Text**and some other text editors too.
* Open the index.html file in your favourite browser so that you can preview the formatted web page in the browser. If you are using **Brackets**, you can use the _Live Preview_ button to load and automatically refresh the page in Chrome as you edit the files. A similar set up can be done with **Sublime Text** after installing some plug-ins.
* Insert the following code in the head of _index.html_ file before the title.

```
 <meta charset="utf-8">
 <meta http-equiv="X-UA-Compatible" content="IE=edge">
 <meta name="viewport" content="width=device-width, initial-scale=1">
 <!-- The above 3 meta tags *must* come first in the head; any other head  content must come *after* these tags -->
```

* Add the following code in the head after the title. This will include Bootstrap CSS into your web page.

```
 <!-- Bootstrap -->
 <link href="css/bootstrap.min.css" rel="stylesheet">
 <link href="css/bootstrap-theme.min.css" rel="stylesheet">

 <!-- HTML5 shim and Respond.js for IE8 support of HTML5 elements and media queries -->
 <!-- WARNING: Respond.js doesn't work if you view the page via file:// -->
 <!--[if lt IE 9]> <script src="https://oss.maxcdn.com/html5shiv/3.7.2/html5shiv.min.js"></script> <script src="https://oss.maxcdn.com/respond/1.4.2/respond.min.js"></script>
 <![endif]-->
```

* Note the subtle change in the fonts of the content of the web page. This is the Bootstrap typography effect coming into play. The default Bootstrap typography sets the font to Helvetica Neue and selects the appropriate font size based on the choice of the heading style and paragraph style for the content.
* At the bottom of the page, just before the end of the body tag, add the following code to include the JQuery library and Bootstrap's Javascript plugins. Bootstrap by default uses the JQuery Javascript library for its Javascript plugins. Hence the need to include JQuery library in the web page.

```
 <!-- jQuery (necessary for Bootstrap's JavaScript plugins) --> 
 <script src="https://ajax.googleapis.com/ajax/libs/jquery/1.11.3/jquery.min.js"></script>
 <!-- Include all compiled plugins (below), or include individual files as needed -->
 <script src="js/bootstrap.min.js"></script>
```

#### Using a Container class

* We use the container class to keep content within a fixed width on the screen, determined by the size of the screen. The alternative is to use the container-fluid class to make the content automatically to span the full width of the screen. We will discuss further about this when we discuss the Bootstrap grid system in the next lecture. Add the container class to the top most div in the file as follows.

```
 <div class="container"> ...
```

#### Dividing the content into rows

* Let us now add the class _row_ to the first-level inner _div_ elements inside the container. This organizes the page into rows of content. In the next exercise, we will see how we can add other classes to the rows.

```
 <div class="row"> ...
```

#### Creating a Jumbotron

* Let us add the class jumbotron to the header class as shown below. This turns the header element into a Bootstrap component named Jumbotron. A jumbotron is used to showcase key content on a website. In this case we are using it to highlight the name of the restaurant.

```
 <header class="jumbotron"> ...
```

* In the header add a container class to the first inner div and a row class to the second inner div.

#### Creating a footer

* Finally, in the footer add a container class to the first inner div and a row class to the second inner div.

#### Conclusion

We have now understood how to set up a web project to use Bootstrap. In the next lecture, we will explore further on responsive design and Bootstrap's grid system.

## 1.3 Responsive Design and Bootstrap Grid System

### Bootstrap Official Documentation

* [Bootstrap Grid System](http://getbootstrap.com/css/#grid)

### Responsive Design

* [The Subtle Magic Behind Why the Bootstrap 3 Grid Works](http://www.helloerik.com/the-subtle-magic-behind-why-the-bootstrap-3-grid-works) \(a detailed explanation of why the Bootstrap grid system works the way it does, a delight to read!\)
* [What The Heck Is Responsive Web Design?](http://johnpolacek.github.io/scrolldeck.js/decks/responsive/) \(a short presentation that introduces responsive web design\)
* [Beginner’s Guide to Responsive Web Design](http://blog.teamtreehouse.com/beginners-guide-to-responsive-web-design) \(simple introduction to responsive web design\)
* [The 2014 Guide to Responsive Web Design](http://blog.teamtreehouse.com/modern-field-guide-responsive-web-design) \(an updated guide to responsive design\)

### Exercise: Responsive Design and Bootstrap Grid System

#### Objectives and Outcomes

This exercise introduces you to responsive design and Bootstrap support for mobile first responsive design through the use of the grid system. In addition we learn how to customize some of the Bootstrap classes through defining our own modifications in a separate CSS file. At the end of this exercise, you will be able to:

* Create responsive websites using the Bootstrap grid system
* Customize the CSS classes through your own additions in a separate CSS file

Note: In this exercise we will continue to update the \*\*_**index.html**_**\*\***\*\***\*\***\*\***\*\***\*\***\*\***\*\***\*\***\*\***\*\***\*\*** file in the **\*\***\*\***\*\***\*\***\*\***\*\***\*\***\*\***\*\***\*\***\*\***\*\***_**conFusion**_\*\* folder that we created and edited in the previous lecture.\*\*

#### Bootstrap Grid System and Responsive Design

Bootstrap is designed to be mobile first, meaning that the classes are designed such that we can begin by targeting mobile device screens first and then work upwards to larger screen sizes. The starting point for this is first through media queries. We have already added the support for media queries in the last lecture, where we added this line to the head:

```
<meta name="viewport" content="width=device-width, initial-scale=1">
```

The _viewport_ meta tag ensures that the screen width is set to the device width and the content is rendered with this width in mind. This brings us to the second issue, designing the websites to be responsive to the size of the viewport. This is where the Bootstrap grid system comes to our aid. Bootstrap makes available four sizes, xs for extra small, sm for small, md for medium and lg for large screen sizes. We have already seen the basics of responsive design. In this exercise, we will employ the Bootstrap grid classes to design the websites. We have already divided the content into rows. Each row in Bootstrap grid system is divided into 12 columns. We would like our website to have the content stacked on extra small devices, but become horizontal within each row for smaller devices and beyond. Towards this goal, we will make use of the classes .col-xs-\*, .col-sm-\*, col-md-\*, and .col-lg-\* for defining the layouts for the various device sizes. We can specify how many columns each piece of content will occupy within a row, all adding up to 12 or a multiple thereof.

#### Applying column classes within each row

* In the header row, we will display the restaurant name and the description to occupy 8 columns, while we will leave four columns for displaying the restaurant logo in the future. Let us go into the jumbotron and define the classes for the inner divs as follows:

```
 <div class="col-xs-12 col-sm-8"> ... </div>
 <div class="col-xs-12 col-sm-4"> ... </div>
```

* For the remaining three div rows that contain content, let us define the classes for the inner divs as follows:

```
 <div class="col-xs-12 col-sm-3"> ... </div>
 <div class="col-xs-12 col-sm-9"> ... </div>
```

* For the footer, let us define the classes for the inner divs as follows:

```
 <div class="col-xs-6 col-sm-3"> ... </div>
 <div class="col-xs-6 col-sm-5"> ... </div>
 <div class="col-xs-12 col-sm-4"> ... </div>
 <div class="col-xs-12"> ... </div>
```

Now you can see how the web page has been turned into a mobile-first responsive design layout.

#### Using Push, Pull and Offset with column layout classes

* In the content rows, we would like to have the title and description to alternate so that it gives an interesting look to the web page. For extra small screens, the default stacked layout works best. This can be accomplished by using the .col-sm-push-\* and .col-sm-pull-\* for the first and the third rows as follows:

```
 <div class="col-xs-12 col-sm-3 col-sm-push-9"> ... </div>
 <div class="col-xs-12 col-sm-9 col-sm-pull-3"> ... </div>
```

* For the div containing the &lt;ul&gt; with the site links, update the class as follows:

```
 <div class="col-xs-5 col-xs-offset-1 col-sm-2 col-sm-offset-1">
```

#### List styles

* You can use several list styles to display lists in different formats. In this exercise, we will use the unordered list style_list-unstyled_ to display the links at the bottom of the page without the bullets. To do this, go to the links in the footer and update the ul as follows

```
<ul class="list-unstyled"> ... </ul>
```

#### Using Custom CSS classes

We can define our own custom CSS classes in a separate CSS file, and also customize some of the built-in CSS classes. We will now attempt to do this in this part of the exercise.

* Create a file named _mystyles.css_ in the _css_ folder. Open this file to edit the contents. Add the following CSS code to the file:

```
.row-header{ 
    margin:0px auto; 
    padding:0px auto;
}

.row-content { 
    margin:0px auto; 
    padding: 50px 0px 50px 0px; 
    border-bottom: 1px ridge; 
    min-height:400px;
}

.row-footer{ 
    background-color: #AfAfAf; 
    margin:0px auto; 
    padding: 20px 0px 20px 0px;
}
```

* Include the mystyles.css file into the head of the index.html file as follows:

```
<link href="css/mystyles.css" rel="stylesheet">
```

* Then add these classes to the corresponding rows in the _index.html_ file as follows. See the difference in the_index.html_ file in the browser. The first one is for the row in the &lt;header&gt;, the next three for the rows in the content, and the last one directly to the &lt;footer&gt; tag.

```
 <div class="row row-header"> ... </div>
 <div class="row row-content"> ... </div>
 <div class="row row-content"> ... </div>
 <div class="row row-content"> ... </div>
 <footer class="row-footer"> ... </footer>
```

* Our last set of customization is to the jumbotron and the address. Add the following to mystyles.css file:

```
.jumbotron {  
    padding:70px 30px 70px 30px;
    margin:0px auto;
    background: #7986CB ;
    color:floralwhite;
}

address{
    font-size:80%;
    margin:0px;
    color:#0f0f0f;
}
```

* Now we begin to see the web page take a form closer to our final design for this module.

#### Conclusion

In this exercise, we reviewed responsive design and the Bootstrap grid system. We also learnt how to customize using our own CSS classes.

## 1.4 Navigation and Navigation Bar: Additional Resoursces

### Official Bootstrap Resources

* [Navbar](http://getbootstrap.com/components/#navbar)
* [Breadcrumbs](http://getbootstrap.com/components/#breadcrumbs)

### General

* [Accessible Rich Internet Applications \(ARIA\)](https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA) \(Accessibility support and screen reader support\)

### Information Architecture

* [Information Architecture 101: Techniques and Best Practices](http://sixrevisions.com/usabilityaccessibility/information-architecture-101-techniques-and-best-practices/) \(Quick introduction to Information architecture with respect to website design\)
* [Web Site Information Architecture models](http://webdesignfromscratch.com/website-architecture/ia-models/) \(Another good resource on information architecture\)
* [What is information architecture?](http://www.steptwo.com.au/papers/kmc_whatisinfoarch/) \(Good definition and explanation about the topic\)
* [Information Architecture Tutorial](http://www.webmonkey.com/2010/02/Information_Architecture_Tutorial/) \(Comprehensive look from a website design perspective\)

### Navigation Bar Design

* [Designing A Winning Navigation Menu: Ideas and Inspirations](http://www.hongkiat.com/blog/navigation-design-ideas-inspiration/) \(Good suggestions on how to design navigation for a website\)
* [Are You Making These Common Website Navigation Mistakes?](https://blog.kissmetrics.com/common-website-navigation-mistakes/) \(Worth reading at least to learn what not to do\)
* [3 Reasons We Should Stop Using Navigation Bars](http://www.webdesignerdepot.com/2014/01/3-reasons-we-should-stop-using-navigation-bars/) \(A provocative view on navigation bars\)

### Breadcrumbs

* [Breadcrumb Navigation Examined: Best Practices & Examples](http://www.hongkiat.com/blog/breadcrumb-navigation-examined-best-practices-examples/) \(Great suggestions on using breadcrumbs for navigation\)
* [Breadcrumb Navigation: A Guide On Types, Benefits And Best Practices](http://blog.woorank.com/2014/11/breadcrumb-navigation-guide/) \(Another great resource on types and usage of breadcrumbs\)

### Icon Fonts

* [Why And How To Use Icon Fonts](http://vanseodesign.com/web-design/icon-fonts/) \(a good overview of icon fonts\)
* [Icon Fonts are Awesome](https://css-tricks.com/examples/IconFont/) \(another good introduction to icon fonts\)
* [FontAwesome](https://fortawesome.github.io/Font-Awesome/) \(one of the most popular icon fonts\)
* [Get started with FontAwesome](https://fortawesome.github.io/Font-Awesome/get-started/) \(good official help\)
* [Bootstrap-Social](http://lipis.github.io/bootstrap-social/)
* [The Final Nail in the Icon Fonts Coffin?](http://www.sitepoint.com/final-nail-icon-fonts-coffin/) \(a controversial opinion piece on icon fonts\)
* [Using SVGs](http://gomakethings.com/using-svgs/) \(alternative to icon fonts\)

### Exercise: Navbar

#### Objectives and Outcomes

In this exercise, we will examine the navigation support that we can build into a web page using the Navbar in Bootstrap. We will also learn the basic use of icons in web page design using the built-in glyphicons that are part of Bootstrap, the Font Awesome icons, and bootstrap-social icons. At the end of this exercise, you will be able to:

* Create a navigation structure for your website using the Navbar
* Use icons within your website to represent various entities making use of the glyphicons, font-awesome icons and bootstrap-social icons
* Include additional CSS classes into your project

#### Create a basic navigation bar

* We will now add a simple navigation bar to the web page so that it provides links to the other pages on the website. Start by adding the following code to the body just above the header jumbotron.

```
<nav class="navbar navbar-inverse navbar-fixed-top" role="navigation"> 
  <div class="container">
    <ul class="nav navbar-nav"> 
      <li class="active"><a href="#">Home</a></li> 
      <li><a href="#">About</a></li> 
      <li><a href="#">Menu</a></li> 
      <li><a href="#">Contact</a></li> 
    </ul> 
  </div> 
</nav>
```

In the above code, we can see the use of the nav element to specify the navigation information for the website. This nav element is styled by the _navbar_ that declares it as a navigation bar, and the _navbar-inverse_ class to specify that the page should use the dark navigation bar. In addition the inner _ul_ is used to specify the items to be put in the navigation bar. This _ul_ is styled with _nav_ and _navbar-nav_ classes to specify that the items should be displayed inline inside the navigation bar. We also use the container class inside the navigation bar. This navigation bar does not use responsive design at the moment.

#### Creating a responsive navigation bar

* We would like the navigation bar elements to collapse for shorter screens, to be replaced by a toggle button so that the items can be toggled on or off when required on smaller screens. This can be achieved by adding the following code to the navigation bar, just below the container div

```
<div class="navbar-header">  
  <button type="button" class="navbar-toggle collapsed" data-toggle="collapse" data-target="#navbar" aria-expanded="false" aria-controls="navbar">    
    <span class="sr-only">Toggle navigation</span>    
    <span class="icon-bar"></span>    
    <span class="icon-bar"></span>    
    <span class="icon-bar"></span>  
  </button>  
<a class="navbar-brand" href="#">Ristorante Con Fusion</a></div>
```

You will now notice the addition of a link to the left of the Home link with the name of the restaurant. This is the brand name for the website. You can replace this with the logo for the website. This is created by the _&lt;a class="navbar-brand"&gt;_ tag. The other part is the creation of a button with three horizontal lines. For larger screens, this button is hidden. For smaller screens, this button becomes visible. This button will act as the toggle for the navbar items on small screens. At the moment you still see the items being displayed in the navigation bar even for smaller screens. We will fix this in the next step.

* To hide the items from the navigation bar for smaller screens, we need to enclose the _ul_ within another navigation bar as follows:

```
<div id="navbar" class="navbar-collapse collapse"> 
  <ul class="nav navbar-nav"> ... </ul> 
</div>
```

By doing this, we are specifying that this _navbar_ with the id _navbar_ will be collapsed on smaller screens, but can be toggled on or off when the toggle button is clicked. Note the use of _data-toggle="collapse" data-target="\#navbar" aria-expanded="false" aria-controls="navbar"_ within the button. This specifies that the menu items are collapsed on smaller screens when the toggle button is visible. They can be displayed or hidden by clicking the toggle button.

Note: that the navbar scrolls when the web page in the browser is scrolled. If we wish to keep the navigation bar always visible at the top of the page when the page is scrolled, then we should change the navbar-static-top to navbar-fixed-top. Let us do this now. Note that after the change, the navigation bar remains visible at the top of the page even when the page is scrolled.

#### Adding a Dropdown Menu to the Navigation Bar

* The next modification adds a Dropdown menu to the navigation bar. Let us target the "Menu" item in the navigation bar and turn it into a dropdown menu item. When this item is clicked, a dropdown menu will be displayed. To do this, modify the list item for the "Menu" item in the navigation bar by replacing it with the following code:

```
body{ 
  padding:50px 0px 0px 0px; 
  z-index:0;
}

.navbar-inverse { 
  background: #303F9F;
}

.navbar-inverse .navbar-nav > .active > a,
.navbar-inverse .navbar-nav > .active > a:hover,
.navbar-inverse .navbar-nav > .active > a:focus { 
  color: #fff; 
  background: #1A237E;
}

.navbar-inverse .navbar-nav > .open > a, 
.navbar-inverse .navbar-nav > .open > a:hover, 
.navbar-inverse .navbar-nav > .open > a:focus { 
  color: #fff; 
  background: #1A237E;
}

.navbar-inverse .navbar-nav .open .dropdown-menu> li> a,
.navbar-inverse .navbar-nav .open .dropdown-menu { 
  background-color: #303F9F; 
  color:#eeeeee;
}

.navbar-inverse .navbar-nav .open .dropdown-menu> li> a:hover { 
  color:#000000;
}
```

* We are already beginning to see the page format close to the final format for this module.

#### Using Icon Fonts and Other CSS classes

* The last part of the exercise is to make use of the glyphicons that are provided as part of Bootstrap. In addition we will also use two additional popular font icons.
* One of the most popular iconic font toolkit is Font Awesome. Go to its website [https:\/\/fortawesome.github.io\/Font-Awesome\/](https://fortawesome.github.io/Font-Awesome/) and download the zip file and move it to the _conFusion_ folder and unzip it. You will find the _font-awesome-4.4.0_ folder being created. Go into this folder and move the contents of the _css_ folder to _conFusion\/css\_and the contents of the \_fonts_ folder to _conFusion\/fonts_ folder. Then you can delete the _font-awesome-4.4.0_ folder.
* Download the [_bootstrap-social.css_](https://d396qusza40orc.cloudfront.net/phoenixassets/web-frameworks/bootstrap-social.css) file to _conFusion\/css_ folder. This is a modified version of the bootstrap-social available on the [http:\/\/lipis.github.io\/bootstrap-social\/.](http://lipis.github.io/bootstrap-social/) We added in support for G+ and YouTube buttons.
* We now need to include the css files for font awesome and bootstrap-social in the index.html file. Add the following code to the head of the file after the links for importing Bootstrap CSS classes:

```
<link href="css/font-awesome.min.css" rel="stylesheet"> 
<link href="css/bootstrap-social.css" rel="stylesheet">
```

* Let us now use some font icons in our web page and decorate it. First use the glyphicons that is part of Bootstrap to add a home icon to the Home link on the navigation bar. Update the home list item as follows:

```
<li class="active"><a href="#"><span class="glyphicon glyphicon-home" aria-hidden="true"></span> Home</a></li>
```

* Next, go down to the address in the footer of the page and replace the "Tel.", "Fax" and "Email" with the corresponding font awesome based icons as follows:

```
<i class="fa fa-phone"></i>: +852 1234 5678<br> 
<i class="fa fa-fax"></i>: +852 8765 4321<br> 
<i class="fa fa-envelope"></i>:  <a href="mailto:confusion@food.net">confusion@food.net</a>
```

* Finally, let us use the bootstrap-social CSS classes to create the social buttons in the footer by replacing the social sites' links with the following code:

```
<div class="nav navbar-nav" style="padding: 40px 10px;"> 
  <a class="btn btn-social-icon btn-google-plus" href="http://google.com/+"><i class="fa fa-google-plus"></i></a> <a class="btn btn-social-icon btn-facebook" href="http://www.facebook.com/profile.php?id="><i class="fa fa-facebook"></i></a> 
  <a class="btn btn-social-icon btn-linkedin" href="http://www.linkedin.com/in/"><i class="fa fa-linkedin"></i></a> <a class="btn btn-social-icon btn-twitter" href="http://twitter.com/"><i class="fa fa-twitter"></i></a> 
  <a class="btn btn-social-icon btn-youtube" href="http://youtube.com/"><i class="fa fa-youtube"></i></a> 
  <a class="btn btn-social-icon" href="mailto:"><i class="fa fa-envelope-o"></i></a> 
</div>
```

#### Conclusions

We have learnt how to add navigation support into a web page using the navigation bar. We also learnt about using other CSS class and other icon fonts in a web project.

## 1.5 Assignment 1: Resources

### Bootstrap Official Documentation

* [Bootstrap Breadcrumbs](http://getbootstrap.com/components/#breadcrumbs) \(resource on Bootstrap site\)


