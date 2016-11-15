Simple JWT Demo
=============

A simple demo implementation of JWT with Rails. 

For a more in depth exploration of this topic, see [here](https://www.sitepoint.com/introduction-to-using-jwt-in-rails/).

## Prerequisites: ##
- Ruby 2.3.0
- Rails 4.2.3

## Setup: ##

1. Clone repository.

2. Run `bundle install` from inside repo directory to install gems.

3. Initialize SQLite database: `rake db:create && rake db:migrate`

4. Add dummy user:
   1. Using the `Rails` console:

        ```console
        rails c
        rails> User.create(email:'jdoe@acme.com', password:'changeme', password_confirmation:'changeme')
        ```
        
## Simple JWT Demo: ##
1. Start rails server.
   1. Like this:

        ```console
        rails s
        ```

2. In separate console, issue `curl` to `localhost:3000`:
   1. Like this:

        ```console
        {"errors":["Not Authenticated"]}
        ```

   - This shows that the endpoint is checking for a JWT Token.

3. Now issue a login request
   1. Like this:

        ```console
        curl -X POST -d email="jdoe@acme.com" -d password="changeme" http://localhost:3000/auth_user 
        ```
   2. To get back a token:

        ```console
        {
        	"auth_token":"eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ1c2VyX2lkIjoxfQ.LgnvSfjuwtADkAsO6OL7jvjyivYvlC3ZwXgMjuhMcYg",
        	"user":{"id":1,"email":"jdoe@acme.com"}
        }
        ```

4. Pass along the token in request:
   1. Like this:

        ```console
        curl --header "Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ1c2VyX2lkIjoxfQ.LgnvSfjuwtADkAsO6OL7jvjyivYvlC3ZwXgMjuhMcYg" http://localhost:3000/home
        ```
   2. To see a successful authentication:

        ```console
        {"logged_in":true}
        ```

## License ##

This code is licensed under the [Apache 2.0 License](https://github.com/mafernando/simple_jwt_demo/blob/master/LICENSE.txt).
