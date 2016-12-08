# 4. Debugging


---
# Install


---


### Gemfile
```
      gem 'pry'
      gem 'pry-byebug'
```

### source code

##### declare requirement

```
      require 'pry-byebug'
```


##### set breakpoint

```
      binding.pry
```


##### check class

```
     (byebug) params[:race].class
     ActionController::Parameters
```



---
# Case Study
___

###  Can't verify CSRF token authenticity 
* You may need 'protect_from_forgery with: :null_session' for your REST API control

```
      module Api
        class ResultsController < ApplicationController
          protect_from_forgery with: :null_session
          ... ...
```


---
# Links

___

* [Rails的调试 ruby-debug 安装使用和命令详解](http://hlee.iteye.com/blog/361405)

* [使用 pry 调试 rails 项目--调试代码成为乐趣](https://ruby-china.org/topics/22376) * [Debugging Rails Applications](http://guides.rubyonrails.org/debugging_rails_applications.html)