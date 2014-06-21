---
layout: page
title: Build
---
# Build

Running GitPHP directly from a snapshot tarball or a git checkout is possible if you would like to try the bleeding edge features.

**There is no guarantee that a bleeding edge source copy is working correctly or is bug free.**

There are a couple preparation steps typically done on release tarballs that you will need to do manually to make sure your bleeding edge GitPHP is fully functional.

1. Gettext lanugage catalogs need to be compiled into binary catalogs before they can be used. You will want to run the message compile script. This depends on your system having the msgfmt command installed. It typically comes with the [gettext](http://www.gnu.org/software/gettext/) package.
```
./util/msgfmt.sh
```
2. Scripts and CSS files are stored in the repository in an uncompressed format for development. You'll want to minify them into compressed versions to reduce bandwidth for your users, using the minification script. This depends on having the java command, which comes with any [Java](http://www.java.com/) runtime environment.
```
./util/minify.sh
```

Note that you will need to rebuild your message bundles and re-minify your scripts whenever you pull changes from the git repository to ensure the new changes get included in the compiled files.
