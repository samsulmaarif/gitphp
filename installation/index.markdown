---
layout: page
title: Installation
---
# Installation

## Minimum Requirements
* git (standard [git](http://git-scm.com/) on \*nix, [Git for Windows](http://msysgit.github.com/) on Windows)
* PHP-compatible web server ([Apache](http://httpd.apache.org/), [nginx](http://www.nginx.org/), etc)
* [PHP 5.2.3](http://php.net/) or higher, with the following:
    * [Zlib](http://www.php.net/manual/en/book.zlib.php)
    * [SPL](http://us.php.net/manual/en/book.spl.php) (Standard PHP Library)
    * [Safe Mode](http://us.php.net/manual/en/features.safe-mode.php) **disabled**

## Optional Additions
* PHP modules:
    * [POSIX](http://us.php.net/manual/en/book.posix.php) for reading repository owner info on \*nix
    * [Multibyte string support](http://us.php.net/manual/en/book.mbstring.php) for reading git repos with multibyte encodings
    * [Bzip2](http://us.php.net/manual/en/book.bzip2.php) for generating bz2 snapshots
    * [xdiff](http://us.php.net/manual/en/book.xdiff.php) for faster diffing
    * [Fileinfo](http://us.php.net/manual/en/book.fileinfo.php) for mime type support for blobs
    * [Memcache](http://us.php.net/manual/en/book.memcache.php) or [Memcached](http://us.php.net/manual/en/book.memcached.php) for Memcache cache support
    * [SimpleXML](http://us.php.net/manual/en/book.simplexml.php) for reading scm-manager config files

## Repository Prep
To begin, you need to have your git repositories set up in a directory that the webserver can access. They can be in subdirectories within that, but you will need a base directory to tell GitPHP where to look for repositories.

**These must be [bare repositories](http://schacon.github.com/git/user-manual.html#public-repositories). GitPHP will not read working copy repositories (the .git hidden folder in your source tree).**

You can make a copy of your bare repository by running:

~~~
git clone --bare ~/myproject /gitprojects/myproject.git
~~~

Or, a new bare repository can be initialized with:

~~~
git init --bare /gitprojects/mybareproject.git
~~~

Once you have your projects in a directory, something like:
* /gitprojects/project1.git
* /gitprojects/project2.git
* /gitprojects/subdir/project3.git
Now you can begin setting up GitPHP.

## Install
1. Extract the GitPHP files to a place readable by your web server.
2. Change the permissions of the templates_c directory to be writable by your webserver. This can be done by either:

~~~
chown apache:apache templates_c
~~~

(assuming your webserver runs as user/group apache - this is the better way), or:

~~~
chmod 777 templates_c
~~~

## Required Configuration
1. Set up your config file. In the config directory, copy the example config file, gitphp.conf.php.example, to gitphp.conf.php.
2. Specify the 'projectroot' setting. This specifies where your git repositories are - following the previous example, it would be set up as "/gitprojects/". This is the only required setting.

All the available config options and their default settings are documented on the [Configuration Options]({{ site.baseurl }}/configuration-options) page, as well as in gitphp.conf.defaults.php. If you want to change any of the settings, just copy the config option from the defaults file to your normal config and change the setting.

During upgrades, your existing config file will not be overwritten. However, new options or features may be added to the defaults file, so you may want to check for updates to the config options page or defaults file every now and then.

## Optional Configuration
1. If you want to enable caching (recommended), see the [Caching]({{ site.baseurl }}/caching) page.
2. If you want to set up categories for your projects, or use a text file with a list of projects, you need to set up the $git_projects array in projects.conf.php. Copy projects.conf.php.example to projects.conf.php and edit it - the definition and structure of this is explained in the config file, or you can visit the [Project List]({{ site.baseurl }}/project-list) page.
3. If you want to edit the text header that appears above the project list on the home page, create templates/hometext.tpl with your header content.
