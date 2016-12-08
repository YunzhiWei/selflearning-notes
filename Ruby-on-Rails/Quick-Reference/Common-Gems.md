# Common Gems

# HTTParty

## Send HTTP request - 'get' method
```
      > HTTPParty.get("http://localhost:3000/roles.json)
```

## Send HTTP request and get response
```
      > HTTPParty.get("http://localhost:3000/roles.json).response
     => #<Net::HTTPOK 200 OK  readbody=true>
```

## Send HTTP request and check response code
```
      > HTTPParty.get("http://localhost:3000/roles.json).response.code
     => 200
```

## Send HTTP request and parse response
```
      > pp HTTPParty.get("http://localhost:3000/roles.json).parsed_response
      => [{"id"=>"2456",
           "url"=>"xxxx",
```


# byebug

# web-console

# spring

