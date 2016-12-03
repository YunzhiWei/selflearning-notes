# Software installation

## Course1_Ruby-on-Rails-An-Introduction - 1.1.3

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

## Course3_Ruby-on-Rails-Web-Services-and-Integration-with-MongoDB - 3.1.5 Mongo Installation
## Course3_Ruby-on-Rails-Web-Services-and-Integration-with-MongoDB - 3.1.6.4 IRB shell and MongoDB

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

# Environment Configure

## Course3_Ruby-on-Rails-Web-Services-and-Integration-with-MongoDB - 3.1.13 Rails Setup

You many need to change the source in the Gemfile as the following if you run bundle in China

```
source 'http://gems.ruby-china.org'
```
