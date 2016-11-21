# 3. Bootstrap Javascript Components

## 3.1 Bootstrap Javascript Components Overview

### Bootstrap Resources

* [Bootstrap and JavaScript](http://getbootstrap.com/javascript/)
* [Bootstrap JS Data Attributes](http://getbootstrap.com/javascript/#js-data-attrs)

## 3.2 Tabs, Pills and Tabbed Navigation

### Bootstrap Resources

* [Bootstrap Navs](http://getbootstrap.com/components/#nav)
* [Bootstrap Tabs](http://getbootstrap.com/components/#nav-tabs)
* [Bootstrap Pills](http://getbootstrap.com/components/#nav-pills)
* [Bootstrap Togglable Tabs Javascript plugin](http://getbootstrap.com/javascript/#tabs)

### Exercise \(Instructions\): Tabs

#### Objectives and Outcomes

In this exercise we will explore Bootstrap tabs and tabbed navigation. In particular we will learn about the use of tabs for organizing the content. At the end of this exercise you will be able to:

* Design a web page to use tabbed navigation for organizing the content
* Use tab panes and organize the content into the panes
* Facilitate navigation among the tab panes using the tabbed navigation elements

#### Adding Tab Navigation Elements

* Open the _aboutus.html_ page and move to the second content row containing the details of the corporate leadership of the restaurant.
* Right after the Corporate Leadership heading, introduce the following code to set up the tabbed navigation:

```
<ul class="nav nav-tabs" role="tablist">
  <li role="presentation" class="active">
    <a href="#peter" aria-controls="peter" role="tab" data-toggle="tab">Peter Pan, CEO</a>
  </li>
  <li role="presentation">
    <a href="#danny" aria-controls="danny" role="tab" data-toggle="tab">Danny Witherspoon, CFO</a>
  </li>
  <li role="presentation">
    <a href="#agumbe" aria-controls="agumbe" role="tab" data-toggle="tab">Agumbe Tang, CTO</a>
  </li>
  <li role="presentation">
    <a href="#alberto" aria-controls="alberto" role="tab" data-toggle="tab">Alberto Somayya, Exec. Chef</a>
  </li>
</ul>
```

Note the use of the _&lt;ul&gt;_ tag with the _nav_ and _nav-tabs_ classes to set up the tab navigation. Each list item within the list acts as the tab element. Within each list item, note that we set up the _&lt;a&gt;_ tags with the _href_ pointing to the _id_ of the tab pane of content to be introduced later. Also note that the _&lt;a&gt;_ tag contains the _data-toggle=tab_ attribute. The first list element's _&lt;a&gt;_ tag contains the class _active_. This tab will be the open tab when we view the web page. We can switch to the other tabs using the tabbed navigation that we just set up.

#### Adding Tab Content

* The details about the various corporate leaders should now be organized into various tab panes. To begin this, we will enclose the entire content into a div element with the class tab-content as specified below:

```
<div class="tab-content">
  ...
</div>
```

* Then we take the name and description of the CEO of the company and enclose it within a tab-pane as follows

```
<div role="tabpanel" class="tab-pane fade in active" id="peter">
  <h3>Peter Pan <small>Chief Epicurious Officer</small></h3>
  <p> ... </p>
</div>
```

Note the use of the _tab-pane, fade, in, \_and_ active_ classes and with \_peter_ as the id. This is the same id used as the_href_ in the _&lt;a&gt;_ link in the navigation.

* The remaining content is also similarly enclosed inside appropriate divs with the correct ids and the classes specified as above. Only the first tab pane will have the _in_ and _active_ classes specified to indicate that the content should be visible on the web page by default.

#### Modifying the tab-content CSS

* We now modify the CSS styles for the tab-content class in the _mystyles.css_ file as follows:

```
.tab-content {
  border-left: 1px solid #ddd;
  border-right: 1px solid #ddd;
  border-bottom: 1px solid #ddd;
  padding: 10px;
}
```

This modification adds a 1px border to the tab content which joins with the upper border introduced by the tab navigation element to give a clean tab like appearance.

#### Conclusions

In this exercise we learnt the use of tabbed navigation, tab content and tab panes and their use in organizing and navigating within the content in a page.

## 3.3 Hide and Seek: Collapse, Accordion, Scrollspy and Affix

### Bootstrap Resources

* [Bootstrap Collapse Plugin](http://getbootstrap.com/javascript/#collapse)
* [Bootstrap Accordion](http://getbootstrap.com/javascript/#collapse-example-accordion)
* [Bootstrap Scrollspy](http://getbootstrap.com/javascript/#scrollspy)
* [Bootstrap Affix](http://getbootstrap.com/javascript/#affix)

### Exercise \(Instructions\): Accordion, Scrollspy and Affix

#### Objectives and Outcomes

In this exercise we explore the use of the collapse Javascript plugin together with panel component and panel group classes to create an accordion to show\/hide content in a web page. We also leverage the nav pills class to create a side navigation menu. We use the scrollspy plugin to highlight the scroll position within this nav component. In addition we use the Affix plugin to enable the nav to scroll with the page initially, but get fixed shortly thereafter. At the end of this exercise, you will be able to:

* Design an accordion using the collapse plugin together with the panel component and panel-group class
* Use a scrollspy to highlight the current scroll position in a nav
* Use the affix plugin together with the scrollspy on the side nav component

#### Adjusting the Content Rows

* For the first row of the content, adjust the column classes for the first column to _col-xs-12 col-sm-6 col-lg-8_. Then adjust the column classes for the second column to _col-xs-12 col-sm-6 col-lg-4_.
* For the remaining two rows, delete the second columns and adjust the column classes for the first column of content to _col-xs-12_ so that it occupies the entire 12 columns.

#### Converting Tabs to Accordion

* First delete the &lt;ul&gt; class that was introduced for the tabbed navigation.
* Then the turn the _tab-content_ div into a _panel-group_ div. Use the code structure as shown below:

```
<div class="panel-group" id="accordion" role="tablist" aria-multiselectable="true">
  ...
</div>
```

* Then, replace the first tab-pane into a panel such that the name appears as a panel heading, and the &lt;p&gt; will be in the panel body. Use the structure of the code as shown below:

```
<div class="panel panel-default">
  <div class="panel-heading" role="tab" id="headingPeter">
    <h3 class="panel-title">
      <a role="button" data-toggle="collapse" data-parent="#accordion" href="#peter" aria-expanded="true" aria-controls="peter">Peter Pan <small>Chief Epicurious Officer</small></a>
    </h3>
  </div>
  <div role="tabpanel" class="panel-collapse collapse in" id="peter" aria-labelledby="headingPeter">
    <div class="panel-body">
      <p>...</p>
    </div>
  </div></div>
```

* For the remaining three leaders, use the same structure as above, with the appropriate ids set up for the panels, as shown in the code structure below:

```
<div class="panel panel-default">
  <div class="panel-heading" role="tab" id="headingDanny">
    <h3 class="panel-title">
      <a class="collapsed" role="button" data-toggle="collapse" data-parent="#accordion" href="#danny" aria-expanded="false" aria-controls="danny">Dhanasekaran Witherspoon <small>Chief Food Officer</small></a>
    </h3>
  </div>
  <div role="tabpanel" class="panel-collapse collapse" id="danny" aria-labelledby="headingDanny">
    <div class="panel-body">
      <p> . . . </em></p>
    </div>
  </div>
</div><div class="panel panel-default">
  <div class="panel-heading" role="tab" id="headingAgumbe">
    <h3 class="panel-title">
      <a class="collapsed" role="button" data-toggle="collapse" data-parent="#accordion" href="#agumbe" aria-expanded="false" aria-controls="agumbe">Agumbe Tang <small>Chief Taste Officer</small></a>
    </h3>
  </div>
  <div role="tabpanel" class="panel-collapse collapse" id="agumbe" aria-labelledby="headingAgumbe">
    <div class="panel-body">
      <p>...</em></p>
    </div>
  </div></div>
  <div class="panel panel-default">
    <div class="panel-heading" role="tab" id="headingAlberto">
      <h3 class="panel-title">
        <a class="collapsed" role="button" data-toggle="collapse" data-parent="#accordion" href="#alberto" aria-expanded="false" aria-controls="alberto">Alberto Somayya <small>Executive Chef</small></a>
      </h3>
    </div>
    <div role="tabpanel" class="panel-collapse collapse" id="alberto" aria-labelledby="headingAlberto">
    <div class="panel-body">
      <p>...</em></p>
    </div>
  </div>
</div>
```

* After completing the update, check the behavior of the accordion on the web page.

#### Adding Scrollspy with Affix

* First we will adjust the content so that we create some space on the right side of the page to accommodate the nav component for the scrollspy behavior. To do this, we will nest the entire content of the web page into a row first, and move the existing content into a column with a column class of col-sm-10. The remaining two columns will be left for the nav. To do this, add the following code right after the container div:

```
<div class="row">
  <div class="col-xs-12 col-sm-10">  ...
  </div>
</div>
```

* To introduce the scrollspy, we first apply some data-\* attributes to the body of the page as follows:

```
<body data-spy="scroll" data-target="#myScrollspy" data-offset="200">
```

This prepares the body to activate the scrollspy using the _data-spy="scroll"_ attribute. The target of this is set using_data-target="\#myScrollspy"_ thus specifying that the element with the id _myScrollspy_ will act as the scrollspy.

* To introduce the scrollspy with the affix plugin, add the following code to the end of the container, inside the outer row:

```
<nav class="hidden-xs col-sm-2" id="myScrollspy">
  <ul class="nav nav-pills nav-stacked" data-spy="affix" data-offset-top="400">
    <li><a href="#history">Our History</a></li>
    <li><a href="#corporate">Corporate</a></li>
    <li><a href="#facts">Facts</a></li>
  </ul>
</nav>
```

This nav element is introduced with the classes _hidden-xs_ to indicate that this element will be hidden for extra small screen sizes. It will occupy the remaining two columns \(specified through the _col-sm-2_ class\) for the small to large screen sizes. We see that the _nav-pills_ is applied to the _&lt;ul&gt;_ along with _nav-stacked_ to create a vertically stacked nav component. Also the affix plugin is applied to this nav component. The list items use the ids of the three rows. We need to apply the ids to the three rows.

* Apply the appropriate ids for the three content rows as follows:

```
<div id="history" class="row row-content"> ... </div>
<div id="corporate" class="row row-content"> ... </div>
<div id="facts" class="row row-content"> ... </div>
```

* Finally, add the following CSS styles to the mystyles.css file to support the affix:

```
.affix {
  top:100px;
}
```

* Now that all updates are complete, you can now view the web page to see the scrollspy and affix in action.

Here is a good example [BOOTSTRAP 3 SCROLLSPY](http://tutsme-webdesign.info/bootstrap-3-scrollspy/).

Here is another good example, [全局 CSS 样式](http://v3.bootcss.com/css/)。

#### Conclusions

In this exercise we constructed the accordion using the collapse plugin together with the panel components. We also explored the use of scrollspy and affix plugins.

#### Note

**Affix will make it very long time to load the page. \(Seems Javascrip needs a lot of time to go through the whole page content.\)**

## 3.4 Revealing Content: Tooltips, Popovers and Modals

### Bootstrap Resources

* [Bootstrap Tooltips](http://getbootstrap.com/javascript/#tooltips)
* [Bootstrap Popovers](http://getbootstrap.com/javascript/#popovers)
* [Bootstrap Modals](http://getbootstrap.com/javascript/#modals)

### Exercise \(Instructions\): Tooltips and Modals

#### Objectives and Outcomes

In this exercise we will examine how to add tooltips to a web page. In addition we look at adding modals to a web page. At the end of this exercise, you will be able to:

* Add tooltips to a web page
* Add modals that are revealed when the user clicks on a link or a button in the web page.

#### Adding a Tooltip

* Let us now switch to the _index.html_ page. We will now add a tooltip to this page. The tooltip will be added to the "Reserve Table" button that is in the jumbotron. We will update the _&lt;a&gt;_ tag for the button as follows:

```
<a type="button" class="btn btn-warning btn-block" data-toggle="tooltip" title="Or Call us at +852 12345678" data-placement="bottom" href="#reserveform">
```

As you can see from the code, we add a _data-toggle_, _data-placement_ and a _title_ attribute to the &lt;a&gt; tag in order to introduce a tooltip.

* The tooltip needs to be activated by adding a small Javascript code to the bottom of the page as follows:

```
<script>
  $(document).ready(function(){
  $('[data-toggle="tooltip"]').tooltip();
  });
</script>

```

This script is added right after the line that imports the bootstrap.min.js file.

#### Adding a Modal

* In the next step we introduce the modal to the web page. First we introduce the code for the modal and then shift the code for the form from the navbar into the modal body. To set up the modal, add the following code right after the navbar at the top of the page.

```
<div id="loginModal" class="modal fade" role="dialog">
  <div class="modal-dialog">
    <!-- Modal content-->
    <div class="modal-content">
      <div class="modal-header">
        <button type="button" class="close" data-dismiss="modal">&times;</button>
        <h4 class="modal-title">Login </h4>
      </div>
      <div class="modal-body">
        ...
      </div>
    </div>
  </div>
</div>
```

* Next, move the code for the login form from the navbar into the modal body. Then update the form class to _form-inline_. You should already have the code for the form from the previous module.
* Next, introduce another button into the form right after the sign-in button. The new button will enable us to dismiss the modal. The corresponding code is given below:

```
<button type="button" class="btn btn-default btn-sm" data-dismiss="modal">Cancel</button>
```

* Next we introduce another link on the right side of the navbar in order to trigger the display of the modal. To do this, add the following code in the navbar:

```
<ul class="nav navbar-nav navbar-right">
  <li>
    <a data-toggle="modal" data-target="#loginModal">
      <span class="glyphicon glyphicon-log-in"></span>
      Login
    </a>
  </li>
</ul>
```

We are introducing another link to the right of the navbar using the _&lt;ul&gt;_ with the _nav, navbar-nav_ and _navbar-right\_classes. This contains a list item with an _&lt;a&gt;_ tag with the \_data-toggle="modal"_ and \_data-target="\#loginModal"\_attributes.

#### Conclusions

In this exercise we explored tooltips and modals as two ways of revealing content for the user upon clicking on a button or a link.

## 3.5 Carousel

### Bootstrap Resources

* [Bootstrap Carousel](http://getbootstrap.com/javascript/#carousel)

### Exercise \(Instructions\): Carousel

#### Objectives and Outcomes

In this exercise we will examine the carousel component and add it to the web page. We will examine the configuration of the carousel and adding controls to the carousel. At the end of this exercise you will be able to:

* Use a carousel component in your web page
* Configure various aspects of the carousel
* Add controls to the carousel to manually control it

#### Adding a row for the carousel

* The carousel will be added to the \_index.html \_page. In this page, go to the top of the container div that contains the content of the page and add a new content row and an inner div spanning all the 12 columns as follows:

```
<div class="row row-content">
  <div class="col-xs-12">
    ...
  </div>
</div>
```

#### Adding a Carousel

* Next, add the basic carousel div inside the content row that you just added as follows:

```
<div id="mycarousel" class="carousel slide" data-ride="carousel">
  ...
</div>
```

#### Adding Carousel Content

* Next add the content inside the carousel as follows:

```
<!-- Wrapper for slides -->
  <div class="carousel-inner" role="listbox">
    <div class="item active">
      <img class="img-responsive" src="img/uthappizza.png" alt="Uthappizza">
      <div class="carousel-caption">
      <h2>Uthappizza 
        <span class="label label-danger">Hot</span>
        <span class="badge">$4.99</span>
      </h2>
      <p>A unique combination of Indian Uthappam (pancake) and Italian pizza, topped with Cerignola olives, ripe vine cherry tomatoes, Vidalia onion, Guntur chillies and Buffalo Paneer.</p>
      <p><a class="btn btn-primary btn-xs" href="#">More &raquo;</a></p>
    </div>
  </div>
  <div class="item">
    ...
    <div class="carousel-caption">
      <h2>Weekend Grand Buffet <span class="label label-danger label-xs">New</span></h2>
      ...
    </div>
  </div>
  <div class="item">
    ...
    <div class="carousel-caption">
    ...
    </div>
  </div>
</div>
```

Note that the first item has been set up already. For the remaining two items, copy the content from the second and third rows in a similar manner.

#### Adding CSS Classes

* Add the following CSS classes to the _mystyles.css_ file:

```
.carousel {
  background:#1A237E;
}
.carousel .item {
  height: 300px;
}
.item img {
  position: absolute;
  top: 0;
  left: 0;
  min-height: 300px;
}
```

#### Adding Carousel Controls

* Next, we will add manual controls to the carousel so that we can manually move among the slides. Add the following code to the top of the carousel to add slide indicators that enable us to select a specific slide:

```
<!-- Indicators -->
<ol class="carousel-indicators">
  <li data-target="#mycarousel" data-slide-to="0" class="active"></li>
  <li data-target="#mycarousel" data-slide-to="1"></li>
  <li data-target="#mycarousel" data-slide-to="2"></li>
</ol>
```

* Then, add the left and right controls to the carousel that enable us to move to the previous and next slide manually. Add this to the bottom of the carousel div:

```
<!-- Controls -->
<a class="left carousel-control" href="#mycarousel" role="button" data-slide="prev">
  <span class="glyphicon glyphicon-chevron-left" aria-hidden="true"></span>
  <span class="sr-only">Previous</span>
</a>
<a class="right carousel-control" href="#mycarousel" role="button" data-slide="next">
  <span class="glyphicon glyphicon-chevron-right" aria-hidden="true"></span>
  <span class="sr-only">Next</span>
</a>
```

#### Conclusions

In this exercise we learnt about the carousel component and how to add it to a web page. We also learnt about introducing manual controls to the carousel.

## 3.6 Assignment 3: Additional Resources

### Bootstrap Resources

* [Bootstrap Buttons Checkbox\/Radio](http://getbootstrap.com/javascript/#buttons-checkbox-radio)
* [Bootstrap Modals](http://getbootstrap.com/javascript/#modals)
* [Bootstrap Forms](http://getbootstrap.com/css/#forms)

