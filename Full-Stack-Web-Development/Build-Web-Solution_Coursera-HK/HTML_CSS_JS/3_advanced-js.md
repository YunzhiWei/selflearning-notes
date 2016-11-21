# 1 Module Outcomes

## **1.1 阅读: **Module Outcomes

## **1.2 阅读: **Presentation Notes and Examples for Week 3

# 2 More on Loops

## 2.1 **视频: **For Loops

### Syntax

* for

* for ... in

* for ... of


### Example

```
<html><head><script>
var continents=["Australia", "Africa", "Antarctica", "Eurasia", "America"];
var response, count=0;
for (var index=0; index < continents.length;index++) {
  response = confirm("Have you been to " + continents[index] + "?");
  if (response) count++;
}
alert("You have been to " + count + " continents!");
</script></head></html>
```

```
<!doctype html>
<html><head><script>
var continents=["Australia", "Africa", "Antarctica", "Eurasia", "America"];
var response, count=0;
for (var index in continents) {
  response=confirm("Have you been to " + continents[index] + "?");
  if (response) count++;
}
alert("You have been to " + count + " continents!");
</script></head></html>
```

```
<!doctype html>
<html><head>
<title>Example of for in</title>

<script>
var response, count=0;
var onePerson = { initials:"DR", age:40, job:"Professor" };
for (var property in onePerson) {
  alert(property + "=" + onePerson[property]);
}
</script>

</head></html>
```

```
<!doctype html>
<html><head>
<title>Example of for of</title>

<script>
var continents=["Australia", "Africa", "Antarctica", "Eurasia", "America"];
var response, count=0;
for (var continent of continents) {
  response = confirm("Have you been to " + continent + "?");
  if (response) count++;
}
alert("You have been to " + count + " continents!");
</script>
</head></html>
```

## **2.2 视频: **Loop Control

### Syntax

* break
* continue

### Example

```
<!doctype html>
<html><head><script>
var total_amount=0;
while (true) {
  this_amount=prompt("How much in this account?");
  this_amount=parseFloat(this_amount);
  if (this_amount>0) total_amount+=this_amount;
  else break;
}
alert("Your total savings: " + total_amount);
</script></head></html>
```

```
<!doctype html>
<html><head><script>
var year, great_years = [];
for (year = 2014; year <= 2016; year++) {
  correct=confirm(year + " was great for you?")
  if (!correct) continue;
  great_years.push(year)
}
alert("Your great years were: " + great_years);
</script></head></html>
```

# **3 More on Arrays**

## **3.1 视频: **More On Arrays

### Syntax

* sort\(\)

  ```
  var pets = \["Dog", "Cat", "Rabbit", "Hamster"\];
  pets.sort();
  // Now pets is ["Cat", "Dog", "Hamster", "Rabbit"]
  ```

* reverse\(\)

  ```
  var pets = ["Dog", "Cat", "Rabbit", "Hamster"];
  pets.reverse();
  // pets is ["Hamster", "Rabbit", "Cat", "Dog"]
  ```

* Descending Order

  ```
  var pets = ["Dog", "Cat", "Rabbit", "Hamster"];
  pets.sort().reverse();
  // pets is ["Rabbit", "Hamster", "Dog", "Cat"]
  ```

* indexOf\(\) - Finding an Element

  ```
  var pets = ["Dog", "Cat", "Rabbit", "Hamster"];
  alert(pets.indexOf("Rabbit")); // This shows 2
  ```

  > If target is not in the array, indexOf\]\(\) will return -1.
  > 
  > 2nd parameter for indexOf\(\) to control where to start the search

  ```
  array.indexOf(target, startPosition)
  ```

  ```
  <html><body><script>
  var pets = ["Dog", "Cats", "Rabbit", "Hamster", "Rabbit", "Rabbit", "Dog", "Cat", "Hamster", "Hamster", "Rabbit"];
  var rabbitPositions = [], startSearchAt = 0;
  do {
  foundAt = pets.indexOf("Rabbit", startSearchAt);
  if(foundAt != 1) {
   rabbitPositions.push(foundAt);
   startSearchAt = foundAt + 1;
  }
  } while(foundAt != 1);
  alert(rabbitPositions); // This shows [2, 4, 5, 10]
  </script></body></html>
  ```

* lastIndexOf\(\)

  ```
  var pets = ["Rabbit", "Dog", "Cat","Rabbit", "Hamster"];
  alert(pets.lastIndexOf("Rabbit")); // This shows 3
  ```

* slice\(\) - Extract Part of an Array

  * array.slice\(startPosition\)

  ```
  var pets = ["Dog", "Cat", "Rabbit", "Hamster"];
  var result = pets.slice(1);
  // result is ["Cat", "Rabbit", "Hamster"]
  ```

  * array.slice\(startPosition, endPosition\)

  ```
  var pets = ["Dog", "Cat", "Rabbit", "Hamster"];
  var result = pets.slice(1, 3);
  // result is ["Cat", "Rabbit"]
  ```

* splice\(\)

  * Remove Elements - array.splice\(position, quantity\)

  ```
  var pets = ["Dog", "Cat", "Rabbit", "Hamster"];
  var result = pets.splice(1, 1);
  // Now pets is ["Dog", "Rabbit", "Hamster"]
  // and result is ["Cat"]
  ```

  * Add an Element Anywhere - array.splice\(position, 0, element\)

  ```
  var pets = ["Dog", "Cat", "Hamster"];
  var result = pets.splice(2, 0, "Rabbit");
  // Now pets is ["Dog", "Cat", "Rabbit", "Hamster"]
  // and result is [], because nothing is removed
  ```

  * Replace an Element Anywhere - array.splice\(position, quantity, elements\)

  ```
  var pets = ["Dog", "Cat", "Hamster"];
  var result = pets.splice(1, 1, "Rabbit", "Fish");
  // Now pets is ["Dog", "Rabbit", "Fish", "Hamster"]
  // and result is ["Cat"]
  ```


## **3.2 视频: **Array Functions

### Syntax

* forEAch\(\)

  * without forEach

  ```
  var pets = ["Dog", "Cat", "Hamster"];
  for(var i = 0; i < pets.length; i++) {
  alert(pets[i]);
  }
  ```

  * with forEach

  ```
  var pets = ["Dog", "Cat", "Rabbit"];
  pets.forEach(alert);
  // This shows 3 separate alerts
  ```

  > You may think of forEach in this way

  ```
  function forEach(theArray, fn) {
  for(var i = 0; i < theArray.length; i++) {
    fn(theArray[i], i, theArray);
  }
  }
  ```

  > Your function should be look like this

  ```
  function yourFunction(element, index, array) {}
  ```

  ```
  <!doctype html>
  <html><body><script>
  var numbers = [1, 2, 3, 4, 5];
  numbers.forEach( function(elem, idx, arr) {
  arr[idx] = elem * elem;
  });
  alert(numbers); // This shows [1,4,9,16,25];
  </script></body></html>
  ```

* map\(\)

  > map\(function\) stores the result of each execution of function into an array it returns
  > 
  > You can think of map\(\) in this way

  ```
  function map(theArray, fn) {
  var results = [];
  for(var i = 0; i < theArray.length; i++) {
    results.push(fn(theArray[i], i, theArray));
  }
  return results;
  }
  ```

  ```
  <!doctype html>
  <html><body><script>
  var square = function(el) { return el * el; }
  var numbers = [1, 2, 3, 4, 5];
  var results = numbers.map(square);
  alert(results); // This shows [1,4,9,16,25];
  </script></body></html>
  ```


# 4 The DOM \(Document Object Model\)

## **4.1 视频: **The DOM - Basic Concepts

### The DOM

* DOM means Document Object Model
  > when you load something into a browser, it is converted into a DOM structure
  > The following code will be stored in a tree structure


```
<!DOCTYPE html>
<html>
  <head>
    <title>A Simple Web Page</title>
    <meta name="author" content="David Rossiter">
  </head>
  <body>
    <h1>My Web Page</h1>
    <p>This web page is so awesome!</p>
  </body>
</html>
```

* Tree Structure

  * node
  * root
  * parent
  * child
  * sibling
  * branch


### WhiteSpace Nodes

* Whitespace is anything you can't see i.e. spacing
* There may be a text node which contains only whitespace
* These is called a 'whitespace node'
* These are sometimes troublesome

> The following code doesn't have a whitespace node between &lt;body&gt; and &lt;p&gt;

```
<body><p>Hello</p></body>
```

> The following code DO have a whitespace node between &lt;body&gt; and &lt;p&gt;

```
<body>
<p>Hello.</p>
```

## **4.2 视频: **Node Relationships

### Node Relationships

* Parent Node

  * parentNode

* Child Node

  * childNotes\[\]
  * firstChild
  * lastChild

* Siblings

  * previousSibling
  * nextSibling


### Code to Find the Path

```
function handleClick(event) {
  event.stopPropagation();
  var node = event.target
  var thisPath = node.nodeName;
  while (node.parentNode) {
    node = node.parentNode;
    thisPath = node.nodeName + " > " + thisPath;
  }
  alert(thisPath);
}
```

> To trigger the code, the user clicks on a node
> To enable this, event handlers are added to the nodes

```
// Register the click event handler for all nodes
function attachHandler(node) {
  if(node == null) return;
  node.onclick = handleClick;
  for (var i = 0; i < node.childNodes.length; ++i) {
    attachHandler(node.childNodes[i]);
  }
}
```

## **4.3 视频: **Locating Nodes

### The DOM

* Everything is in the DOM
* We can add\/delete\/copy\/change anything
* To do this, we need to understand how to access things

### Syntax

* getElementsByTagName\(\)

* getElementById\(\)

* setAttribute\(\)


### How to Access Node? - Using the Exact Path

* Method 1: Use the exact DOM path

  * Sometimes hard to work out the exact path

  * Easy to make mistakes

  * In another browser the DOM may be slightly different - code fails!



* Method 2: Use getElementsByTagName\(\)

  * This requires you to know the exact tag name e.g. is it h2 or h3?

  * There might be several nodes of that type, so you have to know exactly which one it is



* Method 3: Use getElementById\(\)

  * If you give a node a unique name e.g. &lt;element\_name id="thing"&gt; . . . &lt;\/element\_name&gt;, then this method is the easiest way


```
<!DOCTYPE html>
<html>

<head><script>
  function change_color1(){
    document.childNodes[0].childNodes[2].childNodes[1]
      .style.color="red";
  }
  function change_color2(){
    document.getElementsByTagName("h2")[0]
      .style.color="yellow";
  }
  function change_color3(){
    document.getElementById("cute_text").style.color="blue";
  }
</script></head>
<body>
  <h2 style="color:black" id="cute_text">
    Click on a button to change the colour
  </h2>
  <form>
    <input onclick="change_color1()" type="button" value="Change using method 1">
    <input onclick="change_color2()" type="button" value="Change using method 2">
    <input onclick="change_color3()" type="button" value="Change using method 3">
  </form>
</body>

</html>
```

### Set Attributes

```
<!DOCTYPE html>
<html>
<head><script>
function change_color1(){
  document.childNodes[0].childNodes[2].childNodes[1]
    .setAttribute("style", "color:red");
}
function change_color2(){
  document.getElementsByTagName("h2")[0]
    .setAttribute("style", "color:yellow");
}
function change_color3(){
  document.getElementById("cute_text")
    .setAttribute("style", "color:blue");
}
</script></head>
```

## **4.4 视频: **Creating and Adding Nodes

### Syntax

* Creating a node \(first\) \(not in the DOM yet\)

  * createElement\(\)

    ```
    result = document.createElement("div");
    ```

  * createTextNode\(\)

    ```
    result = document.createTextNode("Hello");
    ```



* Adding a node \(second\) \(place the new node in the desired place\)

  * insertBefore\(\)

    ```
    newItem = document.createElement("hr");
    destParent = document.getElementsByTagName("body")[0];
    destParent.insertBefore(newItem, destParent.firstChild);
    ```

  * appendChild\(\)

    ```
    result=document.createTextNode("This is dynamically added Text!");
    document.getElementById("my_text").appendChild(result);
    ```



### Example Code

```
<!DOCTYPE html>
<html>

<head><script>
function insert_new_text() {
  var newItem=document.createElement("hr");
  var destParent=document.getElementsByTagName("body")[0];
  destParent.insertBefore(newItem, destParent.firstChild);
}
</script></head>

<body onclick="insert_new_text()">
  <h1 id="my_text">Please click on the page</h1>
</body>

</html>
```

```
<!DOCTYPE html>
<html>

<head><script>
function insert_new_text() {
  var newText = document.createTextNode("This is dynamically added text!");
  var textpart = document.getElementById("my_text");
  textpart.appendChild(newText);
}
</script></head>

<body onclick="insert_new_text()">
  <h1 id="my_text">Please click on the page</h1>
</body>

</html>
```

## **4.5 视频: **Deleting Nodes

### Syntax

* removeChild\(\)

### Example Code

```
<!DOCTYPE html>
<html>

<head> <script>
function delete1() {
  var the_node=document.getElementById("firstP");
  the_node.parentNode.removeChild(the_node);
}
function delete2() {
  var the_node=document.getElementsByTagName("p")[0];
  the_node.parentNode.removeChild(the_node);
}
function delete3() {
  var the_parent=document.getElementById("theBody");
  the_parent.removeChild(the_parent.firstChild);
}
</script> </head>
<body id="theBody">
  <p id="firstP">Hello.</p>
  How are you?
  <br>
  <p id="secondP">It's a nice day!</p>
  <button type="button" onclick="delete1()">Example 1</button>
  <button type="button" onclick="delete2()">Example 2</button>
  <button type="button" onclick="delete3()">Example 3</button>
  <p>Reload the page to reset the DOM.</p>
</body>

</html>
```

### Delete All Children

```
<!DOCTYPE html>
<html>

<head> <script>
function delete_all_children() {
  var theNode = document.getElementById("theBody");
  while (theNode.firstChild) theNode.removeChild(theNode.firstChild);
}
</script> </head>
<body id="theBody">
  <p id="firstP">Hello.</p>
  How are you?
  <br>
  <p id="secondP">It's a nice day!</p>
  <button type="button" onclick="delete_all_children()">Delete children</button>
</body> </html>
```

## **4.6 视频: **Cloning Nodes

### Syntax

* Copy a Node

  ```
  the_node.cloneNode() // as same as the_node.cloneNode(false)
  ```

* Copy a Branch

  ```
  the_node.cloneNode(true)
  ```

* Adding Nodes

  ```
  dest.appendChild(the_node)
  ```


### Process

1. Copy node\(s\) from the DOM
2. Paste the copied node\(s\) in the DOM

### Example

* A list item node &lt;li&gt; is copied, and then, the new one is pasted to the end of the list

  ```
  <!DOCTYPE html>
  <html>

  <head><script>
  function myFunction() {
    var the_node=document.getElementById("myList").lastChild;  
    var the_clone=the_node.cloneNode();
    document.getElementById("myList").appendChild(the_clone);
  }
  </script></head>

  <body>
    <ul id="myList"><li>Good morning</li><li>Hello</li></ul>
    <p>Click on the button to cloneNode()</p>
    <button onclick="myFunction()">Copy it!</button>
  </body>

  </html>
  ```


* A list item branch &lt;li&gt; with text node child is copied, and then, the new branch is added to the end of the list

  ```
  <!DOCTYPE html>
  <html>

  <head><script>
  function myFunction() {
    var the_node=document.getElementById("myList").lastChild;
    var the_clone=the_node.cloneNode(true);
    document.getElementById("myList").appendChild(the_clone);
  }
  </script><head>

  <body>
    <ul id="myList"><li>Good morning</li><li>Hello</li></ul>
    <p>Click on the button to cloneNode(true)</p>
    <button onclick="myFunction()">Copy it!</button>
  </body>

  </html>
  ```


## **4.7 练习测验: **Practice Questions on DOM

# 5 More on Events

## **5.1 视频: **Mouse Events

### Syntax

* onclick

  > when the user clicks on an object
  > onclick = onmousedown followed by onmouseup

* onmousedown

  > when the user presses down the mouse button

* onmouseup

  > when the user lets go of the mouse button

* onmouseover

  > mouse is moved over an object

* onmouseout

  > mouse is moved away from an object


### Example

```
<html>
<head>
<script>
  function good_choice() { alert("Good choice!"); }
  function bad_choice() { alert("I don't agree!"); }
</script>
</head>
<body>
  <h1>Click on the best social network...</h1>
  <img src="facebook_icon.png" onclick="bad_choice()">
  <img src="google_plus_icon.png" onclick="bad_choice()">
  <img src="twitter_icon.png" onclick="good_choice()">
</body>
</html>
```

```
<html>
<head><script>
  function change_colour( new_colour ) {
    document.getElementById("myDiv").style.background=new_colour;
  }
</script></head>
<body>
  <div id="myDiv" style="position:absolute; background:yellow; left:300; top:100; width:300; fontsize:52pt" onmouseover="change_colour('red');" onmouseout="change_colour('yellow');">
    Move your mouse over this ...
    then move it out...
  </div>
</body>
</html>
```

## **5.2 视频: **Timer Events

### Syntax

* setTimeout

* setInterval

* clearTimeout

* clearInterval


```
var the_timer;
the_timer = setTimeout(do_something, 1000);
```

> do\_something will be executed 1 second later

```
var the_timer;
the_timer = setTimeout(do_something, 1000);
clearTimeout(the_timer);
```

> do\_something will not be executed

```
var the_timer;
the_timer = setInterval(do_something, 2000);
```

> do\_something will be executed every 2 second

```
var the_timer;
the_timer = setTimeout(do_something, 1000);
clearInterval(the_timer);
```

> To stop the repeat timer

### Example

```
<html>
<head><script>
  var wait_duration;
  function set_things_up() {
    wait_duration = prompt("How long do you " + "want to sleep?");
    setTimeout(show_wake_up_message, wait_duration );
  }
  function show_wake_up_message() {
    alert("WAKE UP! WAKE UP! WAKE UP!!");
  }
</script></head>
<body onload="set_things_up()">
  <h1>Alarm clock example</h1>
</body>
</html>
```

```
<html>
<head><script>
  var the_timer, x_position = 0, the_image;
  function set_timer() {
    the_image=document.getElementById("stones_image");
    x_position=x_position+1;
    the_image.style.left=x_position;
    the_timer = setTimeout(set_timer, 50);
  }
</script></head>
<body onload="set_timer()">
  <img src="stones.png" id="stones_image" style="position:absolute; left:0">
</body>
</html>
```

```
<html>
<head><script>
  var the_timer, x_position = 0, the_image;
  function set_timer() {
    the_image = document.getElementById("stones_img");
    x_position = x_position + 1;
    the_image.style.left = x_position;
    the_timer = setTimeout(set_timer, 50); 
  }
</script></head>
<body onload="set_timer()">
  <img src="stones.png" id="stones_img" style="position:absolute; left:0">
  <button onclick="clearTimeout(the_timer)">Stop!</button>
</body>
</html>
```

```
<html>
<head><script>
var the_timer, x_position = 0, the_image;
function do_timer(){
  the_image = document.getElementById("stones_img");
  x_position = x_position + 1;
  the_image.style.left = x_position;
}
</script></head>
<body onload="the_timer=setInterval(do_timer, 50)">
  <img src="stones.png" id="stones_img" style="position:absolute; left:0">
  <button onclick="clearInterval(the_timer)">Stop!</button>
</body></html>
```

## **5.3 视频: **Adding Events Using JavaScript

### Syntax

* addEventListener\(\)

* removeEventListener\(\)


### More than One Handler

* Event handlers are stored in an array
* When an event happens, all the handlers are executed
* They are executed in the order they are added

### Example

* Adding an event to an element in HTML

  ```
  <html>
  <head><script>
  function do_something() {alert("Page has loaded");}
  </script></head>
  <body onload="do_something()"></body>
  </html>
  ```

* Adding an event to an element in JS

  ```
  <html><body id="theBody"><script>
  function do_something() { alert("Page has loaded") }
  window.onload = do_something;
  </script></body></html>
  ```

* Another way

  ```
  <html><body><script>
  function do_something() { alert("Page has loaded") }
  window.addEventListener("load", do_something);
  </script></body></html>
  ```

* Removing an Event Handler

  ```
  <html><body>
  <button id="btn0" onclick=" alert('Hello!') ">Click Me!</button><br>
  <button id="btn1">Remove Listener</button>

  <script>
    function do_something() { alert('Clicked'); }
    var btn0 = document.getElementById("btn0");
    var btn1 = document.getElementById("btn1");
    btn0.addEventListener("click", do_something);
    btn1.addEventListener("click", function() {
      btn0.removeEventListener("click", do_something);
    });
  </script>
  </body></html>
  ```


## **5.4 练习测验: **Practice Questions on Events

# 6 Advanced Use of Functions

## **6.1 视频: **More on Functions

### Passing a Function to a Function

```
<!doctype html>
<html><head><script>

function check(a, b){
  if (b!=0) return true;
  else return false;
}
function myDivide( fn, num, div ) {
  if (fn(num, div)) {
    alert("It's OK!");
    return num/div;
  }
  else {
    alert("Not OK!");
  }
}

result=myDivide(check, 44, 1);

</script></head></html>
```

### Return a Function from a Function

```
<!doctype html>
<html><head><script>

function counter() {
  var count = 0;
  return function() {
    count++;
    alert(count);
  }
}

var count = counter();

count();
count();
count();

</script></head></html>
```

# 7 An Example DOM Project

## **7.1 视频: **An Example DOM Project

# **8 阅读: **Further Resources

Now that you have compled this module, you have a deep understanding of JavaScript. [W3School JavaScript Tutorial](http://www.w3schools.com/js/default.asp) is a good place to fill in any 'missing gaps' from your knowledge.

If you want to improve your coding style with JavaScript, you may be interested in this: [W3School JavaScript Style Guide and Coding Conventions](http://www.w3schools.com/js/js_conventions.asp)

If you would like more practice on JavaScript programming, you can try these:

* JavaScript Exercises [http:\/\/www.billpegram.com\/Javascript\/javascript\_exercises.html](http://www.billpegram.com/Javascript/javascript_exercises.html)
* JavaScript Exercises for Beginners [http:\/\/www.jsexercises.com\/](http://www.jsexercises.com/) . Select a topic by clicking on the table of contents shown on the left. Solution code is included.

If you want to see a complete reference of JavaScript, you can read this: [W3School JavaScript Reference](http://www.w3schools.com/jsref/default.asp)

# 9 Advanced JS - Assessment Task

## **9.1 视频: **Walkthrough Video for Matching Game

## **9.2 阅读: **FAQ for Advanced JavaScript - Assessment Task

# 10 End of Course Message

## **10.1 视频: **Concluding Message

