# Ruby on Rails self Learning Notes

This file file serves as your book's preface, a great place to describe your book's content and ideas.

---

# Convention

---

## Web server response to any web page request

* Web server will try to search _**pulic folder**_ first when getting any _**web page request**_
* If cannot find the resource in _**public folder**_, Web Server will follow the _**route configuration**_.

---

# Links





有了rbenv来管理多版本的ruby环境，我们还需要一个能管理多版本gem\(比如rails\)的工具，那就是bundler了，项目背景不细说了，需要了解的直接到官网http:\/\/bundler.io\/,这里只讲一些实际使用经验。

**安装**

[?](http://www.jb51.net/article/85752.htm#)

| 1 | `gem install` `bundler` |
| --- | --- |

**使用**

[?](http://www.jb51.net/article/85752.htm#)

| 1234 | `mkdir` `app1; cd` `app1;echo` `"source '`[`https://ruby.taobao.org/`](https://ruby.taobao.org/)`'"` `> Gemfileecho` `"gem 'rails,'4.1.0'"` `>> Gemfilebundle install` |
| --- | --- |

上面代码在app1下安装了rails 4.1.0,使用bundle exec rails -v查看当前目录下使用的rails版本，显示内容应该为Rails 4.1.0,同样此时通过bundle exec rails new . --force覆盖原来Gemfile,此时的app使用的rails版本为4.1.0。

[?](http://www.jb51.net/article/85752.htm#)

| 1234 | `mkdir` `app2; cd` `app2;echo` `"source '`[`https://ruby.taobao.org/`](https://ruby.taobao.org/)`'"` `> Gemfileecho` `"gem 'rails,'3.2.13'"` `>> Gemfilebundle install` |
| --- | --- |

上面代码创建了第二个app2文件夹，并通过bundler安装了rails 3.2.13 同样通过bundle exec rails new . --force可以生成基于rails 3.2.13版本的应用。

安装了以上两个版本后，通过gem list --local可以看到rails有两个版本，显示为rails \(4.1.0, 3.2.13\),bundler会智能的判断每个项目的rails版本，以确保应用的正确运行，但前提是通过使用bundle exec命令来执行原来得命令，例如:

[?](http://www.jb51.net/article/85752.htm#)

| 123 | `bundle exec` `rails sbundle exec` `rake db:create` |
| --- | --- |







---

* [Ruby Doc](http://ruby-doc.org) 

* [Ruby微信开发的几个开源项目介绍](http://www.jb51.net/article/49869.htm)_[ruby专题](http://www.jb51.net/article/49869.htm)_[脚本之家](http://www.jb51.net/article/49869.htm)

* [你应该学会使用的5个ruby方法](http://www.tuicool.com/articles/jMrmA3F)


* [Rails 技巧之 tap & try](https://ruby-china.org/topics/5348)

* [5个使用Rails控制台的有用技巧](http://hlee.iteye.com/blog/358516)

* [夜鸣猪的Ruby On Rails 空间](http://hlee.iteye.com/)


