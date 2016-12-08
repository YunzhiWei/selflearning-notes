# 100. Coding and Config

# Helper

## link_to

## params


---

## Config files

---

### Gemfile

```
  gem 'mongoid', '~> 5.0.0'
```

### config\/application.rb

* Load the generated mongoid.yml file when rails runtime environment start
  ```
    module XXXXXXX
      class Application < Rails::Application
        ...
        # bootstraps mongoid within applications -- like rails console
        Mongoid.load!('./config/mongoid.yml')
        ...
      end
    end
  ```


### config\/routes.rb

[Custom routes](http://guides.rubyonrails.org/routing.html)

##### Default Routes \(last line in routes.rb\)

```
      match ':controller(/:action(/:id))(.:format)' 
```

##### RESTful Routes

```
      Prefix     Verb    URI Pattern                   Controller#Action
      racers     GET     /racers(.:format)             racers#index
                 POST    /racers(.:format)             racers#create
   new_racer     GET     /racers/new(.:format)         racers#new
  edit_racer     GET     /racers/:id/edit(.:format)    racers#edit
       racer     GET     /racers/:id(.:format)         racers#show
                 PATCH   /racers/:id(.:format)         racers#update
                 PUT     /racers/:id(.:format)         racers#update
                 DELETE  /racers/:id(.:format)         racers#destroy
```

* racers\_path:     map the path for index and create actions
* new\_racer\_path:  map the path for new action
* edit\_racer\_path: map the path for edit action
* racer\_path:      map the path for show, update, and destroy actions

##### Named Routes

```
      match 'hello', :to => "users#index", as => 'hello' 
```

* hello\_path:      map the path for users\#index
* hello\_url:       map the url for users\#index

  ```
    get "/login" => "sessions#new", as: "login"
    delete "/logout" => "sessions#destroy", as: "logout" 
  ``` 
 * get/delete are the method
 * "/login"/"logout" are the url
 * "sessions#new"/"sessions#destroy" are the controller actions
 * **as: "login"/"logout"** makes the **_path** and **_url** available for you code. You can use **login_path**/**logout_path** or **login_url**/**logout_url** in your code.


##### Nested Routes

```
      resources :aricles do
        resoures :comments
      end
```

or

```
      resources :articles, :has_many => :comments
```

* Example: [http:\/\/localhost:3000\/articles\/1\/comments](http://localhost:3000/articles/1/comments)

##### Regular Routes

```
      match 'users/search/:id/:age', :controller => 'users', :action => 'search', :age => /[2-5][0-9]/
```

* Router will do regular check for :age
* ONLY age between 20 to 59 is valid
* This url will match and be routed: [http:\/\/domain.com\/users\/search\/1\/25](http://domain.com/users/search/1/25)
* This will not match and be routed: [http:\/\/domain.com\/users\/search\/1\/60](http://domain.com/users/search/1/60)

##### Simple

```
      get "demo/index" 
```

equals to

```
      match "demo/index", :to => "demo#index" 
```

##### Root

```
      root :to => "demo#index"
```

* [Ruby On Rails 路由配置简述](http://my.oschina.net/VincentJiang/blog/170543)
* [routes.rb 详解](http://www.360doc.com/content/11/1117/20/1542811_165286129.shtml)

### lib\/\*.rake file

* TBD

---

## Coding

---

### attribute

```
  attr_reader
  attr_accessor
```

### store\_in other collection

```
  class Racer
    include Mongoid::Document
    include Mongoid::Timestamps
    store_in collection: "racer1"
```

### Access self field

```
  class LegResult
    include Mongoid::Document
    field :secs, type: Float
    def secs= value
      self[:secs] = value
      calc_ave
    end
  end
```

### Control list order in controller

```
    class RacesController < ApplicationController
      ... ...
      def index
        @races = Race.all.order_by([[:date, :desc]]) 
      end
```

### Generate url link in view

```
      @patient = Patient.find(17)
      <%= link_to Patient Record", patient_path(@patient)  %>

```

### render - status option

* [Layouts and Rendering in Rails](http://guides.rubyonrails.org/layouts_and_rendering.html)

