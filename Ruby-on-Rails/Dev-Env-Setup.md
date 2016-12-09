# 1. Software installation

## 1.1 Course1_Ruby-on-Rails-An-Introduction - 1.1.3

* Ruby
* Rails

Install Rails with the following command

```
gem install rails -v 4.2.3
```

You may need '--source' option to install Rails correctly

```
gem install rails --source http://rubygems.org -v 4.2.3
```

* 官网下载RailsInstaller 4.2（Ruby 2.2）之后，双击安装。更改安装路径到D盘，安装完成之后，输入命令：ruby -v 和gem -v 都正常，但输入rails -v 之后，提示“系统找不到指定路径”。

**Solution**:
Find the file of 'rails.bat' in the folder of  'C:\\RailsInstaller\\Ruby2.2.0\\bin\\'
And update the content as following:

```
@ECHO OFF
IF NOT "%~f0" == "~f0" GOTO :WinNT
ECHO.This version of Ruby has not been built with support for Windows 95/98/Me.
GOTO :EOF
:WinNT
@"%~dp0ruby.exe" "%~dpn0" %*
```

bundle 命令也存在同样问题，用上述方法加以解决。

* Git
* phantomjs

## 1.2 Course3_Ruby-on-Rails-Web-Services-and-Integration-with-MongoDB - 3.1.5 Mongo Installation

## 1.3 Course3_Ruby-on-Rails-Web-Services-and-Integration-with-MongoDB - 3.1.6.4 IRB shell and MongoDB

* mongo-ruby dirver

```
gem update -system
gem install mongo
gem install bson_ext
```

Using  --source http://rubygems.org when executing gem install command
gem install mongo --source http://rubygems.org

* install gem rake as well (to make the 'rake db:seed' command success)

```
gem install rake --source http://rubygems.org
```

## 1.4 Install DevKit

You may see the following error when running 'bundle install'

```
Gem::InstallError: The 'json' native gem requires installed build tools.

Please update your PATH to include build tools or download the DevKit
from 'http://rubyinstaller.org/downloads' and follow the instructions
at 'http://github.com/oneclick/rubyinstaller/wiki/Development-Kit'

An error occurred while installing json (1.8.3), and Bundler cannot continue.
Make sure that `gem install json -v '1.8.3'` succeeds before bundling.
```

To solve the problem

* Download from [here](http://rubyinstaller.org/downloads)
* Instruction [here](https://github.com/oneclick/rubyinstaller/wiki/Development-Kit)


# 2. Create New Project

## 2.1 Course3_Ruby-on-Rails-Web-Services-and-Integration-with-MongoDB - 3.1.13 Rails Setup

* rails new <project name>
* cd <project folder>
* Update Gemfile
* bundle
* create config/mongoid.yml
* include mongoid.yml in config/application.rb

You many need to change the source in the Gemfile as the following if you run bundle in China

```
source 'http://gems.ruby-china.org'
```

# 3. Scaffolding

## 3.1 Course3_Ruby-on-Rails-Web-Services-and-Integration-with-MongoDB - 3.3.17 Scaffolding

## 3.2 Course3_Ruby-on-Rails-Web-Services-and-Integration-with-MongoDB - 3.1.16.2 Scaffold command

* rails g model
* rails g Scaffold_controller
* routes

**Important**
The Timestamps must be added, else .json will not work correctly

```
include Mongoid::Timestamps
```

# 4. Prepare the data in mLab

* [mLab](https://mlab.com/) is prety simple and straight forward
* Prepare one database and create one or more collections there
* Use the 'Tools' menu to import raw data into the colletions

# 5. Heroku

* Create your own app in [Heroku](https://heroku.com)
* You may need to install **Heroku CLI**
* You may also need to add **Environment Variable** into your OS and Heroku

## 3.3 Course1_Ruby-on-Rails-An-Introduction - 1.3.13 Deploy to Heroku

## 3.4 Course2_Rails-with-Active-Record-and-Action-Pack - 2.4.8 Deploying to Heroku and Enabling SSL

## 3.5 Course3_Ruby-on-Rails-Web-Services-and-Integration-with-MongoDB - 3.1.19 Heroku Setup
