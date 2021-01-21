# ReverseEngineering
AS A developer  I WANT a walk-through of the codebase  SO THAT I can use it as a starting point for a new project

https://docs.google.com/document/d/1ukleYYPqmtgaQw01AIVE0_zrfnk3B6RwrGN_P_24aDc/edit?usp=sharing

Sequelize Reverse Engineering

USER STORY:
As someone who wants to safely log in to "X" site, I want to know my personal details are safely stored in a database so that I don't have to worry about the security of using "X" site.
OVERVIEW & PURPOSE:
This tutorial serves as a ‘walk-through’ for developers to familiarise themselves with a new codebase. This codebase can then be used to start a new project.
This codebase is for password authentication. It allows a user to create an account, log into an account and sign back out securely - all on website files. All user data is stored in a MySQL Database. 

WALKTHROUGH:
Begin using this codebase by first cloning the repository into your local storage.

Create SQL Scripts for 3 x databases as named in the  config.json file.
Open and run scripts in MySQL workbench to create the 3 databases.

Edit the config.js file and include your own personal data (i.e: password for mySQL).
Open integrated terminal and run “NPM install” to install the required node modules for this project.
Run NPM audit fix if any issues 
Run Node Server.JS to check server is working
Test html features (3 sites) by opening the local server link in your web browser.
Check the mySQL database to ensure login data is saved.

FILE WALKTHROUGH WITH STEPS:

Config Folder / Middleware Folder / Authenticated.js This middleware file restricts routes that the user is not allowed to visit if they are not logged in. For example: the user cannot reach the members page if not logged in. If the user is logged in, it continues with request. This is the security feature of this passport codebase.

Config Folder/  config.json middleware connection configuration to connect to server.

Config Folder/  passport.json  contains javascript logic that tells the passport module that  we want to log in with an email address and password.


Models Folder / index.js This model connects to the database and imports each user's log-in data.

Models Folder/ user.js Requires "bcrypt" module  for password hashing. This feature makes our database secure even if compromised. This javascript defines what is in our database.




Bin Folder This folder stores the executable files so that the node module functions work when on the local server.
Public Folder/ js Folder / login.js Getting references to our form and inputs. When the form is submitted, we validate there's an email and password entered. If we have an email and password we run the loginUser function and clear the form. loginUser does a post to our "api/login" route and if successful, redirects us to the members page. If there's an error, log the error.


Js Folder / members.js This file just does a GET request to figure out which user is logged in  and updates the HTML on the page. 

Js Folder / signup.js Getting references to our form and input. When the signup button is clicked, we validate the email and password are not blank. If we have an email and password, run the signUpUser function. Does a post to the signup route. If successful, we are redirected to the members page. Otherwise we log any errors. If there's an error, handle it by throwing up a bootstrap alert.

Stylesheets Folder / style.css This file alters the style of the login page.

Stylesheet Folder / login.html, members.html and signup.html files gives us the layout of our HTML pages.




Routes Folder / api-routes.js  Requiring our models and passport as we've configured it. Using the passport.authenticate middleware with our local strategy. If the user has valid login credentials, send them to the members page.  Otherwise the user will be sent an error. Route for signing up a user. The user's password is automatically hashed and stored securely thanks to. how we configured our Sequelize User Model. If the user is created successfully, proceed to log the user in, otherwise send back an error. Route for logging user out. Route for getting some data about our user to be used client side. The user is not logged in, send back an empty object. Otherwise send back the user's email and id. Sending back a password, even a hashed password, isn't a good idea.






Routes Folder / html-routes.js  Requiring path to so we can use relative routes to our HTML files. Requiring our custom middleware for checking if a user is logged in. If the user already has an account send them to the members page. Here we've added our isAuthenticated middleware to this route. If a user who is not logged in tries to access this route they will be redirected to the signup page. 


.gitignore contains the files to be excluded from being saved in the repository.

Database_production.sql, database_test.sql and passport_demo.sql These files are the database files that we created to run our application. These files are storing the data.


Server.js This file is responsible for ; Requiring necessary npm packages.  Requiring passport as we've configured it. Setting up port and requiring models for syncing. Creating express app and configuring middleware needed for authentication. We need to use sessions to keep track of our user's login status. Requiring our routes. Syncing our database and logging a message to the user upon success. 


AREAS FOR IMPROVEMENTS:
Change all vars to consts and lets where relevant
Add warnings when the user tries to sign up with a email that is already in the database
Add warning when the password does not meet requirements
Create some additional features in the members page to customise such as ‘date joined’ and edit password section.
Potentially use AJAX to streamline API call functions
Move isAuthenticated to within the html routes file 
Integrate the app into a dummy website to practically demonstrate its features. A relevant example might be a shopping site/ login to access wishlist, shopping cart, checkout etc. Another example might be a forum. 
Create github and heroku repos to host your new project and REMEMBER to create a .gitignore file for your node modules!

