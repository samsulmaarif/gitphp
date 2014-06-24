---
layout: page
title: Configuration Options
---
# Configuration Options

This is a list of all of GitPHP supported configuration options. All of these options have reasonable defaults, but they're here if you want to tweak them. These are also documented in config/gitphp.conf.defaults.php.

A handful of these settings can also be overridden on a per-project basis; see the [Project Settings]({{ site.baseurl }}/project-list/#project-settings) page for more info.

## Projects

### projectroot
**This is the only option that must be set by you for GitPHP to function, as there is no way to provide a default.**

Full directory on the server where projects are located

Example: /pub/gitprojects

Default: *none*

### exportedonly
When listing all projects in the project root (not specifying any projects manually or using a project list file), set this to true to only allow repositories with the special file git-daemon-export-ok (see the git-daemon man page)

Default: false

## Appearance

### locale
This is the default locale/language used in the interface. The locale must exist in the locale/ directory.

Default: en_US

### title
The string that will be used as the page title.

The special variable $gitphp_appstring will expand to the app name (gitphp) and version. The special variable $gitphp_version will expand to the version number only.

Default: $gitphp_appstring (gitphp {version})

### homelink
This is the text of the link in the upper left corner that takes you back to the project list. Note that overriding this string will hardcode the language.

Default: projects

### cloneurl
Sets the base clone url to display for a project. This is the publicly-accessible url of the projectroot that gets prepended to the project path to create the clone url. It can be any format, for example:
* http://server.com/
* ssh://server.com/git/
* git://server.com/gitprojects/
If left blank, no clone url will display.

Example: http://localhost/git/

Default: *none*

### pushurl
Sets the base push url to display for a project. Works the same as [cloneurl](#cloneurl).

Example: http://localhost/git/

Default: *none*

### bugpattern
Sets the regular expression to use to find bug number references in log messages. The pattern should have a group that extracts just the bug ID to pass to the bug tracker.

For example, `/#([0-9]+)/` will recognize any number with a # in front of it, and groups the numeric part only. Another common example is `/bug:([0-9]+)/` to extract bug numbers with bug: in front of them.

Example: `/#([0-9]+)/`

Default: *none*

### bugurl
Sets the URL for the bug tracker. This URL must have a back reference to the group in the bug pattern that contains the ID. For example, ${1} uses the first group.

Example: http://localhost/mantis/view.php?id=${1}

Default: *none*

### self
This is the path to the script that will be inserted in URLs. If you leave this blank/commented the script will try to guess the correct URL, but you can override it here if it's not being guessed correctly.

Example: http://localhost/gitphp/

Default: *autodetected*

### stylesheet
Path to the look and feel (skin) stylesheet in the css directory.

Default: gitphpskin.css

### javascript
Toggles on/off javascript features

Default: true

### googlejs
Toggles whether to use the [Google Libraries API](http://developers.google.com/speed/libraries/) to load javascript libraries, which takes advantage of the speed and caching of Google's servers and content delivery network.
The libraries are served from Google's servers, which means your users must have an internet connection, so this may not be appropriate for closed intranets. By enabling this you agree to Google's terms for their library API.

Default: false

## Features

### compat
Set this to true to turn on compatibility mode. This will cause GitPHP to rely more on the git executable for loading data, which will bypass some of the limitations of PHP at the expense of performance.
Turn this on if you are experiencing issues viewing data for your projects.

Default: false

### largeskip
When GitPHP is reading through the history for pages of the shortlog/log beyond the first, it needs to read from the tip but skip a number of commits for the previous pages. The more commits it needs to skip, the longer it takes.
Calling the git executable is faster when skipping a large number of commits, i.e. reading a log page significantly beyond the first. This determines the threshold at which GitPHP will fall back to using the git exe for the log.
Currently each log page shows 100 commits, so this would be calculated at page number * 100. So for example at the default of 200, pages 0-2 would be loaded natively and pages 3+ would fall back on the git exe.

Default: 200

### uniqueabbrev
If this is turned on, when GitPHP abbreviates hashes, it will ensure that the abbreviated hash is unique for the project, extended the abbreviated hash if necessary until it becomes unique.
Searching through every single pack in the repository for collisions is a performance intensive process that can slow down page loads. If you turn this on, it's highly recommended to merge all of your existing packs into a single pack using git gc --aggressive (or git repack -a -d).

Default: false

### compressformat
Indicates what kind of compression will be done on the snapshot archive. Recognized settings are:

* GITPHP_COMPRESS_BZ2 - create a tar.bz2 file (PHP must have bz2 support)
* GITPHP_COMPRESS_GZ - create a tar.gz file (PHP must have gzip support)
* GitPHP_COMPRESS_ZIP - create a zip file

Any other setting, or no setting ,will create uncompressed tar archives. If you choose a compression format and your PHP does not support it, GitPHP will fall back to uncompressed tar archives.

Note that users with javascript get to choose their snapshot format when they request it, so this only applies to users without javascript or if you turn the javascript setting off.

Default: GITPHP_COMPRESS_ZIP

### compresslevel
Sets the compression level for snapshots. Ranges from 1-9, with 9 being the most compression but requiring the most processing.

Bzip2 default: 4

Gzip default: -1

### geshi
Run blob output through geshi syntax highlighting and line numbering

Default: true

### search
Set this to false to disable searching.

Default: true

### filesearch
Set this to false to disable searching within files (it can be performance intensive).

Default: true

### filemimetype
Attempt to read the file's mime type when displaying (for example, displaying an image as an actual image in a browser). This requires either PHP >= 5.3.0, [PECL fileinfo](http://pecl.php.net/package/Fileinfo), or Linux.

Default: true

### abbreviateurl
Generates urls using abbreviated hashes instead of full hashes.

Note that urls with abbreviated hashes are not safe to be saved long term (eg bookmarks), as future objects may be added to the repository that cause an abbreviated hash to no longer be unique.

This option only takes effect with the [compat](#compat) option turned off.

Additionally, this option will automatically enable [uniqueabbrev](#uniqueabbrev), as an abbreviated hash must be unique in order to resolve it to a full hash.

Default: false

### cleanurl
Uses clean, rest-style urls throught GitPHP

This requires additional setup in your web server to rewrite urls (mod_rewrite on Apache, HttpRewriteModule on Nginx, etc). URLs must be rewritten to point to index.php?q={query}.

For more instructions on how to set this up, see [Clean URLs]({{ site.baseurl }}/clean-urls).

Default: false

### feedfilter
Sets a regular expression to use to filter commits out of the project atom/rss feed. Commits that have a commit message matching this pattern will be excluded.

For example, '/GIT_SILENT/' will exclude any commit with the string GIT_SILENT in the commit message.

Default: *none*

### showrestrictedprojects
By default, when [user-based restrictions]({{ site.baseurl }}/user-authentication) are enabled, projects that are not available to the logged in user will be hidden in the project list. Setting this option will instead display these projects as disabled in the project list.

Default: false

## Filesystem Paths

### gitbin
Path to git binary. For example, /usr/bin/git on Linux or C:\\Program Files\\Git\\bin\git.exe on Windows with msysgit. You can also omit the full path and just use the executable name to search the user's $PATH.
Note: Versions of PHP below 5.2 have buggy handling of spaces in paths. Use the 8.3 version of the filename if you're having trouble, e.g. C:\\Progra~1\\bin\\git.exe.

Linux default: git

Windows x86 default: C:\\Progra~1\\Git\\bin\\git.exe (C:\Program Files\Git\bin\git.exe)

Windows x64 default: C:\\Progra~2\\Git\\bin\\git.exe (C:\\Program Files (x86)\Git\bin\git.exe)

### magicdb
Path to the libmagic db used to read mimetypes. Only applies if filemimetype=true. You can leave this as null and let the system try to find the database for you, but that method is known to have issues. If the path is correct but it's still not working, try removing the file extension if you have it on, or vice versa.

Linux default: /usr/share/misc/magic

Windows default: C:\\wamp\\php\extras\\magic

## Cache

See [Caching]({{ site.baseurl }}/caching) for more info on cache options setup.

### cache
Turns on template caching. If in doubt. leave it off. You will need to create a directory 'cache' and make it writable by the web server.

Default: false

### objectcache
Turns on object caching. This caches immutable pieces of data from the git repository. You will need to create a directory 'cache' and make it writable by the web server. This can be used in place of the template cache, or in addition to it for the maximum benefit.

Default: false

### cacheexpire
Attempts to automatically expire cache when a new commit renders it out of date. This is a good option for most users because it ensures the cache is always up to date and users are seeing correct information, although it is a slight performance hit. However, if your commits are coming in so quickly that the cache is constantly being expired, turn this off.

Default: true

### cachelifetime
Sets how long a page will be cached, in seconds. IF you are automatically expiring the cache (see the '[cacheexpire](#cacheexpire)' option), then this can be set relatiely high, 3600 seconds (1 hour) or even longer. -1 means no timeout. If you have turned cacheexpire off because of too many cache expirations, set this low (5-10 seconds).

Default: 3600

### objectcachelifetime
Sets how long git objects will be cached, in seconds. THe object cache only stores immutable objects from the git repository, so there's no harm in setting this to a high number. Set to -1 to never expire.

Default: 86400

### objectcachecompress
Sets the size threshold at which objects will be compressed when being stored into the object cache. Compression saves cache space but adds a very slight decompression overhead. Set to 0 to disable compression.

Default: 500

### memcache
Enables memcache support for caching data, instead of Smarty's standard on-disk cache. Only applies if cache=true or objectcache=true (or both). Requires either the Memcached or Memcache PHP extensions.

This is an array of servers. Each server is specified as an array.
* Index 0 (required): The server hostname/IP
* Index 1 (optional): The port, default is 11211
* Index 2 (optional): The weight, default is 1

Example:
{% highlight php startinline %}
array(
    array('127.0.0.1', 11211, 2),
    array('memcacheserver1.local', 11211),
    array('memcacheserver2.local')
)
{% endhighlight %}

Default: *none*

### objectmemory
If set, this will limit the number of git objects GitPHP keeps in PHP's memory during execution, to this specific number. This can be set if you have a low memory limit on your web server.

Please note that setting this too low will severely degrade performance, as GitPHP will have to repeatedly load the same objects off of the disk, since the limit prevents them from being kept in memory. It's strongly recommended that you turn [debug](#debug) mode on and view the MemoryCache size on various pages (in the debug output) to get a feel for the size of your projects before setting this.

0 means no limit.

Default: 0

## Debugging

### debug
Turns on extra warning/debug messages. Not recommended for production systems, at will give way more info about what's happening than you care about, and will screw up non-html output (rss, opml, snapshots, etc).

Default: false

### benchmark
Turns on extra timestamp and memory benchmarking info when debug mode is turned on. Generates lots of output.

Default: false
