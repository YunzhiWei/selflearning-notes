# 1. Ruby on Rails: An Introduction

## 1.1 Welcome and Setting Up the Development Environment

### 1.1.1 Github Repository for Module 1

* Each module in the course has a Github repository associated with it. The repository for Module 1 is located [here](https://github.com/jhu-ep-coursera/fullstack-course1-module1).

* You can find PDFs of the Module 1 Lecture slides [here](https://github.com/jhu-ep-coursera/fullstack-course1-module1/tree/master/Slides)

* We have also put together a comprehensive list of FAQs in the repository Wiki [here](https://www.coursera.org/learn/ruby-on-rails-intro/supplement/ZLtzV/github-repository-for-module-1). These are usually questions encountered during assignment completion or common issues encountered during the module. Check them out if you are stuck on something or if you just want to see what interesting questions other students had!


### 1.1.2 Recommended Books

| Title | Author | Description |
| --- | --- | --- |
| Mastering Sublime Text | Dan Peleg | Clear step-by-step instructions on using Sublime Text 3. |
| Pro Git | Scott Chacon, Ben Straub | Great book on Git - the electronic version is available for free [here](https://git-scm.com/book/en/v2). |
| Git in Practice | Mike McQuaid | There is a lot to Git and it can be daunting to get comfortable with. This book helps you get going with Git quickly showing you the what you need to know right away |
| Learn Git in a Month of Lunches | Rick Umali | If you can "get by" the basics of Git, but would love to learn more and do so in a structured fashion - this book is for you. |
| Pragmatic Guide to Git | Travis Swicegood | Another really good book on Git. |

### 1.1.3 Software Installation for Linux Users

* \[MUSIC\] Hello, this is Jim. I'm gonna be going through the software installation for module one on Linux Platforms, more specifically, Ubuntu and Fedora. In order to install **Ruby**, the language interpreter, **Rails**, our web application platform, **PhantomJS** used for headless Web testing support, and **Sublime Text** an optional text editor. I'm gonna be starting with some **Docker Images** and the source for those images are available in the module one repository. We'll be installing Mat'z original, Ruby MRI Interpreter it's based on C. Which means we are gonna be doing a lot of compiling on our Linux platform.

* Prerequisites you must have and Ubuntu or Fedora System, a non-root account with sudo privileges. When we install Ruby we have a decision to make right upfront. And luckily, if we're just going to keep with one version and not do a lot of bouncing around between different interpreters, we probably won't have to touch this layer all that much in the future. However we do have to install it in order to work. The installation manager, what it's responsible for is determining what gems work with what versions of Ruby. Installing different versions at different points in time. Now there are various managers you can install, and there's two, let's say, leading managers. There are others. You have the rvm, which is the older, more established but it's a heavyweight manager, it does some things to the shell that people, purists aren't really thinking of. So in a development environment it may not be an ideal choice by some. **RBENV**, thought to be a lighter weight solution, and it works much through more traditional UNIX pathing. Now when we go to the main Ruby site and click on Download, we get a page that says that we should  be using a package management system. And they suggest **RBENV** or **RVM**. Okay, we'll go to the **RAILS **site, click on download. They're recommending **RBENV**. Okay, choices are a little simpler. And they link over to the Stevenson GitHub, which has the implementation or the installation for how we manage it. Doesn't have all the instructions. Has a good bit. So Google it around on the web, **I found a decent article from Mitchell Atticus, on how to install Ruby on Rails with RBENV on Ubuntu**. Well great, all we have to do is fill in some of the Fedora details. And we'll be coming back to this one, or breaking it down in other instructions. But before we get too far down the RBENV, if you really did want to use the RVM, I found that the Rails girl's website has some decent multi-platform and all kinds of other different ways for Ubuntu and Fedora. But their solution is based on RVM, so what I would suggest is that you don't just run the script, you don't actually open the script up, which is basically what we'll be doing today in procedures that I'm doing and actually look at the overall commands.

* So let's get started going through some of the information that's on **Mitchell's page on how to install Rails with RBENV**. So I go back to my two VMs. I have an Ubuntu on the top in green lettering. I have Fedora on the bottom in the white-on-black lettering. And one of the first things we're gonna do, is, we're going to update the existing packages that are on the system.

* It's something that we should do before we add new packages to it. And as you may know that **Ubuntu** uses **AptGet** as a package manager and **Fedora **uses **Yum**. And what's gonna, what we need to do when we run this package manager is to use the sudo command which is going to want a password and that password is going to be good for a period of time. So on follow on sudo commands. Until that timeout is elapsed, we will be able to just issue the future commands without issue.

* Next, we will install **Git**, and what we're gonna use Git initially for is to clone the **RBNV and Ruby build repositories**. That'll be a part of this installation. And we'll also use Git as a part of class. Both installations took roughly about between one and two minutes to complete.

* Next, we'll install the **compiler and some of the libraries** that it will use in order to build Ruby and the various gems that are out there. That installation probably took us about between three and five minutes. Fedora was a little bit faster what I asked it to do. And Ubuntu, took about the five minute time.

* Next we have two very similar operations on both platforms. And we're going to **clone\/install the rbenv repository**. And so we're going to, in our home directory check out clone from Git. The Stevenson repository and we're going to put that in a directory right below our own. The clone was placed in a directory below the home directory and what we are gonna do is use **environment variables**, a path variable, in order to point to that location. While we're on the topic of environment variables, let me make a slight side bar to describe what they're about. Let's say there's some text, recipepuppy.com running at port 80. And we don't want to hard code that in our application and we want to necessarily make a variable reference. But what we can do, is we can export that into our shell and assign it a value. And, we can make it a little more permanent if we put it into our bashrc. So, I am gonna to echo that, so that it goes into the bashrc. And if we do a tail on the **bashrc**, we'll see that it's at the very end. So what we'll do then is we will source bashrc in order to get that environment variable declared. And then what we can do is we can use that environment variable, let's say to bring up Chrome to launch that display. And as we see in our browsers sitting in the background, they are busily bringing up the actual website that the variable points to. So to get RV into our path, we're going to have to declare a variable that references the bin directory. And we do that through the same mechanism. We'll just extend our path in bashrc. We will source. Our bashrc. We will source our bashrc. And, at this point in time, rbenv should be in our path. There's another piece of environment information that gets added, which is this rb init. And what it does is it adds some command completion scripts. It gets those into your path as well, so that you can complete partial commands that you issued to Ruby. Once that's been in place, probably ought to just source it to be able to get what we just put in, into our shell.

* The next thing that we bring in is ruby-build, and ruby-build, it gives us the ability to actually install ruby inside of rbenv. It's going to be installed below home, below rbenv in a plugins directory. And like before it, that plugins directory needs to also be in your path, so let's go ahead and add that to the bashrc. Let's source our bashrc in both areas. Now, here's the step we've been looking for. This is where we're actually going to install Ruby. It's a lengthy step, and you'll notice, there's a lot of compilations that'll go on. You can pretty much bet that this is gonna be about a **20 to 30 minute** install. So, make sure you get this command in, and then go ahead and go find a cup of coffee and a sandwich while it finishes up. If there are any errors or stoppages in it, it's more than likely that you're missing a package or two, and so maybe you didn't have the same starting point I did. Pretty much if you grab the error, Google it, you'll have an easy time at finding out what package maybe your system didn't have that mine already did have, and I didn't have to install it as a part of these installation instructions. Okay, that was just under 30 minutes. Hopefully you had a good lunch.

* The next thing we'll do, is we will set the default version of Ruby to be used from this point forward. We've got it installed so we might as well use it. So we're gonna be using 2.2.2 with this installation. One of the options I suggest
  we set is to tell the gems to not generate local documentation. It'll just eat up disk space and time when they're downloading. And we'll just put that into a gemrc file. Next, we want to bring in the Rails Gem Manager. This will do a lot of the heavy lifting for us as we start putting gems into our applications. You'll hear a lot more about that later but just right now all we have to do is install it. Now here's another interesting step.

* Rails 4.2.3

  Now we're going to be installing the rails now and we're going to be selecting specifically the 4.2.3 version which will be what we'll be base lining in class. This is another lengthy step, not as long as the Ruby install. It's about about a five-minute one, so all you have time to do is get a new cup of coffee for this one. So, come back when it's done. Okay, that wasn't so bad, that was about three to four minutes. And now we have our rails installed. After installing rails, what they suggest is after installing any gem that adds commands, that we do a **rehash** on rbenv. And where that it can reread all the different shims so that we can get command completion in whatever we're trying to type, related to Rails. Next, we're gonna install one of the JavaScript libraries that can be used in class, and here's where we need to catch Ubuntu up on some unique instructions. So I'm going to install a couple of packages that it needs in order
  to get everything ready. I'm also going to install a custom location for it to bring in the packages. Custom location is at chris-lea\/node.js. Hit Enter. And on the Fedora side, it too has a little bit of setup to do. And now the finishing commands, let's do Ubuntu first. Bringing those in, and then pull out my yum commands for Fedora. And OJS is installed in both instances. Next we're going to install PhantomJS. PhantomJS is a library which allows us to do headless testing of web applications. We're gonna be able to do unit testing without users having to poke anything around, really neat. And what we're gonna do is we're gonna start off by making sure that we have bzip, because that's going to be part of our installation steps. We will then set an environment variable so we don't have to repeat ourselves so many times, for how we're going to reference the name of the library. And then let's go over to the temp directory to download it and get it ready for installation. Okay, once we're in the temp directory
  we can run a curl command to unzip it. And one of the things you'll notice is that we're downloading the 1.9.8 version. As of building these install instructions, the 2.0 version which is available in a compiled version for Windows and Mac, is not available in a pre-compiled version for Linux. Now you can download the source, done it, and compile it specifically for Ubuntu or Fedora, add in a few more libraries, and you too can use 2.0. but I'll have to warn you, that is about a four to five hour process, building phantom JS totally from source. So, what we're going to do is we're going to stick with the 198 version. And what we're going to do is we're going to get it into our path by moving things over, things into user share. And of course, creating a pace, creating a soft-link so that it automatically gets placed into our path with user local.


* Sublime
  \[INAUDIBLE\] There, both 198. The next install we'll do is
  a text editor, Sublime Text. So if you go to their website and do the download, you'll find it very much worth it. And once we've downloaded it it's pretty much ready to go. Now all we need to do is get the directory that it came from over in an area we can maintain it. I just happen to be putting it in \/opt. And then we just need to expand our path. And \[INAUDIBLE\] And there's our sublime text. Okay we'll be bringing the editor up later. And if we were to sit back and look at our installation, we'll notice that there's really no files, no non-hidden files showing in our home directory. The files that I have there are part of the install that you can look at in the class repository. But, if you notice that the all the installs, Ruby wise, not the editor and things like that, are at below RBENV. Then what we can do, just to verify everything's the right version, that we're expecting. We can do a couple of repeated commands. And say that we have Git 1.9.1, PhantomJS 1.9.8, Ruby 2.2.2, and Rails 4.2.3.

* Rails application
  Now what I'd like to do is create a rails application. This isn't going to output a lot cuz I asked for it to be quiet. But we're having some Basically the overall application is being built in a test-installed directory, below this directory. And in a few seconds here it'll be ready to test out. Okay, now that the application is done, we can go in and start up the server. Make sure you see the into the directory that was just created. Before running the server command, we get the web brick server. And now, we need to leave the server running. Okay, now that our server's up, I want to run a different command. I want to bring up sublime text. And, I noticed I accidentally created my server in the temp directory. So, I need to cd over to the temp directory, and make sure that I've sourced my bash rc with that information. And then, what I can do is just open a folder, in the file system. Go over to temp, and my test install I can see, I can open up that. And now I can see my overall application. Same thing on Fedora, although I do notice that the fonts by default are not the greatest on Fedora. Out of the box. So I can open that folder. And it's looking at the application as well. Now the other thing I can do, let me just go ahead and open up another tab. Is I can bring up, and look a the web interface of the application that's running. And you see it notifying me that. Here comes my welcome page for the application we built, and I do that on Fedora I hopefully get the same thing. And here is my alert saying page is coming up. And here you go.

* Complete
  We are done installing Ruby Rails, Phantom JS, Sublime Text, and then verifying that the overall installation is complete. It should be good to go. And not have to touch an install for quite a while. All right.

  Good luck.


### 1.1.4 Software Installation for Mac Users

#### 1.1.4.1 Overview

* Mac OS Version: 10.10 - Yosemite

* Ruby \(latest\)

* Rails 4.2.3

* Git \(latest\)

* PhantomJS \(latest\)

* Sublime Text 3

* How to Configure an Environment Variable


#### 1.1.4.2 Install 'git'

* Test if git is installed already with the following command

* The following command will also **trigger** Mac OS to install the command line tools

  ```
  $ git --version
  ```

* Don't need to install the XCode platform, just quick install the command line. That is enough.

* After that, repeat the command line to double check the command line tool is installed.

  ```
  $ git --version
  ```


#### 1.1.4.3 Install Homebrew \(Package Manager\)

* It is easy and straight forward to install **Homebrew** as the **administrator**.

* Need more effort if you are **standard user**.

* **How to check** if you are administrator or standard user?

  1. System Preferences ...
  2. Users and Groups
  3. You can see your role under your name on the left side

* Once you installed Homebrew, you can find a folder named 'homebrew' under your home directory.

* Now you need to add the homebrew bin directory into your system environment. To do so,

  * go into homebrew bin directory first
  * use the following command to find out the path
    ```
    $ pwd
    ```



* go into your home directory

  * use the following command to find out the .bash\_profile

    ```
    $ ls -al
    ```

  * If you cannot find it, you may need to create a new one.

  * Add the follow line into your .bash\_profile

    ```
    export BREW\_HOME=\/Users\/xxxxxxx\/homebrew\/bin
    ... ...
    PATH=$BREW\_HOME:$PATH
    ```

  * Now you need execute the following command to make sure the system environment active

    ```
    $ source .bash\_profile
    ```



* Now double check homebrew installed

  ```
  $ brew -v
  ```


#### 1.1.4.4 Install Ruby

* Install Environment Manager

  ```
  $ brew install rbenv ruby-build
  ```

* Update .bash\_profile \(copy from Ruby web site\)

  ```
  $ echo 'if which rbenv >; /dev/null; then eval "$(rbenv init -)"; fi' >> ~\.bash\_profile
  ```

* Now you need execute the following command to make sure the system environment active

  ```
  $ source .bash\_profile
  ```

* Install Ruby \(take about 10 ~ 30 minutes\)

  ```
  $ rbenv install 2.2.3
  ```

* Set global Ruby version

  ```
  $ rbenv global 2.2.3
  ```

* Now double check ruby installed

  ```
  $ ruby -v
  ```


#### 1.1.4.5 Install Rails 4.2.3 \(this version is used for all examples in this course\)

* Install Rails with gem
  ```
  $ gem install rails -v 4.2.3
  ```


#### 1.1.4.6 rehash rbenv

* **Need to run 'rbenv rehash' any time you install a new gem that also has commands you run in the terminal**

  [https:\/\/github.com\/sstephenson\/rbenv\/\#rbenv-rehash](https://github.com/sstephenson/rbenv/#rbenv-rehash)


```
$ rbenv rehash
```

* Now double check rails installed
  ```
  $ rails -v
  ```


#### 1.1.4.7 Create a new rails project

* Create a new rails project

  ```
  $ rails new test\_project
  ```

* Go into the project directory

* Start rails server

  ```
  $ rails server
  ```

* verify the web server and the web application is running \(default is localhost:3000\)

  [http:\/\/localhost:3000](http://localhost:3000)


#### 1.1.4.8 Install the latest version of git \(optional\)

* Check current version

  ```
  $ git --version
  ```

* Install git with brew

  ```
  $ brew install git
  ```

* Double check the version

  ```
  $ git --version
  ```

* The version doesn't change, becase we need to add the new git version bin path into .bash\_profile

  ```
  $ cd /user/local/xxxxxx/git/2.5.1
  $ ls
  $ cd bin
  $ pwd
  ```

* Edit .bash\_profile

  ```
  export GIT_HOME='/user/local/xxxxxx/git/2.5.1/bin'
  PATH=$GIT_HOME:$PATH
  ```

* Now you need execute the following command to make sure the system environment active

  ```
  $ source .bash\_profile
  ```

* Double check the version

  ```
  $ git --version
  ```


#### 1.1.4.9 Install Phantomjs

* Install with homebrew

  ```
  $ brew install phantomjs
  ```

* Double check the version

  ```
  $ phantomjs -v
  ```


#### 1.1.4.10 Install Sublime 3

#### 1.1.4.11 Add system variable

* Edit .bash\_profile and add a new line like this

  ```
  export WEB\_URL='http://www.coursera.org'
  ```

* Reload the system environment

  ```
  $ source .bash\_profile
  ```

* Double check the new system variable is active

  ```
  $ echo $WEB_URL
  ```


### 1.1.5 Software Installation for Windows Users

* Ruby, Rails, Git

  * [all in one](http://railsinstaller.org/en)
  * download the package and install
  * Upgrade the rails version

    ```
    C:\> gem install rails -v 4.2.3
    ```

  * check git version

    ```
    C:\> git --version
    ```

  * check ruby version

    ```
    C:\> ruby -v
    ```

  * check rails version

    ```
    C:\> rails -v
    ```



* [phantomjs](http://phantomjs.org)

  * download zip file
  * unzip
  * go into the folder
  * bin directory
  * add PATH environment variable  
  * check version
    ```
    C:\> phantomjs -v
    ```



* [sublime](http://www.sublimetext.com)

* test ruby on rails

  ```
  C:\> rails new test_install
  C:\> cd test_install
  C:\test_install>rails server
  C:\test_install>
  ```


### 1.1.6 Editors & IDEs for Ruby on Rails

#### 1.1.6.1 IDE

* RubyMine \(not free\)
* aptana

#### 1.1.6.2 Editor

* vim
* Sublime

#### 1.1.6.3 Sublime 3

* Directory Tree Panel on the left

  Menu: 'File' --&gt; 'Open ...'

* Change color scheme

  Menu: 'Sublime Text' --&gt; 'Preferences' --&gt; 'Color Scheme'

* Customization

  Menu: 'Sublime Text' --&gt; 'Preferences' --&gt; 'Settings - xxxx'

  * Default settings can be overrided by user settings

* View Layout

  Menu: 'View' --&gt; 'Layout' --&gt; 'xxxx'

  * Open more than 1 files, and drag the file from left panel to the right panel

* Short key

  Menu: 'Sublime Text' --&gt; 'Preferences' --&gt; 'Key Bindings - xxxx'

* Find in Files

  Menu: 'Find' --&gt; 'Find in Files ...'

* Goto Anything

  Menu: 'Goto' --&gt; 'Goto Anything ...'

* Builders

  Menu: 'Tools' --&gt; 'Build'

* Plug-in and Packages

  [https:\/\/packagecontrol.io](https://packagecontrol.io)


### 1.1.7 git

#### 1.1.7.1 Introduction to Git

#### 1.1.7.2 Local Git Repository

#### 1.1.7.3 Remote Repos and Github

## 1.2 Introduction to Ruby

### 1.2.1 Github Repository for Module 2

* Each module in the course has a Github repository associated with it. The repository for Module 2 is located [here](https://github.com/jhu-ep-coursera/fullstack-course1-module2).

* You can find PDFs of the Module 2 Lecture slides [here](https://github.com/jhu-ep-coursera/fullstack-course1-module2/tree/master/Slides).

* We have also put together a comprehensive list of FAQs in the repository Wiki [here](https://github.com/jhu-ep-coursera/fullstack-course1-module2/wiki). These are usually questions encountered during assignment completion or common issues encountered during the module. Check them out if you are stuck on something or if you just want to see what interesting questions other students had!


### 1.2.2 Recommended Books

| Title | Author | Description |
| --- | --- | --- |
| Eloquent Ruby | Russ Olsen | This book eloquently describes the Ruby programming language and does not put you to sleep in the process! Whether you are new to Ruby or have programmed in Ruby before, you will find “Eloquent Ruby” useful. |
| Programming Ruby | Dave Thomas, Andy Hunt, and Chad Fowler | The famous “Pickaxe” book, called so because of the pickaxe appearing on the cover. Complete Ruby reference. |
| Beginning Ruby | Peter Cooper | Excellent coverage for many Ruby topics. |
| Head First Ruby | Jay McGavren | This book just recently came out and everyone is talking about it! I am personally a huge fan of the Head First series - they explain stuff well and get you excited about learning in the process, so you don't fall asleep. |
| Learn To Program | Chris Pine | Great for Ruby beginners. Nice build up that won't overwhelm you. Some great examples of using Ruby in everyday life. |
| Ruby Cookbook | Lucas Carlson, Leonard Richardson | Lets you break your learning of Ruby down into chunks \(recipes\). |
| The Well-Grounded Rubyist | David A. Black | David Black knows his Ruby cold and is great at explaining it to others. The book has great reviews on Amazon. |
| Metaprogramming Ruby | Paolo Perrotta | A book about the cool “don’t-try-this-at-home” Ruby features. :\) |

### 1.2.3 Ruby Introduction

#### 1.2.3.1 Ruby Basic

* Ruby History

  * Invented by Yukihiro "Matz" Matsumoto
  * **Version 1.0** released in **1996** \(Japan\)
  * Popularized by **Ruby on Rails** beginning in **2005**


* High Level Overview
  * Dynamic
  * Object-oriented: almost everything is object
  * Elgant, expressive and declarative
  * Influenced by Perl, Smalltalk, Eiffel and Lisp
  * "**Designed to make programmers happy**"


* Example
  * Loop
  * ```
    3.times { puts "hello world" }
    ```



* Ruby Basic

  * 2 spaces indentation is encouraged
  * \\# is used for commetns

    * Use comments in moderation -  the code itself should tell the story

  * Everything is evaluated



* Printing to Console

  * puts - **Standard Ruby method** to print strings to console \(as in **put s**tring\)
  * p - Prints out internal representation of an object
    * Debugger-style output



* Executing Ruby

  * code - test.rb
  * ```
    puts 3
    ```

  * Execute

  * ```
    $ ruby test.rb
    ```



* Naming Conventions

  * Variables

    * Lowercase or **_snake\_case_** if multiple words

  * Constants

    * Either **_ALL\_CAPS_** or **_FirstCap_**

  * Classes \(and Modules\)

    * **_CamelCase_**



* Drop the Semicolons
  * Leave semicolons off at the end of the line
  * Can cram several statements in with a semicolon in between
  * Usually highly discouraged
  * ```ruby
    a = 2   # encuraged
    a = 2; b = 3  # discouraged
    ```



* IRB - Interactive Ruby

  * Console-based interactive Ruby interpreter

    * REPL \(Read Evaluate Print Loop\)

  * Comes with a Ruby installation

  * Lets you experiment \(quickly\)!

    ```ruby
    $ irb
    irb> 
    irb> "hello world"
    => "hello world"
    irb>
    irb> puts "hello world"
    hello world
    => nil
    ```

  * Anything evaluates to something - no need to asign to a variable \("hello world" in the previous example\)

  * return nil \(puts "hello world"\)



#### 1.2.3.2 Flow of Control

* if, elsif, else

* ```ruby
  a = 5

  if a == 3
    puts "a is 3"
  elsif a == 5
    puts "a is 5"
  else
    puts "a is not 3 or 5"
  end

  # => a is 5
  ```

* unless

* ```ruby
  a = 5

  unless a == 6
    puts "a is not 6"
  end

  # => a is not 6
  ```

* while

* ```
  a = 10
  while a > 9
    puts a
    a -= 1
  end

  # => 10
  ```

* until

* ```
  a = 9
  until a >= 10
    puts a 
    a += 1
  end

  # => 9
  ```

* if, unless, while, until - on the same line as the statement

* ```
  # if modifier form

  a = 5
  b = 0

  puts "One liner" if a == 5 and b == 0

  # => One liner
  ```

* ```
  # while modifier form

  times_2 = 2
  times_2 *= 2 while times_2 < 100
  puts times_2 

  # => 128
  ```

* True \/ False

  * false and nil objects are false
  * **Everything else** is true


* Triple Equal

  * ===
  * "Equal" in its own way

    * Sometimes it's not about being exactly equal

  * ```
    if /sera/ === "coursera"
      puts "Triple Equals"
    end
    # => Triple Equals

    if "coursera" === "coursera"
      puts "also works"
    end
    # => also works

    if Integer === 21
      puts "21 is an Integer"
    end
    # => 21 is an Integer 
    ```



* Case Expressions

  * Two "flavors"

    * Similar to a series of "if" statement
    * Specify a target next to case and each when clause is compared to target

  * === is called the case equality operator because it is used in precisely this case!

  * No fall-through logic

  * ```
    age = 21

    case # 1st flavor
      when age >= 21
        puts "You can buy a drink"
      when 1 == 0
        puts "Written by a drunk programmer"
      else
        puts "default condition"
    end
    # => You can buy a drink
    ```

  * ```
    name = 'Fisher'
    caes name # 2nd Flavor
      when /fish/i then puts "Something is fishy here"
      when 'Smith' then puts "Your name is Smith"
    end
    # => Something is fishy here
    ```



* Loop

  * Hardly used
  * each \/ times preferred
  * ```
    for i in 0..2
      puts i
    end

    # => 0
    # => 1
    # => 2
    ```

  * **0..2** is Range data type



#### 1.2.3.3 Functions

* In Ruby, every function\/method has at least one class it belongs to

  * Not always written inside a class

* So, no real functions in Ruby, ONLY methods

* Methods

  * **Parentheses **are **optional**, both when **defining** and **calling** a method

    * Used for **clarity**

  * ```
    def simple
      puts "no parens"
    end
    def simple1()
      puts "yes parens"
    end

    simple()  # => no parens
    simple    # => no parens
    simple1   # => yes parens
    ```



* Return

  * **No need** to declare type of parameters
  * Can return **whatever** you want
  * **return** keyword is optional \(last executed line returned\)
  * ```
    def add(one, two)
      one + two
    end
    def div(one, two)
      return "I don't think so" if two == 0
      one / two
    end

    puts add(2, 2) # => 4
    puts div(2, 0) # => I don't think so
    puts div(12, 4) # => 3
    ```



* Expressive Method Names

  * Method names can end with

    * '?' - Predicate methods
    * '!' - Dangerous side-effects \(example later by strings\)

  * ```
    def can_div_by?(number)
      return false if number.zero?
      true
    end

    puts can_div_by? 3  # => true
    puts can_div_by? 0  # => false
    ```



* Default arguments

  * Methods can have default arguments

    * If a value is passed in - use that value
    * Otherwise - use the default value provided

  * ```
    def factorial(n)
      n == 0? 1 : n * factorial(n - 1)
    end
    def factorial_with_default(n = 5)
      n == 0? 1 : n * factorial_with_default(n-1)
    end

    puts factorial 5 # => 120
    puts factorial_with_default # => 120
    puts factorial_with_default(3) # => 6
    ```



* Splat

  * **\* prefixes parameter inside** method definition

    * Can even apply to **middle parameter**, not just the last

  * ```
    def max(one_param, *numbers, another)
      # Variable length parameters passed in 
      # become an array
      numbers.max
    end

    puts max("something", 7, 32, 4, "more")  # => 32
    ```



#### 1.2.3.4 Blocks

* Chunks of code

  * Enclosed between either curly braces \(**{}**\) or the keywords **do** and **end**
  * Passed to methods as last "parameter"

* Convention

  * Use **{}** when block content is a single line
  * Use **do** and **end **when block content spans multiple lines

* Often used as **iterators**

* Can accept arguments \( \| \| \)

* ```
  1.times { puts "hello world" }
  # => hello world

  2.times do |index|
    if index > 0
      puts index
    end
  end
  # => 1

  2.times { puts index if index > 0 }
  # => 1
  ```


* Coding with blocks

  * two ways to configure a block in your own method

    * Implicit

      * Use **block\_given?** to see if block was passed in

        * otherwise, an exception is thrown

      * Use **yield** to "**call**" the block

      * ```
        def two_times_implicit
          return "No block"nless block_given?
          yield
          yield
        end

        puts two_times_implicit { print "Hello" }  # => Hello
                                                   # => Hello
        puts two_times_implicit # => No block
        ```





    * Explicit

      * Use **&** in front of the last "parameter"
      * Use **call** method to call the block
      * Should check if the block is nil?
      * ```
        def two_times_explicit (&i_am_a_block)
          return "No block" if i_am_a_block.nil?
          i_am_a_block.call
          i_am_a_block.call
        end

        puts two_times_explicit # => No block
        two_times_explicit { puts "hello" } # => hello
                                            # => hello
        ```

      * 
      * 

#### 1.2.3.5 Files

* Reading from File

  * ```
    File.foreach('test.txt') do |line|
      puts line
      p line
      p line.chomp # chops off newline character
      p line.split # array of words in line
    end
    ```

  * If the file doesn't exist, you will get an exception



* Handling Exception

  * ```
    begin
      File.foreach('do_not_exist.txt') do |line|
        puts line.chomp
      end

    rescue Exception => e
      puts e.message
      puts "Let's pretent this didn't happen..."
    end
    ```

  * Alternative to Exception

  * ```
    if File.exist? 'test.txt'
      File.foreach('test.txt') do |line|
        puts line.chomp
      end
    end
    ```



* Writing to File
  * The file is automatically closed after the block executes
  * ```
    File.open("test1.txt", "w") do |file|
      file.puts "One line"
      file.puts "Another"
    end
    ```



* Environment Variables
  * Check previous chapters to revisit how to setup system environemtn variables
  * ```
    puts ENV["EDITOR"]  # => subl
    ```



#### 1.2.3.6 Strings

##### 1.2.3.6.1 String

* Single-quote literal strings are **very literal**

  * Allow **escaping** of **'** with **\**
  * Show \(almost\) everything else **as is**

* Double-quote strings

  * Interpret special characters like **\n** and **\t**
  * Allow string interpolation!

* !!! **DON'T** bother **concatenating** with **+** , you cannot concatenate strings with + operator in Ruby.

* Strings \/ Interpolation

* ```
  single_quoted = 'ice cream \n followed by it\'s a party'
  double_quoted = "ice cream \n followed by it\'s a party"

  puts single_quoted  # => ice cream \n followed by it's a party
  puts double_quoted  # => ice cream
                      # =>   followed by it's a party

  def multiply (one, two)
    "#{one} multiplied by #{two} equals #{one * two}"
  end
  puts multiply(5, 3)
  # => 5 multiplied by 3 equals 15
  ```

  * Interpolation only available for double-quoted strings

* String methods

  * String methods **ending with !** will modify the existing strings
  * Most others just return a new string
  * Can also use %Q{long multiline string}

    * same behavior as double-quoted string

  * 
  * ```
    my_name = " tim"
    puts my_name.lstrip.capitalize # => tim
    p my_name # => " tim"
    my_name.lstrip! # (destructive) removes the leading space
    my_name[0] = 'K'  # replace the first character
    ptus my_name  # => Kim

    cur_weather = %Q{It's a hot day outside
                        Grab your umbrellas ...}
    cur_weather.lines do |line|
      line.sub! 'hot', 'rainy'  # substitute 'hot' with 'rainy'
      puts "#{line.strip}"
    end
    # => It's a rainy day outside
    # => Grab your umbrella ...
    ```



* Very useful to master [string API](http://ruby-doc.org/core-2.2.2/String.html)
  * ```
    "hello".include? "lo"  # => true
    "hello".include? "ol"  # => false
    "hello".include? ?h    # => true
    ```



##### 1.2.3.6.2 Symbol

* **:foo **- highly optimized strings

* **Constant names** that you don't have to pre-declare

  * **"stands for something"** string type

* Less methods than string

* Has special purpose

* Guaranteed to be **unique** and **immutable**

* Can be converted to a **String** with **to\_s**

  * Or from String to **Symbol** with **to\_sym**

* Symbol can be a representation of a method name in Ruby

* ```
  $ irb
  > "hello".methods.grep /case/
  => [:casecmp, :upcase, :downcase, :swapcase, :upcase!, :downcase!, :swapcase!]
  ```

* Symbols and Strings are similar - You must determine which makes more sense to use


#### 1.2.3.7 Arrays

* Collection of **object references** \(auto-expeandable\)

* Indexed using **\[ \]** operator \(method\)

* Can be indexed with **negative numbers** or **ranges**

* **Heterogenous types allowed** in the same array

* Can use **%w{str1 str2}** for string array creation

* ```
  het_arr = [1, "two", :three] # heterogenous types
  puts het_arr[1]  # => two (array indicates start at 0)

  arr_words = %w{ what a great day today!}
  puts arr_words[-2]  # => day
  puts "#{arr_words.first} - #{arr_words.last}"  # => what - today!
  p arr_words[-3, 2]  # => ["great", "day"] (go back 3 and take 2)

  p arr_words[2..4]  # => ["great", "day", "today"]

  puts arr_words.join(',')  # => what,a,great,day,today!
  ```

* Modifying Array

  * Append: **push** or **&lt;&lt;**
  * Remove: **pop** or **shift**
  * Set: **\[ \]=** \(method\)

* Other methods

  * Randomly pull element\(s\) out with **sample**
  * Sort or reverse with **sort!** and **reverse!**
  * Sort or reverse **without exclamation** will return new copy of array

* ```
  stack = []; stack << "one"; stack.push ("two")
  puts stack.pop  # => two

  queue = []; queue.push "one"; queue.push "two"
  puts queue.shift  # => one

  a = [5,3,4,2].sort!.reverse!
  p a  # => [5,4,3,2]  (actually modifies the array)
  p a.sample(2)  # => 2 random elements

  a[6] = 33
  p a  # => [5,4,3,2,nil,nil,32]
  ```

* More useful methods

  * each - loop through array \(iterator\)
  * select - filter array by selecting \(takes a block, specified condition is in the block\)
  * reject - filter array by rejecting \(opposite of select\)
  * map - modify each element in the array \(map each element in the array with another element\)
  * [other API](http://ruby-doc.org/core-2.2.0/array.html)

* ```
  a = [1,3,4,7,8,10]
  a.each { |num| print num }  # => 1347810 (no new line)
                              # use puts to replace print, will get new line

  new_arr = a.select { |num| num > 4 }
  p new_arr  # => [7,8,10]
  new_arr = a.select { |num| num < 10 }.reject{ |num| num.even? }
  p new_arr  # => [1, 3, 7]

  new_arr = a.map { |x| x * 3 }
  p new_arr  # => [3, 9, 12, 21, 24, 30]
  ```


#### 1.2.3.8 Ranges

* Used to express natural **consecutive** sequences

  * 1..20, 'a'..'z'

* Two dots -&gt; **all-inclusive**

  * 1..10 \(1 and 10 are all included\)

* Three dots -&gt; **end-exclusive**

  * 1...10 \(10 is **EXCLUDED**\)

* Efficient

  * Only **start** and **end** stored

* Can be **converted** to an array with **to\_a**

* Used for **conditions** and **intervals**

* ```
  some_range = 1..3
  puts some_range.max  # => 3
  puts some_range.include? 2  # => true

  puts (1...10) === 5.3  # => true
  puts ('a'...'r') === "r"  # => false (end exlusive)

  p ('k'..'z').to_a.sample(2)  # => ["k", "w"]

  age = 55
  case age
    when 0..12 then puts "Still a baby"
    when 13..99 then puts "Teenager at heart!"
    else puts "You are getting older..."
  end
  # => Teenager at heart!
  ```


#### 1.2.3.9 Hashes

* **Indexed collections** of object references

* Created with either **{ }** or **Hash.new**

* Also known as **associative arrays**

* Index\(key\) can be **anything**

  * **Not just an integer** as in the case of arrays

* Accessed using the **\[ \]** operator

* Values set using

  * =&gt; \(creation\)
  * \[ \] \(post creation\)

  ```
  editor_props = { "font" => "Arial", "size" => 12, "color" => "red" }
  #The above is not a block, it is a hash

  puts editor_props.length  # => 3
  puts editor_props["font"]  # => Arial

  editor_props["background"] = "Blue"
  editor_props.each_pair do |key, value|
    puts "Key: #{key} value: #{value}"
  end
  # => Key: font value: Arial
  # => Key: size value: 12
  # => Key: color value: red
  # => Key: background value: Blue
  ```

* What if you try to access a value in the Hash for which an entry doesn't exist?

  * **nil** is returned by default
    * But if the Hash was created with Hash.new\(**0**\)
      * **0** is returned instead




* ```
  word_frequency = Hash.new(0)

  sentence = "Chicka chicha boom boom"
  sentence.split.each do |word|
    word_frequency[word.downcase] += 1
  end

  p word_frequency  # => {"chicka" => 2, "boom" => 2}
  ```


* As of Ruby 1.9
  * The **order** of putting things into Hash **is maintained**
  * If using symbols as key - can use **symbol:** syntax
  * If a **Hash** is the **last argument** to a method, **{ }** are **optional**
    * Last argument not including a block!



* ```
  family_tree_19 = {oldest: "Jim", older: "Joe", younger: "Jack"}
  family_tree_19[:youngest] = "Jeremy"
  p family_tree_19
  # => {:oldest=>"Jim", :older=>"Joe", :younger=>"Jack", :youngest=>"Jeremy"}

  def adjust_colors ( props = {foreground: "red", background: "white" })
    puts "Foreground: #{props[:foreground]}" if props[:foreground]
    puts "Background: #{props[:background]}" if props[:background]
  end
  adjust_colors  # => Foreground: red
                 # => Background: white
  adjust_colors ({:foreground => "green" })  # => Foreground: green
  adjust_colors background: "yella"  # => Background: yella
  adjust_colors :background => "magenta"  # => Backgroud: magenta
  ```

* Block and Hash confusion

* ```
  # You have a hash
  a_hash = { :one => "one" }

  # You output it
  puts a_hash  # => {:one => "one"}

  # If you try to do it in one step - you get a SyntaxError
  # puts { :one => "one" }

  # Ruby gets confused and think { } is a BLOCK !!!

  # To get around of this - you can use parens
  puts ({ :one => "one" })  # => {:one=>"one"}
  # Or drop the { } altogether ...
  puts one: "one"  # => {:one=>"one"}
  ```

* 
* [Hash API](http://ruby-doc.org/core-2.2.0/Hash.html)
* 

#### 1.2.3.10 Classes

* OO Review

  * Identify **things** your program is **dealing with**
  * **Classes** are **things** \(blueprints\)

    * Containers of methods \(behavior\)

  * Objects are **instances** of those things

  * Objects contain instance variabes \(state\)



* Instance variables in Ruby

  * Begin with **@**

    * Example: @name

  * Not declared

    * **Spring into existence** when first used

  * **Available to all instance methods** of the class



* Object Creation

  * Classes are **factories**

    * Calling **new** method **creates an instance** of class
    * **new** method causes **initialize**

  * Object's **state** can be \(should be\) **initialized** inside the **initialize** method, the "constructor"

  * ```
    class Person
      def initialize (name, age)  # "CONSTRUCTOR"
        @name = name
        @age  = age
      end
      def get_info
        @additional_info = "Interesting"
        "Name: #{@name}, age: #{@age}"
      end
    end

    person1 = Person.new("Joe", 14)
    p person1.instance_variables  # [:@name, :@age]
    puts person1.get_info  # => Name: Joe, age: 14
    p person1.instance_variables  # [:@name, :@age, :@additional_info]
    ```



* Accessing Data

  * Instance variables are **private**

    * Cannot be accessed from outside the class

  * Methods have **public access** by default

  * To access instance variables - need to define **"getter" \/ "setter"** methods

  * ```
    class Person
      def initialize (name, age)
        @name = name
        @age  = age
      end
      def name
        @name
      end
      def name= (new_name)
        @name = new_name
      end
    end

    person1 = Person.new("Joe", 14)
    puts person1.name  # Joe
    person1.name = "Mike"
    puts person1.name  # Mike
    # puts person1.age  # undefined method 'age' for #<Person: ...
    ```

  * Many times the getter\/setter logic is **simple**

    * **Get existing** value \/ **Set new** value

  * There should be an **easier way** instead of actually defining the getter\/setter methods

    * Use **attr\_\*** for instead
      * **attr\_accessor** - getter and setter
      * **attr\_reader** - getter only
      * **attr\_writer** - setter only




* ```
  class Person
    attr_accessor :name, :age
  end

  person1 = Person.new
  p person1.name  # => nil
  person1.name = "Mike"
  person1.age = 15
  puts person1.name  # => Mike
  puts person1.age   # => 15
  ```


* **Two problems** with the previous example

  * Person is in an uninitialized state upon creation \(without a name or age\)
  * We probably want to control the maxium age assigned

* **Solution**: Use a **constructor** and a **more intelligent** age **setter**

* Self

  * Inside instance method, **self** refer to the **object itself**
  * Usually, using **self** for **calling other methods of the same instance** is **extraneous**
  * At other times, using **self** is **required**

    * Ex. - when it could mean a **local variable assignment**

  * Outside instance method definitiion, **self** refers to the **class itself**

  * ```
    class Person
      attr_reader :age
      attr_accessor :name

      def initialize (name, ageVar)
        @name = name
        self.age = ageVar   # call the age= method
        puts age
      end
      def age= (new_age)
        @age = new_age unless new_age > 120
      end
    end

    person1 = Person.new("Kim", 13)  # => 13
    puts "My age is #{person1.age}"  # => My age is 13
    person1.age = 130  # try to change the age
    puts person1.age  # => 13
    ```

  * Why do we need **self **here?

    * Without the **self**, Ruby will create a local variable instead to use the instance variable.
    * With the **self**, Ruby will call the class method **self=** 



#### 1.2.3.11 Classes Inheritance

* var = var \|\| something

  * **\|\|** operator evaluates the left side
  * if **true** - **return** it
  * **else** - returns the **right side**
  * @x = @x \|\| 5 will return 5 the first time and @x the next time

* Short form

  * @x \|\|= 5

* ```
  class Person
    attr_reader :age
    attr_accessor :name

    def initialize (name, age)
      @name = name
      self.age = age
    end
    def age= (new_age)
      @age ||= 5  # default
      @age = new_age unless new_age > 120
    end
  end

  person1 = Person.new("Kim", 130)
  puts person1.age  # => 5  # default
  person1.age = 10
  puts person1.age  # => 10
  person1.age = 200
  puts person1.age  # => 10
  ```

* Class Methods and Variables

  * Invoked on the class \(as opposed to instance of class\)

    * Similar to **static** methods in Java

  * **self OUTSIDE** of the **method definition** refers to the **Class** object

  * **Three** ways to **define class methods** in Ruby

  * Class variables **begin** with @@



* ```
  class MathFunctions
    def self.double(var)  # 1. Using self
      times_called; var * 2;
    end
    class << self  # 2. Using << self
      def times_called
        @@times_called ||= 0; @@times_called += 1
      end
    end
  end
  def MathFunctions.triple(var)  # 3. Outside of class
    times_called; var * 3
  end

  # No instance created!
  puts MathFunctions.double 5  # => 10
  puts MathFunctions.triple(3)  # => 9
  puts MathFunctions.times_called  # => 3
  ```

* Class Inheritance

  * Every class **implicitly inherits** from **Object**

    * object itself inherits from BasicObject

  * No multiple inheritance

    * Mixins are used instead



* ```
  class Dog  # Implicitly inherites from Objects
    def to_s
      "Dog"
    end
    def bark
      "barks loudly"
    end
  end
  class SmallDog < Dog  # Denotes inheritance
    def bark  # Override
      "barks quietly"
    end
  end

  dog = Dog.new
  small_dog = SmallDog.new
  puts "#{dog}1 #{dog.bark}"  # => Dog1 barks loudly
  puts "#{small_dog}2 #{small_dog.bark}  # => Dog2 barks quietly
  ```


#### 1.2.3.12 Modules

* **Container** for classes, methods and constants

  * or other **modules**...

* Like a **Class**, but **cannot** be **instantiated**

  * **Class** inherits from **Module** and adds **new**

* Serves **two** main purpose

  * Namespace

* ```
  module Sports
    class Match
      attr_accesor :score
    end
  end

  module Patterns
    class Match
      attr_accessor :complete
    end
  end

  match1 = Sports::Match.new
  match1.score = 45; puts match1.score  # => 45

  match2 = Patterns::Match.new
  match2.complete = true; pusts match2.complete  # => true
  ```

  * Mix-in

    * Interfaces in OO

      * Contract - define what a class "could" do

    * Mixins provide a way to share \(min-in\) ready code among multiple classes

    * You can include build-in modules like **_Emunerable_** that can do the hard work for you




* ```
  module SayMyName
    attr_accessor :name
    def print_name
      puts "Name: #{@name}"
    end
  end

  class Person
    include SayMyName
  end
  class Company
    include SayMyName
  end

  person = Person.new
  person.name = "Joe"
  person.print_name  # => Name: Joe
  company = Company.new
  company.name = "Google"
  company.print_name  # => Name: Google
  ```

* Enumerable Module

  * **map, select, reject, detect** etc.
  * Used by **Array** class and **many others**
  * You can **include it** in your own class
  * Provide an implementation for **each** method

* ```
  # file name: player.rb
  class Player
    attr_reader :name, :age, :skill_level

    def initialize (name, age, skill_level)
      @name = name
      @age  = age
      @skill_level = skill_level
    end

    def to_s
      "<#{name}: #{skill_level}(SL), #{age}(AGE)>"
    end
  end
  ```

* ```
  # file name: team.rb
  class Team
    include Enumerable  # LOTS of functionality

    attr_accessor :name, :players

    def initialize (name)
      @name = name
      @players = []
    end
    def add_players (*players)  # splat
      @players += players
    end
    def to_s
      "#{@name} team: #{@players.join(", ")}"
    end
    def each
      @players.each { |player| yield player }
    end
  end
  ```

  * Demo

* ```
  require_relative 'player'  # require_relative allows importing other .rb files
  require_relative 'team'

  player1 = Player.new("Bob, 13, 5); player2 = Player.new("Jim", 15, 4.5)
  player3 = Player.new("Mike", 21, 5); player4 = Player.new("Joe", 14, 5)
  player5 = Player.new("Scott", 16, 3);

  red_team = Team.new("Red")
  red_team.add_players(player1, player2, player3, player4, player5)

  # select only between 14 and 20 and reject skill-level below 4.5
  elig_players = red_team.select { |player| (14..20) === player.age }
                         .reject { |player| player.skill_level < 4.5 }
  puts elig_players  # => <Jim: 5(SL), 15(AGE)>
                     # => <Joe: 5(SL), 14(AGE)>
  ```


#### 1.2.3.13 Scope

* Methods and classes begin **new score** for variables

  * Outer scope variables **do not** get carried over to the inner scope
  * Can use **local\_variables** method to see which variables are in \(and which are not in\) the current scope

* ```
  v1 = "outside"

  class MyClass
    def my_method
      # p v1 EXCEPTION THROWN - no such variable exists
      v1 = "inside"
      p v1
      p local_variables
    end
  end

  p v1  # => outside
  obj = MyClass.new
  obj.my_method  # => inside
                 # => [:v1]
  p local_variables  # => [:v1, :obj]
  p self  # => main
  ```

* Scope: Constants

  * **Constant** is any reference that begins with **uppercase**, including classes and modules
  * Constants' scope rules are **different** than variable scope rules
  * Inner scope **can see** constants defined in outer scope and **can also override** outer constants
    * Value remains **unchanged** outside



* ```
  module Test
    PI = 3.14
    class Test2
      def what_is_pi
        puts PI
      end
    end
  end

  Test::Test2.new.what_is_pi  # => 3.14
  ```

* ```
  module MyModule
    MyConstant = 'Outer Constant'
    class MyClass
      puts MyConstant  # => Outer Constant
      MyConstant = 'Inner Constant'
      puts MyConstant # => Inner Constant
    end
    puts MyConstant  # => Outer Constant
  end
  ```

* Scope: Block

  * Blocks **inherit** outer scope
  * Block is a **closure**
    * **Remembers** the context in which it was defined and **uses** that context whenever it is called



* ```
  class BankAccount
    attr_accessor :id, :amount
    def initialize(id, amount)
      @id = id
      @amount = amount
    end
  end

  acct1 = BankAccount.new(123, 200)
  acct2 = BankAccount.new(321, 100)
  acct2 = BankAccount.new(421, -100)
  accts = [acct1, acct2, acct3]

  total_sum = 0
  accts.each do |eachAcct|
    total_sum += eachAcct.amount
  end

  puts total_sum  # => 200
  ```

  * Even though blocks **share** the outer scope - a variable created inside the block is **only available** to the block
  * **Parameters** to the block are **always local** to the block - **even if** they have the **same name** as variables in the outer scope
  * Can **explicitly declare** block-local variables after a **semicolon** in the block parameter list

* ```
  arr = [5, 4, 1]
  cur_number = 10
  arr.each do |cur_number|
    some_var = 10  # NOT available outside the block
    print cur_number.to_s + " "  # => 5 4 1
  end
  puts  # print a blank line
  puts cur_number  # => 10

  adjustment = 5
  arr.each do |cur_number; adjustment|  # declare a local variable and will not effect the outer variable with the sam ename
    adjustment = 10
    print "#{cur_number + adjustment}"  # => 15 14 11
  end
  puts
  puts adjustment  # => 5 (Not affected by the block)
  ```


#### 1.2.3.14 Access Control

* When **designing** your class - **important** to think about **how much** of it you will be **exposing** to the world

* **Encapsulation**: try to hide the **internal representation** of the object so you **can change it** later
* Three levels: **public**, **protected** and **private**
* ```
  class Car
    def initialize (speed, comfort)
      @rating = speed * comfort
    end

    # Cannot SET rating from outside
    def rating
      @rating
    end
  end

  puts Car.new(4, 5).rating  # => 20
  ```

  * Details of how rating is calculated are kept inside the class. And you can change the formula as well.

* **Two ways** to **specify** access control
  * **Specify** public, protedted or private
    * **Everything** until the **next access control keyword** will be of that access control level

  * **Define** the methods regularly and then specify public, protected and private access levels and list the comma-separated methods **under** those levels using **method symbols**


```
class MyAlgorithm
  private
    def test1
      "Private"
    end
  protected
    def test2
      "Protected"
    end
  public
    def public_again
      "Public"
    end
end
```

```
class Another
  def test1
    "Private, as declared later on"
  end
  private :test1
end
```

* Access Control

  * **public** methods - **no** access control is enforced
    * **Anybody** can call these methods

  * **protected** methods - **can be invoked** by the objects of the defning class or its subclasses
  * **private** methods - **cannot be invoked** with an explicit receiver
    * **Exception**: Setting an attribute can be invoked with an explicit receiver


* ```
  class Person
    def initialize (age)
      self.age = age  # LEGAL - EXCEPTION (Because we have no choice. Without self.,  ruby will treat age as a local variable)
      puts my_age
      # puts self.my_age  # ILLEGAL
                          # CANNOT USE self or any other receiver
    end

    private
      def my_age
        @age
      end
      def age=(age)
        @age = age
      end
  end

  Person.new(25)  # => 25
  ```













### 1.2.4 Introduction to Unit Testing

* Ruby ships with **Test::Unit**

* In Ruby 1.8 - Test::Unit was **bloated with extra libraries** that include unnecessary code

* Ruby 1.9 **stripped** Test::Unit to a minimum

  * The new framework is officially called **MiniTest**, but it's a **drop-in replacement**, so **no changes are required** to Test::Unit code.

* Test::Unit is a member of the XUnit family \(JUnit, CppUnit\)

* Basic idea - extend Test::Unit::TestClass

* Prefix method names with **test\_**

* If one of the methods **fails** - others **keep going** \(this is good\)

* Can use **setup\(\)** and **teardown\(\)** methods for setting up behavior that will execute before **every** test method


* Example

  * calculator.rb

  ```
  class Calculator

    attr_reader :name

    def initialize(name)
      @name = name
    end

    def add (one, two)
      one - two
    end

    def sub (one, two)
      one + two
    end

    def div (one, two)
      one/two
    end
  end
  ```

  * calculator\_test.rb

  ```
  require 'test/unit'
  require_relative 'calculator'

  class CalculatorTest < Test::Unit::TestCase
    def setup
      @calc = Calculator.new('test')
    end

    def test_addition
      assert_equal 4, @calc.add(2,2)
    end

    def test_subtraction
      assert_equal 2, @calc.sub(4,2)
    end

    def test_division
      assert_equal 2, @calc.div(4,2)
    end

    def test_divide_by_zero
      assert_raise ZeroDivisionError do
        @calc.divide(1, 0)
      end
    end
  end
  ```

  * **assert\_raise**: what exception you expecting \(XXXXXXError\)

  * Execute **Test::Unit**



```
  $ ruby calculator.rb
```

### 1.2.5 Introduction to RSpec

* More **descriptive**, more **English-like**
* The **writing** of the test is more **intuitive** as well as the **output**
* Installing RSpec
* ```
  $ gem install rspec
  ```

* In your project, generate rspec folder by

* ```
  $ rspec --init
  ```

* describe\(\) method

  * is the top level method
  * Include set of **related tests** \(a.k.a. example group\)
  * Takes either a **String** or **Class** as argument
  * All specs **must be inside a describe block**
  * No class to subclass
    * Unlike Test::Unit which always subclasses TestCase class
    * Everything happends inside the describe\(\) method



* before\(\) and after\(\) methods
  * **before\(\)** and **after\(\)** methods are similar to **setup\(\)** and **teardown\(\)** in **MiniTest**
  * Can pass in either **:each** or **:all** \(infrequently used\) to **specify** whether the block will run **before\/after each test or once before\/after all tests**
  * **before :all** could be useful, if for example you only want to connect to DB once


* it\(\) method
  * Used to define the **actual** RSpec specifications\/examples
  * Takes an **optional string** that **describes the behavior** being tested


* Example

  * calculator.rb
  * ```ruby
    class Calculator

      attr_reader :name

      def initialize(name)
        @name = name
      end
      def add(one, two)
        one - two
      end
      def sub(one, two)
        one + two
      end
      def div(one, two)
        one / two
      end
    end  
    ```

  * calculator\_spec.rb

  * ```ruby
    require 'rspec'
    require_relative '../calculator'

    describe Calculator do
      before { @calculator = Calculator.new('RSpec calculator') }

      it "should add 2 numbers correctly" do
        expect(@calculator.add(2, 2)).to eq 4
      end
      it "should sub 2 numbers corrctly" do
        expect(@calculator.sub(4, 2)).to eq 2
      end
    end
    ```

  * Run the test

  * ```
    $ rspec
    $ rspec --format documentation
    ```



### 1.2.6 RSpec Matchers

* RSpec "hangs" **to** and **not\_to** methods on **all outcome of expectations**
* to\(\)\/not\_to\(\) methods take **one parameter** - a **matcher**
* Matcher examples

  * be\_true \/ be\_false \/ be\_nil \/ be\_even \/ be\_odd
  * eq 3
  * raise\_error\(SomeError\)

* Be\_predicate - boolean

  * If the **object** on which the **test is operating** has a **predicate \(boolean\) method** - you **automatically** get a **be\_predicate** matcher

  * So, for exampe **be\_nil** is a **valid matcher** since every Ruby object has a :nil? method



* [More matchers](https://relishapp.com/rspec/rspec-expectations/docs/built-in-matchers)

## 1.3 Introduction to Ruby on Rails

### 1.3.1 Github Repository for Module 3

* Each module in the course has a Github repository associated with it. The repository for Module 3 is located [here](https://github.com/jhu-ep-coursera/fullstack-course1-module3).

* You can find PDFs of the Module 3 Lecture slides [here](https://github.com/jhu-ep-coursera/fullstack-course1-module3/tree/master/Slides).

* We have also put together a comprehensive list of FAQs in the repository Wiki [here](https://github.com/jhu-ep-coursera/fullstack-course1-module3/wiki). These are usually questions encountered during assignment completion or common issues encountered during the module. Check them out if you are stuck on something or if you just want to see what interesting questions other students had!


### 1.3.2 Recommended Books

| Title | Author | Description |
| --- | --- | --- |
| Agile Web Development with Rails 4 | Dave Thomas, Sam Ruby and David Heinemeier Hansson | Great book on Rails! First runs through a Rails application and only then explains the topics, but a lot of people actually like that. |
| Ruby on Rails Tutorial | Michael Hartl | This book does a wonderful job of explaining Rails development. |
| Rails 4 in Action | Ryan Bigg, Yehuda Katz, Steve Klabnik, Rebecca Skinner | Another great book on developing with Ruby on Rails |

### 1.3.3 Introduction to Rails

### 1.3.4 Creating your First Application

* Console command

  ```
  $ rails new [app name]
  ```

  * In the end, will run 'bundle install'. This will access rubygems.org and may take some time.
  * Can try '--skip-bundle' command option if necessary

* Command will generate .gitignore. So you can

  ```
  $ git init
  $ git add .
  $ git commit -m "Initial commit"
  ```

* Start the build in web server

  ```
  $ rails s
  ```

* Access your web appliction @ localhost:3000

* Place static web page into **public** folder

  * Server looks into **public** directory before looking anywhere else


### 1.3.5 Controller and View

* Console command

  ```
  $ rails g controller [controller name] [action1 action2 。。。]
  ```

  * This command will generate controller and view

* ERB \(Embedded Ruby\)

  * .erb extension
  * Looks like HTML
  * Embedded Ruby
  * Two tag patterns
    ```
    <% ... ruby code ... %>
    <%= ... ruby code ... %>
    ```



### 1.3.6 Routes

* Routes file location
  config\/routes.rb

* Rake

  * Ruby's build language
  * Ruby's **make**
  * No XML - wirtten in Ruby
  * Rails uses rake to automate app-related tasks

* List rake tasks

  ```
  $ rake --tasks
  ```

* Get details for individual task

  ```
  $ rake --describe [task\_name\]
  ```

  _For example_

  ```
  $ rake --describe routes
  ```

* Rake Routes

  ```
  $ rake routes
  ```


### 1.3.7 Moving Business Logic Out of View

### 1.3.8 Helpers

* Helpers are useful for those reusable code

* Available for ALL views!!! \(NOT ONLY one controller's view\)

* in app\/helpers folder

* Rails Build-in Helpers

  * link\_to

    ```
    link_to name, path
    ```

  * Path could either be \_url\(full path\) or \_path

    ```
    <p><%= link_to "Google", "http://www.google.com" %></p>
    <p><%= link_to "Goodby", greater_goodbye_path %></p>
    ```



### 1.3.9 Introduction to HTTPParty

* [https:\/\/rubygems.org](https://rubygems.org)

* Command gem to get more information

  ```
  gem
  ```

* Check if HTTParty is installed

  ```
  gem list httparty
  ```

* To install HTTParty

  ```
  gem install httparty
  ```

* Get more details about HTTParty

  ```
  gem list httparty -d
  ```

* Restful Web Services

  * Have a **base URI**
  * Support a **data exchange format** like XML or JSON
  * Support a set of HTTP operations \(GET, POST etc.\)

* HTTParty Gem

  * Restful web services client \(Web browser\)
  * Automatic parsing of JSON and XML into Ruby hashes
  * Provides support for:
    * Basic http authentication
    * Default request query parameters



* Lots of Restful APIs out [there](http://www.programmableweb.com/apis)

* To use HTTParty

  * include HTTParty module
  * Can specify:
    * base\_uri
    * default\_params \(API developer key for example\)
    * format



* Coursera Restful API

  [https:\/\/tech.coursera.org\/app-platform\/catalog\/](https://tech.coursera.org/app-platform/catalog/)


### 1.3.10 Bundler

* Rails build in gem

  http:\/\/bundler.io

* Gemfile

* Run bundle install or bundle after specifying a new gem in Gemfile

* Run bundle update when modifying a version of a gem

* Can specify a version

  ```
  gem "nokogiri"
  gem "rails", "3.0.0.beta3"
  gem "rack", "&gt;=1.0"
  gem "thin", "&gt;= 1.1", "&lt; 2.0"
  gem "thin", "~&gt;1.1"
  ```

* Can give another name for require in source code

  ```
  gem "sqlite3-ruby", require: "sqlite3“
  ```

* Can use different version of Rails

* Gemfile.lock contains the actual gem versions


### 1.3.11 Rails & HTTPParty Integration

* in Gemfile

  ```
  gem 'httparty', '0.13.5'
  ```

* in console

  ```
  bundle
  ```

  _or_

  ```
  bundle install
  ```

* restart Rails server

* Generate controller

  ```
  rails g controller courses index
  ```

  * This command will add route automatically

* Create new model

  * Create new file **coursera.rb** in model folder

* In coursera.rb

  ```
  class Coursera
  include HTTParty

  base_uri 'http://api.coursera.org/api/catalog.v1/courses'
  default_params fields: "smallIcon, shortDescription", q: "search"
  format :json

  def self.for term
    get("", query: { query: term})["elements"]
  end
  end
  ```

  * Here we can include HTTParty directly, no need to require HTTPary at the beginning of the file. Because all files in **app** folder are automatically required.


* In controller, courses\_controller.rb
  ```
  class CoursesController < ApplicationController
  def index
    @search_term = 'jhu'
    @courses = Coursera.for(@search_term)
  end
  end
  ```


### 1.3.12 CSS, Parameters & Root Path

* views\/layout\/application.html.erb
  * This file will apply to all views


* yield

  ```
  <%= yield %>
  ```

  * This line will display the view


* app\/assets\/stylesheets folder
  * there is one scss file for each controller
  * scss is super css
  * you can define css patten in scss


* Zebrify the rows

  ```
  <% @courses.each do |course| %>
  <tr class=<%= cycle('even', 'odd') %>
    <td><%= image_tag(course["smallIcon"])%></td>
    <td><%= course["name"] %></td>
    <td><%= course["shortDescription"] %></td>
  </tr>
  <% end %>
  ```

  * cycle is Rails helper function
  * cycle can take more than two parameters


* params helper

  * add the following into controller index action

    ```
    @search_term = params[:looking_for] || 'jhu'
    ```

  * [http:\/\/localhost:3000\/courses\/index?looking\_for=Python](http://localhost:3000/courses/index?looking_for=Python)



* root path
  * in routes.rb
    ```
    root 'courses#index'
    ```



### 1.3.13 Deploy to Heroku

* [heroku](http://heroku.com) is a PaaS \(Platform as a Service\)
* Free account
* heroku toolbelt - download and install

  * command line tool

* Heroku uses **Postgres** and recommand **rails\_12factor** gem

  * find more details about **rails\_12factor** in **github**

* Put **sqlite** gem into development group and **heroku** gems in production

  * Gemfile 

  ```
  source 'https://rubygems.org' 

  gem 'rails', '4.2.3' 
  gem 'sqlite3', group: :development
  gem 'sass-rails', '~> 5.0' 
  gem 'uglifier', '>= 1.3.0' 
  gem 'coffee-rails', '~> 4.1.0' 
  gem 'jquery-rails' 
  gem 'turbolinks' 
  gem 'jbuilder', '~> 2.0' 
  gem 'sdoc', '~> 0.4.0', group: :doc 

  # Use ActiveModel has_secure_password 
  gem 'bcrypt', '~> 3.1.7' 

  group :development, :test do 
    gem 'byebug' 
    gem 'web-console', '~> 2.0' 
    gem 'spring'  
  end 

  group :production do 
    gem 'pg' 
    gem 'rails_12factor' 
  end 

  gem 'httparty', '0.13.5' 
  ```

* bundle

  ```
  $ bundle --without production 
  ```

* heroku login and push project source code

  ```
  $ heroku login
  $
  $ heroku create search-coursera-jhu
  $
  $ git remote -v
  $
  $ git push heroku master
  $
  ```

* Make sure that the top level directory of your git repo contains your app directory and other Rails files and directories. Thus heroku can know your are using Ruby on Rails.


### 1.3.14 Blackbox Testing

* Combine **RSpec** and **[Capybara](https://github.com/jnicklas/capybara)** Ruby gems

#### 1.3.14.1 Example git repository

* [blackbox testing repository in git](https://github.com/jhu-ep-coursera/fullstack-course1-module3-blackbox-testing)

* .rspec file in root directory

* spec\_helper.rb file in **spec** folder

  ```
  require 'xxxxx'
  ```

* Capybara.app\_host

* describe "xxxxx" do

* it "xxxxx" do

* visit "xxxxx"

* Check the README.md in this repos

  How do I get started?

  ```
  $ gem install rspec
  $ gem install selenium-webdriver
  $ gem install capybara
  $ gem install poltergeist
  $ rbenv rehash
  ```

* .rspec

  * .rspec is from the following command

  ```
  $ rspec --init
  ```

  * Capybara::DSL
    * Capybara::DSL is a kind of language



* command to test

  ```
  $ rspec --format documentation
  ```


#### 1.3.14.2 :selenium vs. :poltergeist

* Different drivers to determind if you want browser flash in front of your eyes

* Example blackbox testing source code

* spec\coursera\_app\_spec.rb file

* set default driver

  ```
  Capybara.default_driver = xxxxxx
  ```

* Need PhantomJS browser

* [poltergeist](https://github.com/teampoltergeist/poltergeist) is a PhantomJS driver for Capybara


#### 1.3.14.3 rspec parameter

* rspec --format documentation

* Will output blackbox test details to the console


### 1.3.15 Debugging Rails Applications

* use heroku logs in production environment

  * goto app folder in console
    ```
    $ heroku logs
    ```



* in develop environment

  * Gemfile

    ```
    group :development, :test do
    gem 'byebug'
    gem 'web-console', '~> 2.0'
    gem 'spring'
    end
    ```

  * rails server provide logs and embedded console for debugging



