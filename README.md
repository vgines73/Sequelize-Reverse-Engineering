# Sequelize - Reverse Engineering

## 1) Config Folder:
middleware Folder: to restrict routes to user if not logged in;

isAuthenticated.js: function to where the user is logged in, proceed; if not return to login page

config.json: used to connect the mysql database either in development, test, production. Input user password under password to connect the data from the database.

passport.js: to authentic user login; requires passport, passport-local, and models. Pretty much use passport to create username and password but instead of username will be using email. Functions used to search for email and password; if email is not in the system, return message that it email was incorrect; Or if password is incorrect, return message password was incorrect. However if both email and password are legit, the user gets to log in. To keep authentication across HTTP requests, you need to serialize and deserialize using Sequelize.

## 2) Models Folder: 
Using Sequelize to create and use the database. Pretty much mySQL under the hood.

Index.js: connects to server.js, passport.js, api-routes.js; ‘use strict’ pretty much means you need declare variables to create the database. There’s no comments in the file so will add that in the file. See file for comments.

user.js: connects to isAuthenticated.js, passport.js, uses bcryptjs for password hashing. Create a User model where it creates the tables for the database (what's needed for email and what's needed for password). There’s another function that compares users password with stored hashed password. Last one is to automatically hash password the first time User is created by using a Hook Method.

## 3) Public Folder: 
Front-End; What the user sees; Bootstrap is used for styling as well;
	
js Folder: javascript functionality; jQuery

login.js: connects to login.html in the same folder and api-routes.js in the routes folder; submits a form and validates that must have both email and password to login; then redirects to members.html page and posts the users info.

members.js: does a GET request to figure out which user logged in and updates the page; connects to members.html page.

signup.js: connects to signup.html in the same folder and api-routes.js in the routes folder; submits a form and validates that must have both email and password to sign in; then redirects to members.html page and posts the users info.

stylesheets Folder: front-end styling for the html pages

style.css: top margins for classes form.signup and form.login have 50px.

login.html: connects to login.js in js folder in public folder; html login page setup using a form with inputs and a button to submit; link provided for those who do not have a login and need to sign up; if clicked, goes to signup.html.

members.html: connects to members.js in js folder in public folder; html members page setup contains a navbar with link to logout. Logout connects to routes folder under api-routes.js

signup.html: connects to signup.js in js folder in public folder; html signup page setup using a form with inputs and a button to submit; also contains an error alert message. Link provided for those who already have an account and needs to log in.

## 4) Routes Folder: 
What connects the front end to the back end;

api-routes.js: back end; requires models and passport; uses the middleware to authenticate email and password to proceed if not send err. Looks like basic CR in CRUD functionality for sign up and log in.

html-routes.js: front end; requires path and middleware to check if a user is logged in by authenticating email and password. Bunch of GET functions to sign up or login and redirects them to the correct html page. 

## 5) package-lock.json: 
Contains libraries and dependencies needed to operate.

## 6) package.json: 
Pretty much a list of what libraries and dependencies are needed.

## 7) server.js: 
Creates the server to run the app on localhost. Require npm packages, Set up port, require models for syncing, create express app and configure middleware for authentication, require the routes, then sync database using sequelize and listen on the port. 
