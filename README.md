# yii2 advanced Project

This is a Symfony project. Below you will find the necessary configuration for the `.htaccess` file to handle different request paths and redirect them appropriately.

## .htaccess Configuration

Create or update the `.htaccess` file in the root of your project with the following content:

```
Options +FollowSymLinks
IndexIgnore */*
RewriteEngine on

# If the request starts with /api, rewrite to /api/web/
RewriteCond %{REQUEST_URI} ^/api
RewriteRule ^api\/?(.*) /api/web/$1

# If the request starts with /admin, rewrite to /backend/web/
RewriteCond %{REQUEST_URI} ^/admin
RewriteRule ^admin\/?(.*) /backend/web/$1

# Redirect any request that does not start with /frontend/web, /backend/web, /admin, /api/web, or /api to /frontend/web/
RewriteCond %{REQUEST_URI} !^/(frontend/web|backend/web|admin|api/web|api)
RewriteRule (.*) /frontend/web/$1

# If the request is within /frontend/web
RewriteCond %{REQUEST_URI} ^/frontend/web
RewriteCond %{REQUEST_FILENAME} !-f
RewriteCond %{REQUEST_FILENAME} !-d
RewriteRule . /frontend/web/index.php

# If the request is within /backend/web
RewriteCond %{REQUEST_URI} ^/backend/web
RewriteCond %{REQUEST_FILENAME} !-f
RewriteCond %{REQUEST_FILENAME} !-d
RewriteRule . /backend/web/index.php

# If the request is within /api/web
RewriteCond %{REQUEST_URI} ^/api/web
RewriteCond %{REQUEST_FILENAME} !-f
RewriteCond %{REQUEST_FILENAME} !-d
RewriteRule . /api/web/index.php
```
