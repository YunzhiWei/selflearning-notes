# 2 Bootstrap CSS Components

## 2.1 User Input: Buttons and Forms

### Bootstrap Resources

* [Bootstrap Buttons](http://getbootstrap.com/css/#buttons)
* [Bootstrap Button Groups](http://getbootstrap.com/components/#btn-groups)
* [Bootstrap Forms](http://getbootstrap.com/css/#forms)

### Other Useful Resources

* [The Difference Between Anchors, Inputs and Buttons](http://davidwalsh.name/html5-buttons) \(Semantic differences in the usage\)
* [When To Use The Button Element](https://css-tricks.com/use-button-element/) \(The multifaceted button element\)

### Exercise: Buttons and Forms

#### Objectives and Outcomes

In this exercise, we will examine user input for a website through the use of Buttons and Forms support in Bootstrap. At the end of this exercise, you will be able to:

* Create, style and activate buttons in a web page using the button classes
* Design a form using various form elements and style the form using Bootstrap form classes

#### Set up for the Exercise

* Download [_contactus.html_](https://spark-public.s3.amazonaws.com/phoenixassets/web-frameworks/contactus.html) file and move it to the _conFusion_ folder that contains your ongoing website project. This file is already pre-formatted with some content.
* Set up the links in the navigation bars for all the three pages, _index.html, aboutus.html_ and _contactus.html_ so that we can navigate from one to another with ease. We have configured the links in _contactus.html_ appropriately.
* Add glyphicons and font awesome icons to all the links in the navbar. We have already configured for _Home_ and_About_ links. Now add the glyphicon _glyphicon-list-alt_ to the _Menu_ link, and the font awesome icon _fa-envelope-o_ to the _Contact_ link. Do this in all the three html pages in the website. Note that this instruction is brief since you should by now be familiar with doing this step from the previous module.

#### Adding a Button Bar

* We are now going to add content to _contactus.html_ file to learn more about buttons and button bars. Go to the div where we specify "Button group goes here", and replace it with the following code to create a button bar containing three buttons

  ```
  <div class="btn-group" role="group" aria-label="...">
    <a type="button" class="btn btn-primary" href="tel:+85212345678"><i class="fa fa-phone"></i> Call</a>
    <a type="button" class="btn btn-info"><i class="fa fa-skype"></i> Skype</a>
    <a type="button" class="btn btn-success" href="mailto:confusion@food.net"><i class="fa fa-envelope-o"></i> Email</a>  </div>
  ```


Note how we define the button bar using the _btn-group_ class, and then add the three buttons using the _&lt;a&gt;_ tag. In this case, the three buttons are hyperlinks that cause an action and have an _href_ associated with them. So we decided to use the _&lt;a&gt;_ tag instead of the _&lt;button&gt;_ tag. Note how the _&lt;a&gt;_ tags have been styled using the _btn_ class.

#### Adding a Basic Form

* Next, we will add a simple form to the page at the location identified by "Form goes here". Add the following code to page to create a simple horizontal form with two fields:

  ```
    <form class="form-horizontal" role="form">
      <div class="form-group">
        <label for="firstname" class="col-sm-2 control-label">First Name</label> 
        <div class="col-sm-10">
          <input type="text" class="form-control" id="firstname" name="firstname" placeholder="Enter First Name">
        </div>
      </div>
      <div class="form-group">
        <label for="lastname" class="col-sm-2 control-label">Last Name</label>
        <div class="col-sm-10">
          <input type="text" class="form-control" id="lastname" name="lastname" placeholder="Enter Last Name">
        </div>
      </div>
    </form>
  ```


This creates a form with two elements in the form. Note that the class _form-group_ acts as a row in the Bootstrap grid system. Hence we can style the contents using the column classes as appropriate.

#### Adding a Input Group with addons

* We now see the use of an input-group together with input-group-addons. Let us add fields to seek user's telephone number and email:

  ```
    <div class="form-group">
      <label for="telnum" class="col-xs-12 col-sm-2 control-label">Contact Tel.</label>
      <div class="col-xs-5 col-sm-4 col-md-3">
        <div class="input-group">
          <div class="input-group-addon">(</div>
          <input type="tel" class="form-control" id="areacode" name="areacode" placeholder="Area code">
          <div class="input-group-addon">)</div>
        </div>
      </div>
      <div class="col-xs-7 col-sm-6 col-md-7">
        <input type="tel" class="form-control" id="telnum" name="telnum" placeholder="Tel. number">
      </div>
    </div>
    <div class="form-group">
      <label for="emailid" class="col-sm-2 control-label">Email</label>
      <div class="col-sm-10">
        <input type="email" class="form-control" id="emailid" name="emailid" placeholder="Email">
      </div>
    </div>
  ```


Note the use of the _input-group_ and _input-group-addon_ classes.

#### Adding a Checkbox and Select

* We now see the addition of a checkbox and a select element to the form. Note the styling of these elements using Bootstrap classes:

  ```
    <div class="form-group">
      <div class="checkbox col-sm-5 col-sm-offset-2">
        <label class="checkbox-inline">
          <input type="checkbox" name="approve" value="">
          <strong>May we contact you?</strong>
        </label>
      </div>
      <div class="col-sm-3 col-sm-offset-1">
        <select class="form-control">
          <option>Tel.</option>
          <option>Email</option>
        </select>
      </div>
    </div>
  ```


#### Adding a textarea

* Next we add a textarea for the users to submit their feedback comments as follows:

```
    <div class="form-group">
      <label for="feedback" class="col-sm-2 control-label">Your Feedback</label>
      <div class="col-sm-10">
        <textarea class="form-control" id="feedback" name="feedback" rows="12"></textarea>
      </div>
    </div>
```

#### Adding the Submit Button

* Finally, we add the submit button to the form as follows:

```
    <div class="form-group">
      <div class="col-sm-offset-2 col-sm-10">
        <button type="submit" class="btn btn-primary">Send Feedback</button>
      </div>
    </div>
```

Note the declaration of the type for the button to _submit_.

#### Conclusions

We have learnt how to add buttons and button groups to a web page. We also learnt how to add a form and style the form using Bootstrap form classes.

## 2.2 Display Content: Tables, Panels, Wells

### Bootstrap Classes

* [Bootstrap Tables](http://getbootstrap.com/css/#tables)
* [Bootstrap Panels](http://getbootstrap.com/components/#panels)
* [Bootstrap Wells](http://getbootstrap.com/components/#wells)
* [Bootstrap Blockquote](http://getbootstrap.com/css/#type-blockquotes)

### Exercise \(Instructions\): Displaying Content: Tables, Panels and Wells

#### Objectives and Outcomes

In this exercise, we will examine tables and Bootstrap classes for styling tables. We will also examine two Bootstrap components: Panels and Wells and their use for displaying content. At the end of this exercise, you will be able to:

* Create, style and present tabular data in tables in a web page using the Bootstrap table classes
* Display content in a web page using Panels and Wells using Bootstrap Panel and Well classes

#### Set up for the Exercise

* In this exercise we will be modifying the _aboutus.html_ page to add a table, a panel with some content and a well with a quotation.
* Let us get started by opening _aboutus.html_ page in a text editor.

#### Bootstrap Tables

* In this part, we will add a new row of content after the Corparate Leadership row in the page. We first start by adding a row and columns to the page as follows:

```
    <div class="row row-content">
      <div class="col-xs-12 col-sm-9">
        <h2>Facts &amp; Figures</h2>
      </div>
      <div class="col-xs-12 col-sm-3">
        <p style="padding:20px;"></p>
      </div>
    </div>
```

* Inside the first column of this row, insert the table as follows:

```
  <div class="table-responsive">
    <table class="table table-striped">
      <tr>
        <td>&nbsp;</td>
        <th>2013</th>
        <th>2014</th>
        <th>2015</th>
      </tr>
      <tr>
        <th>Employees</th>
        <td>15</td>
        <td>30</td>
        <td>40</td>
      </tr>
      <tr>
        <th>Guests Served</th>
        <td>15000</td>
        <td>45000</td>
        <td>100,000</td>
      </tr>
      <tr>
        <th>Special Events</th>
        <td>3</td>
        <td>20</td>
        <td>45</td>
      </tr>
      <tr>
        <th>Annual Turnover</th>
        <td>$251,325</td>
        <td>$1,250,375</td>
        <td>~$3,000,000</td>
      </tr>
    </table>
  </div>
```

Note the use of _table-responsive_ class to create a responsive table, and the _table-striped_ class for styling the table.

#### Bootstrap Panel

* Before we proceed we adjust the column classes for the two columns in the first content row to be _col-sm-8_ and _col-sm-4_ respectively so that the two divs span 8 and 4 columns respectively.
* Next we add a panel to the second div in the first content row as follows:\`

```
    <div class="panel panel-primary">
      <div class="panel-heading">
        <h3 class="panel-title">Facts At a Glance</h3>
      </div>
      <div class="panel-body">
        <dl class="dl-horizontal">
          <dt>Started</dt>
          <dd>3 Feb. 2013</dd>
          <dt>Major Stake Holder</dt>
          <dd>HK Fine Foods Inc.</dd>
          <dt>Last Year's Turnover</dt>
          <dd>$1,250,375</dd>
          <dt>Employees</dt>
          <dd>40</dd>
        </dl>
      </div>
    </div>
```

Note the use of the _panel_ and _panel-primary_ classes to style the panel. The panel contains two divs, one with_panel-heading \_class to host the heading of the panel, and the second with the \_panel-body_ class to host the content. Note the use of _&lt;dl&gt;_ tag with the _dl-horizontal_ class to create a horizontal description list.

#### Bootstrap Well

* Next, we add a Bootstrap well component and include a quotation in the well using the blockquote typography style:

```
    <div class="well">
      <blockquote>
        <p>You better cut the pizza in four pieces because
            I'm not hungry enough to eat six.</p>
        <footer>Yogi Berra,
          <cite>The Wit and Wisdom of Yogi Berra,
 P. Pepe, Diversion Books, 2014</cite>
        </footer>
      </blockquote>
    </div>
```

Note the use of the _&lt;blockquote&gt;_ tag to create a block quote in the well. We can use a _&lt;footer&gt;_ inside the block quote to specify the attribution of the quote to its origin.

#### Conclusions

In this exercise, we constructed a table and styled it with the Bootstrap table classes. Thereafter, we added two components, a panel and a well to the web page. We also saw the use of the description list and the block quote in the content.

## 2.3 Images and Media: Images, Thumbnails, Media Objects

### Bootstrap Resources

* [Bootstrap Image Classes](http://getbootstrap.com/css/#images)
* [Bootstrap Thumbnail Classes](http://getbootstrap.com/components/#thumbnails)
* [Bootstrap Media Object Classes](http://getbootstrap.com/components/#media)
* [Bootstrap Responsive Embed Classes](http://getbootstrap.com/components/#responsive-embed)

### Exercise \(Instructions\): Images and Media

#### Objectives and Outcomes

In this exercise, we will explore the Bootstrap classes to support image and media on a website. In particular, we will look at how to include images on a website, how to make use of images within a media objects. At the end of this exercise you will be able to:

* Use Bootstrap classes to include a responsive images in a website
* Use a media object to include images and description on a website

#### Set up for the Exercise

* Download the [img.zip](https://spark-public.s3.amazonaws.com/phoenixassets/web-frameworks/img.zip) file that we provide and unzip it in the _conFusion_ folder. This should create a folder named_img_ there.
* We will now update the _index.html_ file to include images and media objects on the web page.

#### Adding the Restaurant Logo

* We will now add the restaurant logo to the Jumbotron. In index.html go to the header row inside the jumbotron and replace the second &lt;div&gt; column with the following code:

```
  <div class="col-xs-12 col-sm-2">
    <p style="padding:20px;"></p>
    <img src="img/logo.png" class="img-responsive">
  </div>
```

You will immediately notice the restaurant logo being displayed in the jumbotron.

* Next, we will add the logo to the navbar where we display the restaurant brand. Go to the navbar and replace the code there for the &lt;a&gt; tag with the "navbar-brand" class with the following code:

```
  <a class="navbar-brand" href="#"><img src="img/logo.png" height=30 width=41></a>
```

Note the inclusion of the logo in the navbar.

* Repeat the above two steps for the _aboutus.html_ and the _contactus.html_ page also to update their navbars and jumbotrons.

### Adding Media Objects

* Next we will work with the content on the web page and use the media object classes to style the content in the content rows.
* Go to the first content row, and replace the content in the second column containing the description of Uthappizza with the following code:

```
  <div class="media">
    <div class="media-left media-middle">
      <a href="#">
        <img class="media-object img-thumbnail" src="img/uthappizza.png" alt="Uthappizza">
      </a>
    </div>
    <div class="media-body">
      <h2 class="media-heading">Uthappizza</h2>
      <p>A unique combination of Indian Uthappam (pancake) and Italian pizza, topped with Cerignola olives, ripe vine cherry tomatoes, Vidalia onion, Guntur chillies and Buffalo Paneer.</p>
      <p><a class="btn btn-primary btn-xs" href="#">More &raquo;</a></p>
    </div>
  </div>
```

Note the use of the _media_ class and the related Bootstrap classes to style the content. Also, note the application of the button classes to the _more_ link to turn it into a button.

* Next, we will go to the third row and replace the contents of the second column containing the description about Alberto with the following content:

```
  <div class="media">
    <div class="media-left media-middle">
      <a href="#">
        <img class="media-object img-thumbnail" src="img/alberto.png" alt="Alberto Somayya">
      </a>
    </div>
    <div class="media-body">
      <h2 class="media-heading">Alberto Somayya</h2>
      <h4>Executive Chef</h4>
      <p>Award winning three-star Michelin chef with wide International experience having worked closely with whos-who in the culinary world, he specializes in creating mouthwatering Indo-Italian usion experiences. </p>
      <p><a class="btn btn-primary btn-xs" href="#">More &raquo;</a></p>
    </div>
  </div>
```

* Finally, update the more link in the second row as follows:

```
  <p><a class="btn btn-primary btn-xs" href="#">More &raquo;</a></p>
```

### Conclusions

In this exercise, we learnt about the Bootstrap classes to support images and media in a web page. We saw how we can include responsive images on a web page. In addition, we saw the use of images within a media object to style and display content.

### Adding Media Objects

* Next we will work with the content on the web page and use the media object classes to style the content in the content rows.
* Go to the first content row, and replace the content in the second column containing the description of Uthappizza with the following code:

## 2.4 Alerting Users: Labels, Badges, Alerts, Progress Bars

### Bootstrap Resources

* [Bootstrap Labels](http://getbootstrap.com/components/#labels)
* [Bootstrap Badges](http://getbootstrap.com/components/#badges)
* [Bootstrap Alerts](http://getbootstrap.com/components/#alerts)
* [Bootstrap Progress Bars](http://getbootstrap.com/components/#progress)

### Exercise \(Instructions\): Alerting Users

#### Objectives and Outcomes

In this short exercise we will examine the use of labels and badges as a way of alerting users. At the end of this exercise, you will be able to:

* Add a label to your web page using the Bootstrap label class
* Add a badge to your website using the Bootstrap badge class.

#### Adding a Label

* We will continue to edit the _index.html_ file. In this file, we will add a label _HOT_ next to the name of the dish Uthappizza in the first content row. To do this, add the following code inside the _&lt;h2&gt;_ containing the name of the dish:

  ```
  <span class="label label-danger">Hot</span>
  ```


#### Adding a Badge

* Next we will add a badge right next to the label in the web page. Add the following code to the _&lt;h2&gt;_ tag:

```
  <span class="badge">$4.99</span>
```

#### Conclusions

In this short exercise, we learnt how to add labels and badges to our web page.

## 2.5 Assignment 2: Additional Resources

### Bootstrap Resources

* [Bootstrap Navbar Forms](http://getbootstrap.com/components/#navbar-forms)
* [Bootstrap Dismissible Alerts](http://getbootstrap.com/components/#alerts-dismissible)
* [Bootstrap Forms with Optional Icons](http://getbootstrap.com/css/#forms-control-validation)


