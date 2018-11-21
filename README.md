# Basic login project with Angular 6
This is a example of a login with Angular6. Well it's not only login, its actually authentication and it's basic pattern.

## Reinventing the wheel again
Every project I have authentication (web or mobile), I keep repeating myself and write the authentication layer from scratch. As I get older, I wanted to have a basic goto authentication template to work with. So that's the reasen of this little project.

## What's in this project?
- Bootstrap 4 (https://getbootstrap.com/)
- Fontawesome 5 (https://fontawesome.com/)
- Angular 6 (https://angular.io/)
- A basisc authentication service to handle the login/logout/check authentication token
- A simple secure dashboard
- A simple login page (including error handling)
- A fake backend service to handle the api request
- A service to inject the authentication token on each request to the api
- Angular Routing system
- Some RxJS function (http://reactivex.io/) 

## The authentication pattern
So what's the authentication pattern/lifecycle?

- Login (validate the user on the serve)
- Check the auhtentication status of the logged in user
- Logout

Sounds easy right? But a lot goes into this logic. And a lot of this logic goes behind the scenes. Let's dive into it.

## Login flow
So for mortal people, they only see the login page, fill in the details and press submit. But what actually happens behind the screen? These are (in short) the steps/workflow:

- The application sends the login data to the server.
- Server checks if the user is valid.
- If the user is valid, the server will generate a token. This token is associated to the user, so every time a api request is made with that token, the server knows wich user it is.
- The server will return (or not) the token (and depending on your backend service also some basic information about the user)
- When the application recieves the token, the token will be locally stored and the user get's redirected to the next page (usually a home or dashboard page).
- If there is a invalid login, the application needs to handle the error (for example display an error text)

## Validate token flow
Each time you start the application, it checks if there was a token stored. The token is just a string generated by the server. This token can be anything ofcourse. So we need to check if the token is still valid. The basic flow is this:

- The application checks if a token is stored.
- If there's a token stored, check make a api request to validate the token.
- If everything in the the above steps is ok, then the application can just continue.
- If there was an error of any kind, the logout process is started and the user will be presented with the login screen


## Logout flow
When the logout process is started (started by the user or by the application), the following wil happen:

- An api request is made to the server with the stored token.
- The server can remove the token, so this token cannot be used anymore.
- The application will delete all stored data (for example the token, user meta data).
- The application will send a signal that a logout is issued so other components/services etc can act on it.
- The user is redirected to the login page




License
----

MIT


**Free Software, Hell Yeah!**