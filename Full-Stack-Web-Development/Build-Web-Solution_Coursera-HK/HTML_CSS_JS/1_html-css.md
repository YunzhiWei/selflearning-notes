# 1 Welcom

## **1.1 视频: **Introduction to the Course

## **1.2 视频: **Full Stack Web Development Specialization

## **1.3 阅读: **Module outcomes

## **1.4 视频: **Learning About HTML

## **1.5 阅读: **Presentation Notes and Examples for Week 1

# 2 The Basic of HTML

## **2.1 视频: **About HTML

### Example List of Elements

* &lt;div&gt;

  > For large area

* &lt;span&gt;

  > For a few words


### Example List of Style Properties

* font-size

* font-family

* background

* align

* width

* position

* top

* left


### An Alternative to HTML

* SVG

  > Graphics approch, few libraries

* HTML

  > Text approach, many libraries


## **2.2 视频: **Getting to Know HTML

### HTML Elements

* Structure

  * &lt;html&gt;
  * &lt;head&gt;
  * &lt;body&gt;

* In &lt;head&gt;

  * &lt;meta&gt;
  * &lt;author&gt;
  * &lt;style&gt;
  * &lt;link&gt;
  * &lt;script&gt;
  * &lt;base&gt;
  * ...

* In &lt;body&gt;

  * &lt;h1&gt;
  * &lt;p&gt;
  * ...


### HTML Spec

* [W3C](http://www.w3.org/TR/html5/)

### HTML Commands

HTML commands are called elements.

Most elements have a start tag and an end tag. &lt;p&gt; ... &lt;\/p&gt;

### HTML Structure

```
<!DOCTYPE html>
<html>
<head>
... header elements here ...
</head>
<body>
... main web page content here ...
</body>
</html>
```

### A Very Simple Web Page

```
<!DOCTYPE html>
<html>
<head>
  <title>A simple Web Page</title>
  <meta name="author" content="Chris Wei">
</head>
<body>
  <h1>My Web Page</h1>
  <p>This web page is so awesome!</p>
</body>
</html>
```

### Other Things You Might Use in Head

* Style

```
<style>
  body {background-color:yellow}
</style>
```

* Link

```
<link rel="stylesheet" href="stylerules.css">
```

* Meta Information

```
<meta name="description" content="An example">
<meta name="keywords" content="HTML, CSS, Javascript">
<meta charset="UTF-8">
```

* Script

```
<script>
function surprise() {
  alert("Hello!");
}
</script>

<script src="mycode.js"></script>
```

* The Location of the Main File

```
<base href="http://www.xxxx.com" target="_blank">
```

* Attributes

```
<meta name="author" content="Chris Wei">
<meta name='author' content='Chris Wei'>
```

### 

## **2.3 视频: **Using a Code Editor For HTML

### One HTML Editor

* TinyMCE

## **2.4 视频: **Some Common HTML Elements

### Elements

* Headings

  * &lt;h1&gt;&lt;h2&gt;&lt;h3&gt;&lt;h4&gt;&lt;h5&gt;&lt;h6&gt;

* Sections

  * &lt;section&gt;

* Lists

  * &lt;ul&gt; and &lt;ol&gt; together with &lt;li&gt;


```
<ul>
  <li>1st</li>
  <li>2nd</li>
  <li>3rd</li>
</ul>
```

```
<ol>
 <li>1st</li>
 <li>2nd</li>
 <li>3rd</li>
</ol>
```

```
<ol start="1999">
 <li>1st</li>
 <li>2nd</li>
 <li>3rd</li>
</ol>
```

```
<ol start="1999" reversed>
 <li>1st</li>
 <li>2nd</li>
 <li>3rd</li>
</ol>
```

```
<ol type="A">
 <li>1st</li>
 <li>2nd</li>
 <li>3rd</li>
</ol>
```

* Comments

  * &lt;!-- a comment --&gt;


## **2.5 视频: **Formatting HTML Text

### Font Format

* Italic and Bold

  * &lt;i&gt;&lt;em&gt;&lt;b&gt;&lt;strong&gt;

* Underline

  * &lt;u&gt;

* Big and Small

  * &lt;big&gt;&lt;small&gt;

* Highlighted

  * &lt;mark&gt;

* Subscript and Superscript

  * &lt;sub&gt;&lt;sup&gt;

* Inserted and Deleted

  * &lt;ins&gt;&lt;del&gt;


# 3 Multimedia

## **3.1 视频: **Images

### Image

* &lt;img&gt;

  * src
  * width
  * height


### Example Code

```
<img src="xxxxx.jpg">
```

```
<img src="xxxxx.jpg" width="300" height="300">
```

```
<img src="xxxxx.jpg" width="300">
```

```
<img src="xxxxx.jpg" width="50%">
```

## **3.2 视频: **Audio

### Audio

* &lt;audio&gt;

  * src
  * autoplay
  * controls
  * loop


### Example Code

```
<audio src="xxxxx.mp3"></audio>
```

```
<audio src="xxxxx.map3" autoplay></audio>
```

```
<audio src="xxxxx.mp3" controls></audio>
```

```
<audio src="xxxxx.mp3" autoplay loop></audio>
```

### Consider for Old Browser

Older Browser cannot handle new HTML tags.

```
<this_new_html_tag>
  <p>Sorry, your browser cannot handle <i>this_new_html_tag<i>!</p>
</this_new_html_tag>
```

## **3.3 视频: **Video

### Video

* &lt;video&gt;

  * src
  * autoplay
  * controls
  * loop
  * alt


### Example Code

```
<video src="xxxxx.mp4"></video>
```

```
<video src="xxxxx.mp4" autoplay></video>
```

```
<video src="xxxxx.mp4" controls></video>
```

```
<video src="xxxxx.mp4" autoplay loop></video>
```

```
<video src="xxxxx.mp4" alt="Walking the High Junk Peak trail">
  <p>Sorry, your browser cannot handle <i>video<i> tag!</p>
</video>
```

# 4 Strengthen You Knowkedge of HTML

## **4.1 视频: **Links

### Links

```
<a href="https://www.gmail.com/">gmail</a>
```

```
<a href="https://twitter.com"><img src="twitter_icon.png"></a>
<a href="https://www.facebook.com"><img src="facebook_icon.png"></a>
<a href="https://plus.google.com"><img src="google_plus_icon.png"></a>
```

### A Position within a Page

* Add id="here" to the element you want link to

* Use within the page


```
<a href="#here">Go here</a>
```

* From another page

```
<a href="web_page.html#here">Go here</a>
```

## **4.2 视频: **Void Elements & Breaks

### Handling Breaks

* &lt;br&gt;&lt;wbr&gt;&lt;hr&gt;

### Void Elements

* > Most elements have this structure: &lt;start\_tag&gt; ... &lt;\/end\_tag&gt;
  > Some elements don't have any content. They are called 'void elements'. And they don't have end tag.


### Meta

```
<meta name="author" content="Chris Wei">
```

### Img

```
<img>
```

### Forms

```
<input>
```

### Breaks

```
<br><wbr><hr>
```

## **4.3 视频: **Style and ID

### General Concept

* Information + Style = Visual Output

### 1 CSS File, Multiple Web Page

* The following reference can be used in multiple pages.

```
<link href='main.css' rel='stylesheet' type='text/css'>
```

### Simple CSS File

```
h1 { color:purple }
p { color:blue }
```

### Common Style Properties

* color - for text color

* background - for background color

* font-family - for text fonts

* font-size - for text sizes

* text-align - for text alignment


### Simple Example

```
<html>
  <head>
    <style>
      h1 { color:purple }
      p { color:blue }
    </style>
  </head>
  <body>
    <h1>Head</h1>
    <p> content </p>
  </body>
</html>
```

### Use a Unique ID

```
<html>
  <head>
    <style>
      #rainbowColors {background: grey}
      #red {background: red}
      #orange {background: orange}
      #yellow {background: yellow}
      #green {background: green}
      #blue {background: blue}
      #indigo {background: indigo}
      #violet {background: violet}
    </style>
  </head>
  <body>
    <ul id="rainbowColors">
      <li id="red">Red</li>
      <li id="orange">Orange</li>
      <li id="yellow">Yellow</li>
      <li id="green">Green</li>
      <li id="blue">Blue</li>
      <li id="indigo">Indigo</li>
      <li id="violet">Violet</li>
    </ul>
  </body>
</html>
```

### Use Class

```
<html>
  <head>
    <style>
      .zappy {color:purple; background:yellow}
      .wow {color:blue; background:lightgrey}
    </style>
  </head>
  <body>
    <h1 class="zappy">Head</h1>
    <p class="wow">Violet</p>
  </body>
</html>
```

### Use Multiple Classes

```
<html>
  <head>
    <style>
      .zappy {color:purple}
      .spicy {color:red}
      .wow {background:lime}
      .lol {background:lightgrey}
    </style>
  </head>
  <body>
    <h1 class="zappy">Head</h1>
    <p class="wow">Violet</p>
  </body>
</html>
```

## **4.4 视频: **More on Style

### Inline Style

```
<p style="text-align:right">Welcome.</p> 
```

```
<html>
  <head>
    <style>
      li {background:yellow}
    </style>
  </head>
  <body>
    <ul>
      <li>One</li>
      <li>Two</li>
      <li style="background:purple">Three</li>
      <li>Four</li>
    </ul>
  </body>
</html>
```

### Context Control

```
<html>
  <head>
    <style>
      ul li {background:yellow}
    </style>
  </head>
  <body>
    <ul>
      <li>One</li>
      <li>Two</li>
      <li>Three</li>
      <li>Four</li>
    </ul>
    <ol>
      <li>One</li>
      <li>Two</li>
      <li>Three</li>
      <li>Four</li>
    </ol>
  </body>
</html>
```

### Pseudo-Classes

```
<html>
  <head>
    <style>
      a:link {background:yellow}
      a:visited {background:pink}
      a:hover {background:lightgreen}
      a:active {background:purple}
      li:empty {background:brown}
    </style>
  </head>
  <body>
    <a href="http://www.google.com">Google</a>
    <a href="http://www.cnn.com">CNN</a>
    <a href="http://www.twitter.com">Twitter</a>
    <a href="http://www.facebook.com">Facebook</a>
    <ol>
      <li>One</li>
      <li>Two</li>
      <li>Three</li>
      <li></li>
    </ol>
  </body>
</html>
```

## **4.5 视频: **Tables

### Table Elements

* Structure

  * &lt;table&gt;&lt;thead&gt;&lt;tbody&gt;


* Header

  * &lt;th&gt;

* Body

  * &lt;tr&gt;&lt;td&gt;


```
<table>
  <thead>
    <tr> <th>Skills</th> <th>Difficulty</th> <th>My Level</th> </tr>
  </thead>
  <tbody>
    <tr> <td>HTML</td> <td>Easy</td> <td>Some</td> </tr>
    <tr> <td>CSS</td> <td>Medium</td> <td>A little</td> </tr>
    <tr> <td>JavaScript</td> <td>Hard</td> <td>Zero</td> </tr>
  </tbody>
</table>
```

### Properties

* border

* width

* height

* vertical-align

* padding


```
<html>
  <head>
  <style>
    table, td, th {border:1px solid black; padding:15px}
    td {color:purple}
  </style>
  </head>
  <body>
    <table>
      <tr> <th>Menu</th> <th>Price</th> </tr>
      <tr> <td>Pizza</td> <td>$15</td> </tr>
      <tr> <td>Curry</td> <td>$10</td> </tr>
      <tr> <td>Salmon</td> <td>$12</td> </tr>
    </table>
  </body>
</html>
```

### Class Rules

```
<html>
  <head> <style>
    table, td, th {border:1px solid green; width:50%; text-align:center}
    .profit {text-align:left; background-color:lightblue}
    .zero {text-align:center; background-color:yellow}
    .loss {text-align:right; background-color:red}
  </style> </head>
  <body>
    <table>
      <tr><th>Product</th><th>Income</th><th>Cost</th><th>Difference</th></tr>
      <tr><td>Laptops</td><td>$300</td><td>$100</td><td class="profit">$200</td></tr>
      <tr><td>Stationary</td><td>$150</td><td>$150</td><td class="zero">$0</td></tr>
      <tr><td>Chairs</td><td>$50</td><td>$300</td><td class="loss">$250</td></tr>
    </table>
  </body>
</html>
```

### Position Example

```
<html>
  <head> <style>
    table, td {border:1px solid black; width:80%; height:80%}
    td {width:33.33%; height:33.33%}
    .t {verticalalign:top} .m {verticalalign:middle} .b {verticalalign:bottom}
    .l {textalign:left} .c {textalign:center} .r {textalign:right}
  </style> </head>
  <body>
    <table>
      <tr><td class="t l">1</td><td class="t c">2</td><td class="t r">3</td></tr>
      <tr><td class="m l">4</td><td class="m c">5</td><td class="m r">6</td></tr>
      <tr><td class="b l">7</td><td class="b c">8</td><td class="b r">9</td></tr>
    </table>
  </body>
</html>
```

## **4.6 视频: **Div and Span

### Elements

* Div for large area

  * no default style
  * no default meaning
  * can use it for any purpose
  * can be put anywhere, use position: absolute with top:xxx and left:yyy

* Span for a few words

  * no default style
  * can use it for a few words


### Properties

* font-size
* font-family
* background
* position
* top
* left
* width

### Div

* div

```
<p>This is a paragraph before the div</p>
<div>
  This is a div with no style
</div>
<p>This is a paragraph in the middle</p>
<div style="background:lightblue">
  This is a div with a blue background
</div>
```

* font-xxx

```
<p>This is a paragraph before the div</p>
<div style="background:yellow; font-size:16pt; font-family:courier">
  This is a div with a yellow background
</div>
<p>This is a paragraph in the middle</p>
<div style="background:lightblue; font-size:18pt;font-family:Arial; width:50%">
  This is a div with a blue background
</div>
```

* Absolute Position

```
<div style="background:yellow; fontsize:16pt; fontfamily:courier;position:absolute; top:60px;left:60px">
  This is a div with a yellow background
</div>
<div style="background:lightblue; fontsize:18pt;position:absolute; top:92px; left:80px">
  This is a div with a blue background
</div>
```

* Relative Position

```
<p>This is a paragraph</p>
<div style="background:yellow; fontsize:14pt; fontfamily:courier;position:relative; top:20px;left:20px">
  This is a div with a yellow background
</div>
```

### Span

```
<p>This is not span text <span>but this is</span> and this isn't</p>
<p>This is not span text <span style="background:yellow">but this is</span>and this isn't</p>
```

## **4.7 练习测验: **Practice Questions on CSS

# 5 Handling Forms

## **5.1 视频: **HTML Form Basics

### Elements

* &lt;form&gt;&lt;textarea&gt;&lt;input type="submit"&gt;

### Structure

```
<form action="destination" method="get or post">
  ...
  <input type="submit">
</form>
```

### Destination

* Tell the browser where to submit the form

```
<form action="http://www.server.com/subdirectory/program.php">
```

* If the program is on the same server html file

```
<form action="subdirectory/program.php">
```

* If the program is in the same directory as the html file

```
<form action="program.php">
```

### Get or Post

Get is the default method

### Elements

* Text Area

```
<form>
  <p>Please enter any feedback you have.</p>
  <textarea rows="3" cols="60" name="feedback" >
    Please enter your text here
  </textarea>
</form>
```

* Submit Button

```
<form action="http://ihome.ust.hk/~rossiter/cgibin/show_everything.php" method="get">
  <p>Please enter any feedback you have.</p>
  <textarea rows="3" cols="60" name="feedback" >
    Please enter your text here
  </textarea>
  <br>
  <input type="submit" value="Send">
</form>
```

## **5.2 视频: **More on Forms

### Elements

* &lt;select&gt;&lt;option&gt;

* &lt;input type="text"&gt; &lt;input type="password"&gt; &lt;input type="checkbox"&gt;  &lt;input type="radio"&gt;


### Attributes

* placeholder

  > shows useful text which disappears when the user enters something

* value

  > fixes what is shown at the start

* autofocus

  > sets which field is given focus at the start

* required

  > means this field must be completed


### A Reminder

```
<form action="http://ihome.ust.hk/~rossiter/cgibin/show_everything.php" method="get">
  <p>Please enter any feedback you have.</p>
  <textarea rows="3" cols="60" name="feedback" >
    Please enter your text here
  </textarea>
  <br>
  <input type="submit" value="Send">
</form>
```

### Text, CheckBox, Radio

```
<form>
  Please enter your name. <br>
  <input type="text" name="feedback"> <br> <br>
  Please select each of the following that you have. <br>
  <input type="checkbox" name="items" value="car">Car <br>
  <input type="checkbox" name="items" value="teddy bear">Teddy bear <br>
  <input type="checkbox" name="items" value="toothbrush">Toothbrush <br> <br>
  Please indicate your intelligence level. <br>
  <input type="radio" name="iq" value="high">High <br>
  <input type="radio" name="iq" value="medium" checked>Medium <br>
  <input type="radio" name="iq" value="low">Low <br> <br>
</form>
```

### Password

```
<form>
  <p>What is the secret password?</p>
  <input type="password" name="userpassword"> <br>
  <input type="submit" value="Send">
</form>
```

### Select from a List

```
<form>
  <p>What city would you like to go to?</p>
  <select name="cities">
    <option value="hk">Hong Kong</option>
    <option value="vc">Vancouver</option>
    <option value="sf">San Francisco</option>
  </select>
</form>
```

### Attributes Example

```
<form>
  <p>Please fill in the following information:</p>
  <label for="firstname">First name:</label>
  <input type="text" name="firstname" value="Dave" autofocus>
  <br>
  <label for="lastname">Last name:</label>
  <input type="text" name="lastname" placeholder="Your last name goes here">
  <br>
  <label for="age">Age:</label>
  <input type="text" name="age" required>
  <br>
  <input type="submit" value="Submit">
</form>
```

## **5.3 视频: **Handling File Upload

### Element

* &lt;input type="file"&gt;

### Structure

```
<form action="destination" method="post" enctype="multipart/formdata">
  . . . other form input elements go here, if any . . .
  <input type="file" name="fileToUpload">
  <input type="submit">
</form>
```

### Example

```
<form method="post" enctype="multipart/formdata" action="http://ihome.ust.hk/~rossiter/cgibin/show_everything.php">
  <p>Select the file you want to upload</p>
  <input type="file" name="fileToUpload">
  <p>Press this button to send it</p>
  <input type="submit" value="Upload the file">
</form>
```


## **5.4 视频: **Some New HTML5 Input Elements

### Eletments

* &lt;input type="number"&gt;
* &lt;input type="date"&gt;
* &lt;input type="color"&gt;
* &lt;input type="range"&gt;
* &lt;input type="time"&gt;

### Example

```
<form action="http://ihome.ust.hk/~rossiter/cgibin/show_everything.php">
  <label for="age">Your age:</label>
  <input type="number" min="0" max="99" step="1" value="18" name="age" required><br>
  <label for="birthday">Your birthday:</label>
  <input type="date" name="birthday"><br>
  <label for="wakeup">You want to wake up at:</label>
  <input type="time" name="wakeup"><br>
  <label for="color">Your favorite color:</label>
  <input type="color" name="color"> <br>
  <label for="mood">Your mood:</label>
  Bad <input type="range" min="0" max="100" step="5" value="50" name="mood"> Good<br
  <input type="submit" value="Submit!">
</form>
```


## **5.5 练习测验: **Practice Questions on Forms

# 6 Grouping

## **6.1 视频: **Element Grouping

### Elements

* &lt;fieldset&gt;&lt;legend&gt;

### Example

```
<form>
  <fieldset>
    <legend>Personal Information</legend>
    First name? <input type="text" name="firstName"> <br>
    Last name? <input type="text" name="lastName"> <br>
  </fieldset> <br>
  <fieldset>
    <legend>Favourite Things</legend>
    Favourite cartoon? <input type="text" name="favCartoon"> <br>
    Favourite pizza? <input type="text" name="lastName"> <br>
  </fieldset> <br>
  <input type="submit" value="Send">
</form>
```

```
<div>
  <fieldset>
    <legend>Defeated Enemies</legend>
    Ice Cream Man <br>
    Super Scary Monster <br>
  </fieldset> <br>
  <fieldset>
    <legend>Friends</legend>
    Flower lady<br>
    Amazon Ant 57 <br>
  </fieldset> <br>
</div>
```


# Further Resources

Having completing this module, you have a good understanding of many common HTML elements and CSS style rules. However, only the most common HTML elements and CSS properties have been discussed.

If you want to learn more about the many different HTML elements, you can find a good reference list of all HTML elements here: [W3School HTML Element Reference](http://www.w3schools.com/tags/default.asp)

If you want to learn more CSS properties and usage, there is a good reference site for CSS here: [W3School CSS Reference](http://www.w3schools.com/cssref/default.asp)

# 7 Assessment Task

## 7.1 **视频: **HTML & CSS - Assessment

## 7.2 **阅读: **FAQ for HTML & CSS - Assessment Task

