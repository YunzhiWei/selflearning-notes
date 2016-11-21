# **1 Learning JS in This Course**

## **1.1 阅读: **Module outcomes

## **1.2 视频: **Learning JavaScript

## **1.3 阅读: **Presentation Notes and Examples for Week 2

# 2 Introduction to JS

## **2.1 视频: **About JavaScript

## **2.2 视频: **Getting To Know JavaScript

### JS Functions

* alert\(\)

  > show text to the user

* prompt\(\)

  > display a popup box with a message, along with an OK and Cancel button
  > get user's input

* confirm\(\)

  > Similiar with prompt


### Where to put the JS code

* common practice

```
<!DOCTYPE html>
<html>
  <head>
    ... load JS libraries here ...
  </head>
  <body>
    ...
    ... your JS code typically goes at the end of the body ...
  </body>
<html>
```

* Example

```
<script>
function surprise() {
  alert("Hello!");
}
</script>
```

* Put JS Code in another File

HTML

```
<script src="mycode.js"></script>
```

JS file

```
function surprise() {
  alert("Hello!");
}
```

### Redirect to another web page

```
<!doctype html>
<html>
  <head>
    <title>Example of confirm()</title>
    <script>
      if (confirm("Want to go to Disneyland?"))
        document.location.href="http://park.hongkongdisneyland.com";
    </script>
  </head>
</html>
```

### Variables

```
var totalCost = 7000;
```

### Simple Text Input - prompt\(\) and write content to web page

```
<!doctype html>
<html>
  <head>
    <title>Example of prompt()</title>
    <script>
      var user_name;
      user_name=prompt("What is your name?");
      document.write("Welcome to my page" + user_name + "!" );
    </script>
  </head>
</html>
```

## **2.3 视频: **Using A Code Editor For JavaScript

# 3 Basic of JS

## **3.1 视频: **Variables

### var and typeof

* Data Types

  * Number

    * JS has ONLY ONE type of number \(for both integer and float\)
    * Can use scientific notation

    ```
    var number1 = 34.12;
    var number2 = 1234;
    var big_num = 123e5;     // 12300000
    var small_num = 123e-5;  // 0.00123
    ```

  * String

    * Single or double quotes
    * quotes inside a string is OK

    ```
    var name = "Chris";
    var title = 'CTO';
    var message = "It's OK";  // ' in ""
    ```

  * Boolean

    ```
    var condition1 = true;
    var condition0 = false;
    ```

  * Other e.g. Object



* A Variable's Type Can Be Changed

  ```
  var vvariable = "Chris"; // Type is String
  vvariable = 777;         // Type is changed to number
  ```

* Using Typeof

  ```
  <!doctype html>
  <html>
  <head>
    <title>Variable Type Example</title>
  </head>
  <body>
    <script>
      alert( '"John" is type: ' + typeof "John" + "\n\n"
        + "3.14 is type: " + typeof 3.14 + "\n\n"
        + "false is type: " + typeof false ) ;
    </script>
  </body>
  </html>
  ```


### Common Changes

* count++

* count--

* count += 10

* count -= 10

* count \*= 2

* count \/= 2

* count += "abc"


### Convert from One Type to Another

* parseInt\(\)

  > Converts to an integer

* parseFloat\(\)

  > Converts to a floating point number

* String\(\)

  > Converts the value of an object to a string


## **3.2 视频: **Introduction to Events and Functions

### Events

* onload

  > onload is triggered when the object has loaded

  ```
  <!doctype html>
  <html>
  <body onload="alert('Hello!')">
    <p>A message is shown as soon as the page is loaded.</p>
  </body>
  </html>
  ```

  ```
  <!doctype html>
  <html>
  <body onload="alert('Hello!');
              alert('We start soon...');
              prompt('Excited?!') ">
    <p>3 popup windows are shown as soon as the page is loaded.</p>
  </body>
  </html>
  ```


### Functions

* Example

```
<!doctype html>
<html>
  <head>
    <title>Example of a function</title>
    <script>
      function greet_the_user(){
        alert('Hello!');
        alert('We start soon...');
        prompt('Excited?!')
      }
    </script>
  </head>
  <body onload="greet_the_user()">
  </body>
</html>
```

* Parameters

```
<!doctype html>
<html><body onload="check_user_age()" style="position:absolute">
  <h1>This is my naughty home page.</h1>
  <script>
    function check_user_age(){
      if (age_of_user() < 18) alert("Please go to another page.");
    }
    function age_of_user(){
      var age_text, age;
      age_text=prompt("What is your age?");
      age=parseInt(age_text);
      return age;
    }
</script></body></html>
```

### Recursive Function

**A function can call itself**

```
<!doctype html>
<html><body><script>
  alert("It's my " + build_great(5) + "grandmother!");
  function build_great( depth ) {
    if (depth > 0) return "great " + build_great( depth 1);
    else return "";
  }
</script></body></html>
```

## **3.3 视频: **Handling Bugs

# 4 Decisions and Loops

## **4.1 视频: **Making Decisions

### Syntax

* if

* if ... else ...

* if ... else if ...

* if ... else if ... else

* switch ... case ... default

* &lt;

* &lt;=

* &gt;

* &gt;=

* ==

* !=


### Example

```
<!doctype html>
<html><head><script>
  var user_name;
  user_name=prompt("What is your name?");
  if (user_name == "dave") alert("Great name!");
</script></head></html>
```

```
<!doctype html>
<html><head><script>
  var user_name;
  user_name=prompt("What is your name?");
  if (user_name == "dave") alert("Great name!");
  else alert("Your name isn't great...");
</script></head></html>
```

```
<!doctype html>
<html><head><script>
  var user_name;
  user_name=prompt("What is your name?");
  if (user_name == "dave") alert("Great name!");
  else if (user_name == "jogesh") alert("Pretty good name!");
</script></head></html>
```

```
<!doctype html>
<html><head><script>
  var user_name;
  user_name=prompt("What is your name?");
  if (user_name == "dave") alert("Great name!");
  else if (user_name == "jogesh") alert("Pretty good name!");
  else if (user_name == "oz") alert("Excellent name!");
  else alert("Your name isn't great, never mind...");
</script></head></html>
```

```
<!doctype html>
<html><head><script>
  var user_name=prompt("What is your name?");
  switch(user_name) {
  case "dave":
    alert("Great name!");
  break;
  case "jogesh":
    alert("Pretty good name!");
  break;
  default:
    alert("Your name isn't great, never mind...");
  }
</script></head></html>
```

```
<!doctype html>
<html><head><script>
  var user_name=prompt("What country would you like to visit?");
  switch(user_name) {
  case "Canada":
  case "France":
    alert("Take me also!");
    break;
  case "Japan":
  case "Philippines":
    alert("Great! Have fun!");
    break;
  case "North Korea":
    alert("Oh! Good luck!");
    break;
  default:
    alert("I am sure you will have a great time");
  }
</script></head></html>
```

## **4.2 视频: **While Loops

### Syntax

* while
* do ... while

### indexOf\(\)

```
var text = "The cat's hat was wet";
result = text.indexOf("at");  // result is 5
```

### Example

```
<!doctype html>
<html><head>
  <title>Example of while()</title>
  <script>
    var response, finished;
    finished=false;
    alert("Rossiter is a great name.");
    while (!finished){
      response=prompt("Do you agree?");
      if (response.indexOf("y")==0) finished=true;
    }
  </script>
</head></html>
```

```
<!doctype html>

<html><head>
  <title>Example of do .. while()</title>
  <script>
    var response, finished;
    finished=false;
    alert("Rossiter is a great name.");

    do {
      response=prompt("Do you agree?");
      if (response.indexOf("y")==0) finished=true;
    } while (!finished);
  </script>
</head></html>
```

# 5 Handling Data

## **5.1 视频: **More on Variables

### Local Variables

Variables declared within a function, can only be accessed within the function

```
<!doctype html>
<html><body><script>
function show_money() {
  var money = 2;
  alert("In the function, the value is: "+ money);
}
money = 99;
alert("In the main part, the value is: "+ money);
show_money();
alert("In the main part, the value is: "+ money);
</script></body></html>
```

### Global Variables

* The opposite of a local variable is a global variable
* Global variables are created in the main part
* They can work inside or outside functions

```
<!doctype html>
<html><body><script>
function show_money() {
  alert("In the function, the value is: "+ money);
}
var money = 99;
alert("In the main part, the value is: "+ money);
show_money();
alert("In the main part, the value is: "+ money);
</script></body></html>
```

### Creating Global Variables inside Functions

If you assign a value to a variable that has not been declared, it will automatically become a global variable.

```
<!doctype html>
<html><body><script>
function show_money() {
  money = 2;
  alert("In the function, the value is: "+ money);
}
show_money();
alert("In the main part, the value is: "+ money);
</script></body></html>
```

## **5.2 视频: **Logical Operators

### Syntax

* Boolean values

  * true
  * false

* Logical Operators

  * &&
  * \|\|
  * !


### Example

```
<html><body><script>
var you_are_rich = false;
var you_have_partner = true;
var you_have_flat = true;
var life_is_fantastic = you_are_rich && you_have_partner && you_have_flat;
alert("life is fantastic is " + life_is_fantastic);
you_are_rich = true;
life_is_fantastic = you_are_rich && you_have_partner && you_have_flat;
alert("life is fantastic is now " + life_is_fantastic);
</script></body></html>
```

```
<!doctype html>
<html><body><script>
var you_are_rich = false;
var you_have_partner = true;
var you_have_flat = false;
var life_is_good = you_are_rich || you_have_partner || you_have_flat;
alert("life is good is " + life_is_good);
you_have_partner = false;
life_is_good = you_are_rich || you_have_partner || you_have_flat;
alert("life is good is now " + life_is_good);
</script></body></html>
```

```
<!doctype html>
<html>
<head>
  <title>Not Operator Example</title>
</head>
<body>
  <script>
    var you_are_male = true;
    var you_are_female = !you_are_male;
    alert("you_are_male is " + you_are_male);
    alert("you_are_female is " + you_are_female);
  </script>
</body>
</html>
```

### ATTENTION!!! - Short-Circuit in AND

* JavaScript is clever
* When it evaluates an And it checks the first input
* If the value is false it knows the result must be false
* So it doesn't bother checking the next input

```
<!doctype html>
<html><body><script>
function first_function() {
  alert("first_function() is running!");
  return true;
}
function second_function() {
  alert("second_function() is running!");  // will be invoked
  return false;
}
var test_function = first_function() && second_function();
</script></body></html>
```

```
<!doctype html>
<html><body><script>
function first_function() {
  alert("first_function() is running!");  // will NOT be invoked

  return true;
}
function second_function() {
  alert("second_function() is running!"); 
  return false;
}
var test_function = second_function() && first_function();
</script></body></html>
```

```
<!doctype html>
<html><body><script>
function first_function() {
  alert("first_function() is running!");
  return true;
}
function second_function() {
  alert("second_function() is running!");  // will NOT be invoked
  return false;
}
var test_function = first_function() || second_function();
</script></body></html>
```

## **5.3 视频: **Arrays

### Syntax

* Creating an Array

  > Create a new array with 3 boxes

  ```
  var pets = ["Dog", "Cat", "Rabbit"];
  ```

  > Create a new array with 10 boxes without any element inside

  ```
  var pets = new Array(10);
  ```

  * You can put anything in an array
  * Any element can be any data type

* \[\]

  > retrive something

  ```
  var pets = ["Dog", "Cat", "Rabbit"];
  alert(pets[2]); // This shows "Rabbit"
  ```

  > change something

  ```
  var pets = ["Dog", "Cat", "Rabbit"];
  pets[2] = "Rabbit";
  // Now pets is ["Dog", "Cat", "Rabbit"]
  ```

* length

  > array size

  ```
  var pets = ["Dog", "Cat", "Rabbit"];
  alert(pets.length); // This shows 3
  ```

* push\(\)

  > **add **a new element to the end

  ```
  var pets = ["Dog", "Cat", "Rabbit"];
  pets.push("Hamster");
  // Now pets is
  // ["Dog", "Cat", "Rabbit", "Hamster"]
  ```

* pop\(\)

  > **remove **an element fromt the end

  ```
  var pets = ["Dog", "Cat", "Rabbit"];
  var result = pets.pop();
  // Now pets is [Dog", "Cat"]
  // result is "Rabbit"
  ```

* shift\(\)

  > **remove **an element fromt the front

  ```
  var pets = ["Dog", "Cat", "Rabbit"];
  var result = pets.shift();
  // Now pets is ["Cat", "Rabbit"]
  // result is "Dog"
  ```

* unshift\(\)

  > **add **a new element to the front

  ```
  var pets = ["Dog", "Cat", "Rabbit"];
  pets.unshift("Hamster");
  // Now pets is
  // ["Hamster", "Dog", "Cat", "Rabbit"]
  ```

* concat\(\)

  > combine two arrays into one

  ```
  var pets = ["Dog", "Cat", "Rabbit", "Hamster"];
  var primes = [2, 3, 5, 7, 11];
  var result = pets.concat(primes);
  // result is ["Dog", "Cat", "Rabbit", "Hamster", 2, 3, 5, 7, 11]
  ```

* join\(\)

  > convert array into string

  ```
  var pets = ["Dog", "Cat", "Rabbit"];
  alert(pets.join(" and "));
  // This shows "Dog and Cat and Rabbit"
  ```

  > separator is by default ","

  ```
  var pets = ["Dog", "Cat", "Rabbit"];
  alert(pets.join());
  // This shows "Dog,Cat,Rabbit"
  ```


## **5.4 练习测验: **Practice Questions on Arrays, While Loops and Boolean Logic

# 6 Generating Random Numbers

## **6.1 视频: **Generating Random Numbers

### Syntax

* Math.random\(\)

  > generate a random number
  > set up the range: \[0, 1\)

  ```
  var random_number = Math.random();
  ```

  ```
random_number = Math.random() * max_value;
  ```

  ```
<!doctype html>
<html><body><script>
var random_number;
random_number = Math.random();
alert( random_number );
</script></body></html>
  ```

  ```
<!doctype html>
<html><body><script>
var random_number;
random_number = Math.random() * 8;
alert("Random number in the range 0 to " + "7.9999999:\n" + random_number );
</script></body></html>
  ```

* Math.floor\(\)
  > throw away the decimal place

  ```
<!doctype html>
<html><body><script>
var random_number;
random_number = Math.random() * 50;
random_number = Math.floor( random_number );
alert("Random number in the range 0 to 49: " + random_number);
</script></body></html>
  ```

# 7 An Example JS Project - Guessing Game

## **7.1 视频: **An Example JavaScript Project

### isNan\(\) example

```
<html>
<head>
  <title>isNaN() Example</title>
</head>
<body><script>
  alert("378 is a number: " + !isNaN(378) +"\n\n" +
  "HKUST is a number: " + !isNaN("HKUST"));
</script></body>
</html>
```

### Project Code

```
function check_guess() {
  if (isNaN(guess_input)) {
    alert("You have not entered a number.\n\n" +
    "Please enter a number in the range 1 to 100.");
    return false;
  }
  if ((guess_input < 1) || (guess_input > 100)) {
    alert("Please enter an integer number in the range 1 to 100.");
    return false;
  }
  if (guess_input > target) {
    alert("Your number is too large!");
    return false;
  }
  if (guess_input < target) {
    alert("Your number is too small!");
    return false;
  }
  alert("You got it! The number was " + target + ".\n\nIt took you " + guesses + " guesses to get the number!");
  return true;
}
```

```
var target;
var guess_input_text;
var guess_input;
var finished = false;
var guesses = 0;

function do_game(){
  var random_number = Math.random() * 100;
  var random_number_integer = Math.floor(random_number);
  target = random_number_integer + 1;
  while (!finished) {
    guess_input_text = prompt("I am thinking of a number "+ "in the range 1 to 100.\n\n"+ "What is the number? ");
    guess_input = parseInt(guess_input_text);
    guesses += 1;
    finished = check_guess();
  }
}
```


# **8 阅读: **Further Resources

Now that you have compled this module, you have a basic understanding of JavaScript. In the next module, you will deepen your understanding further. If you want to have greater appreciation of the topics before moving on to the next module, this is a good place to do that: [W3School JavaScript Tutorial](http://www.w3schools.com/js/default.asp)

If you want to improve your coding style with JavaScript, you may be interested in this: [W3School JavaScript Style Guide and Coding Conventions](http://www.w3schools.com/js/js_conventions.asp)

If you would like more practice on JavaScript programming, you can try these:

* JavaScript exercises [http:\/\/www.ugrad.cs.ubc.ca\/~cs101\/2013W2\/practice-questions\/prejavascriptartlab\/](http://www.ugrad.cs.ubc.ca/~cs101/2013W2/practice-questions/prejavascriptartlab/)
* JavaScript Exercises [http:\/\/www.billpegram.com\/Javascript\/javascript\_exercises.html](http://www.billpegram.com/Javascript/javascript_exercises.html)
* JavaScript Exercises for Beginners [http:\/\/www.jsexercises.com\/](http://www.jsexercises.com/) . Select a topic by clicking on the table of contents shown on the left. Solution code is included.

# 9 Introduction to JS - Assessment Task

## **9.1 视频: **Introduction to JavaScript - Assessment

## **9.2 阅读: **FAQ for Introduction to JavaScript - Assessment

