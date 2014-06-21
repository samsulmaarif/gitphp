---
layout: page
---
GitPHP is a web frontend for [git](http://git-scm.com/) repositories. It emulates the look of standard gitweb, but is written in PHP and makes use of [Smarty](http://www.smarty.net/) templates for customization.

GitPHP is open source under the [GNU GPLv2](http://www.gnu.org/licenses/old-licenses/gpl-2.0.html).

# Features

Some key features of GitPHP are:

* Support for multiple projects with categories
* Various ways to set up project list (search a directory, hardcoded list, Gitweb/Gitosis/Gitolite project list, [scm-manager](http://www.scm-manager.org/) config)
* Support for viewing common git objects/actions (log, commit, tree, blob, tag, head, file history, blame)
* Syntax highlighting using [GeSHi](http://qbnz.com/highlighter/)
* Unified and side-by-side diffs of commits and files
* Commit and file searching
* Snapshot downloading
* RSS/Atom and OPML feeds
* Multilanguage support
* Caching using files or memcache for performance
* Works with standard [git](http://git-scm.com/) on Linux as well as [Git for Windows](http://msysgit.github.com/)

# Download

The current release is 0.2.9.1. You can get it from the [releases list](https://github.com/xiphux/gitphp/releases).

# Demo

You can use GitPHP to browse the GitPHP master repository at [http://source.gitphp.org](http://source.gitphp.org).

# Documentation

Installing and configuring GitPHP is easy. The [installation]({{ site.baseurl }}/installation) page should be all you need to get started.

Other documentation:

* [Frequently Asked Questions]({{ site.baseurl }}/faq)
* [Configuration Options]({{ site.baseurl }}/configuration-options)
* [Configuring the Project List]({{ site.baseurl }}/project-list)
* [Caching]({{ site.baseurl }}/caching)
* [Clean URLs]({{ site.baseurl }}/clean-urls)
* [User Authentication]({{ site.baseurl }}/user-authentication)
* [Translating]({{ site.baseurl }}/translating)
* [Acknowledgements]({{ site.baseurl }}/acknowledgements)

# Source

### Browse

You can browse the GitPHP repository using GitPHP at [http://source.gitphp.org](http://source.gitphp.org) or on [GitHub](https://github.com/xiphux/gitphp).

### Clone

You can clone the GitPHP repository from the [GitHub project page](https://github.com/xiphux/gitphp).

### Build

GitPHP can be run directly from a snapshot tarball or a git checkout. However, there are a few things to be aware of before doing this. Please read [building a release]({{ site.baseurl }}/build).

# API

Generated documentation for the source tree can be viewed at [http://api.gitphp.org](http://api.gitphp.org).

# Support

For bugs, enhancement suggestions, and questions, feel free to submit to the [issue tracker](https://github.com/xiphux/gitphp/issues?state=open) with the appropriate label. Alternately, you can contact [Chris Han](https://github.com/xiphux) directly.

# Contribute

GitPHP is currently a single developer project. However, I’m willing to review and accept code contributions from a variety of sources - patches submitted on the issue tracker or directly by email, pull requests, discussions on forums, etc.
