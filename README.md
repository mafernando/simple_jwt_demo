Simple JWT Demo
=============

A simple implementation of JWT with Rails for demo purposes. 

For a more in depth exploration of this topic, see [here](https://www.sitepoint.com/introduction-to-using-jwt-in-rails/).

## Prerequisites: ##
- Ruby 2.3.0
- Rails 4.2.3

## Setup: ##

1. Clone repository.

2. Run `bundle install` from inside repo directory to install gems.

3. Initialize SQLite database:
```console
  rake db:create
  rake db:migrate
```

4. Add dummy user in Rails console:
```console
rails c
rails> User.create(email:'a@a.com', password:'changeme', password_confirmation:'changeme')
```

## Simple JWT Demo: ##
1. Start rails server.
```console
rails s 
```

2. In separate console, issue `curl` to `localhost:3000`:
   1. Like this:

        ```c
        printf("Hello, World!");
        ```

   - This shows that the endpoint is checking for a JWT Token.

3. Now issue a login request to get back a token:
```console
curl -X POST -d email="a@a.com" -d password="changeme" http://localhost:3000/auth_user 
# {
# 	"auth_token":"eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ1c2VyX2lkIjoxfQ.LgnvSfjuwtADkAsO6OL7jvjyivYvlC3ZwXgMjuhMcYg",
# 	"user":{"id":1,"email":"a@a.com"}
# }
```

4. Pass along the token in a subsequent request to see a successful authentication:
```console
curl --header "Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ1c2VyX2lkIjoxfQ.LgnvSfjuwtADkAsO6OL7jvjyivYvlC3ZwXgMjuhMcYg" http://localhost:3000/home
# {"logged_in":true}
```

## License ##

This code is licensed under the [Apache 2.0 License](https://raw.githubusercontent.com/mafernando/api/master/LICENSE).