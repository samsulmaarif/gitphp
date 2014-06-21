---
layout: page
title: Caching
---
# Caching

To turn on caching, set the 'cache' config item to true.  GitPHP will cache every page's output, including plaintext output and binary output such as blobs and snapshots, for the number of seconds specified in the 'cachelifetime' config key.  You will need to set the "cache" directory writable by the server, as with the templates_c directory during installation.

GitPHP can also cache immutable objects from the git repository, by setting 'objectcache' to true.  These cached objects can be reused on multiple pages.  The 'objectcachelifetime' config key controls how long they are cached.  Since these objects don't ever change in the git repository, they can be cached for significantly longer than templates can (or in theory, forever).  This option can be used on its own, or in addition to the regular template 'cache' option for the maximum benefit.  This option also requires the "cache" directory writable by the server, as above.

The 'cacheexpire' key is recommended for most users.  With this option on, GitPHP will attempt to keep the cache in sync by automatically expiring any cached pages that are older than the most recent commit, on any branch.  It is a slight performance hit to make this check, but the performance hit is tiny compared to the gain you get from turning on caching.  It will  avoid situations where users are getting a cached version of a page that isn't up to date and doesn't reflect the most recent commit, or worse, pages that have been cached at different times and show data from both before and after a commit (eg page 1 of the shortlog shows the most recent commit but page 1 of the log was cached a while ago and doesn't show the most recent commit).

However, if your project is so active that commits are constantly coming in and invalidating the cache, rendering it useless, it would be better to turn cache expiration off and just set a really short cache lifetime of a few seconds.  In other words:

Most users:
* Set 'cache' to TRUE
* Set 'objectcache' to TRUE
* Set 'cacheexpire' to TRUE (this is the default)
* Set 'cachelifetime' high, 3600 seconds (1 hour) or more. (3600 is the default)
* Set 'objectcachelifetime' even higher, eg 86400 seconds or more.  (86400 is
  the default)

These are the defaults.

Extremely active projects, with commits every few seconds, or advanced users that know exactly how often commits come in and want to save the performance of the expiration check:
* Set 'cache' to TRUE
* Set 'objectcache' to TRUE
* Set 'cacheexpire' to FALSE
* Set 'cachelifetime' low, between 5-10 seconds.
* Set 'objectcachelifetime' high, 86400 seconds or more.  (86400 is the default)
