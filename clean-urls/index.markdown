---
layout: page
title: Clean URLs
---
# Clean URLs

GitPHP supports generating clean urls (also known as permalinks and REST-style urls) throughout the application. This means that instead of a url that looks like this:

```
/gitphp/index.php?p=project.git&a=commit&h=1a2b3c4d5e6f7a8b9c0d1e2f3a4b5c6d7e8f9a0b
```

You can have URLs that look like:

```
/gitphp/projects/project.git/commits/1a2b3c4d5e6f7a8b9c0d1e2f3a4b5c6d7e8f9a0b
```

Or, if you additionally turn on [abbreviateurl]({{ site.baseurl }}/configuration-options/#abbreviateurl):

```
/gitphp/projects/project.git/commits/1a2b3c6
```

GitPHP will automatically generate these clean URLs throughout the application by setting the [cleanurl]({{ site.baseurl }}/configuration-options/#cleanurl) config setting. However, in order for your web server to be able to route these urls to the appropriate action, you will need to set up URL rewrite rules in your web server's configuration.

## Apache mod_rewrite
If your Apache instance is set up to support reading .htaccess files, you can create a file called .htaccess in the GitPHP root directory with the following directives:

```
RewriteEngine On
RewriteBase /
RewriteCond %{REQUEST_FILENAME} !-f
RewriteCond %{REQUEST_FILENAME} !-d
RewriteRule ^(.*)$ index.php?q=$1 [L,QSA]
```

If you have GitPHP set up in a subdirectory of the domain instead of the domain root, you can modify the RewriteBase command to the appropriate subdirectory:

```
RewriteEngine On
RewriteBase /my/gitphp/install
RewriteCond %{REQUEST_FILENAME} !-f
RewriteCond %{REQUEST_FILENAME} !-d
RewriteRule ^(.*)$ index.php?q=$1 [L,QSA]
```

If your webserver does not have htaccess enabled, but you do have access to the web server configuration, the rewrite directives can be set up in a directory block inside your virtual host in httpd.conf:

```
<Directory "/var/www/localhost/htdocs/domain.com">
    RewriteEngine on
    RewriteBase /
    RewriteCond %{REQUEST_FILENAME} !-f
    RewriteCond %{REQUEST_FILENAME} !-d
    RewriteRule ^(.*)$ index.php?q=$1 [L,QSA]
</Directory>
```

Or again, if you have GitPHP in a subdirectory:

```
<Directory "/var/www/localhost/htdocs/domain.com/my/gitphp/install">
    RewriteEngine on
    RewriteBase /my/gitphp/install
    RewriteCond %{REQUEST_FILENAME} !-f
    RewriteCond %{REQUEST_FILENAME} !-d
    RewriteRule ^(.*)$ index.php?q=$1 [L,QSA]
</Directory>
```

## Nginx HttpRewriteModule
Nginx rewriting is very easy using the try_files config option, which will check for a file's existence and automatically fallback to a rewrite if the file doesn't exist. This helps ensure that the static files such as javascript and css continue to be served properly, and is much faster than using an if statement in your nginx configuration.

If you are running GitPHP as the root application of the domain, in your nginx configuration, add a block inside your `server` block that looks like this:

```
location / {
    try_files $uri $uri/ /index.php?q=$uri&$args;
}
```

This will attempt to serve the request uri if it exists, and automatically rewrite it to the q parameter with the associated arguments if the static file doesn't exist.

If you are running GitPHP from a subdirectory below your root domain, just edit the rewrite with the appropriate directory:

```
location /my/gitphp/install/ {
    try_files $uri $uri/ /my/gitphp/install/index.php?q=$uri&$args;
}
