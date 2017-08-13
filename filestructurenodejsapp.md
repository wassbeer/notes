# Best Practice Express File Structure

This file outlines a best practice file structure as initialized by Stefan Fidanov on the <a href="https://www.terlici.com/2014/08/25/best-practices-express-structure.html">Terlici blog</a>. 

## Table of Contents:
1. [Background](#Background)
2. [File Structure](#file-structure)
3. [Elucidation](#elucidation)

## Background

During te NYCDA Web Development with Node.js course in the summer of 2017, Amsterdam, several projects required clear structuring of files and directories. For a timestamp-microservice-api side project I wrote this file. 

## File Structure

project/
  routes/
    comments.js
    index.js
    users.js
  helpers/
    dates.js
  middlewares/
    auth.js
    users.js
  models/
    comment.js
    user.js
  public/
    libs/
    css/
    img/
  views/
    comments/
      comment.jade
    users/
    index.jade
  tests/
    controllers/
    models/
      comment.js
    middlewares/
    integration/
    ui/
  .gitignore
  app.js
  package.json

## Elucidation

controllers/ – defines your app routes and their logic
helpers/ – code and functionality to be shared by different parts of the project
middlewares/ – Express middlewares which process the incoming requests before handling them down to the routes
models/ – represents data, implements business logic and handles storage
public/ – contains all static files like images, styles and javascript
views/ – provides templates which are rendered and served by your routes
tests/ – tests everything which is in the other folders
app.js – initializes the app and glues everything together
package.json – remembers all packages that your app depends on and their versions