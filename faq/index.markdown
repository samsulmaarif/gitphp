---
layout: page
title: Frequently Asked Questions
---
# Frequently Asked Questions

## General Setup

### GitPHP says it can't run the git executable
Try setting the 'gitbin' config variable to the full path to your git executable. If that still doesn't work and you're sure your git executable is set up correctly, check to make sure [safe mode](http://us.php.net/manual/en/features.safe-mode.php) is turned off.

## Project Setup

### GitPHP says there are "No projects found" in my projectroot
Try setting the 'debug' config option to true and loading up GitPHP. At the bottom of the page, you'll see info on the directories being searched and which ones are being skipped.

### With debugging turned on, it says GitPHP is skipping myproject/.git
The .git hidden directory means you've copied your entire working copy into /projectroot/myproject, not the [bare repository](http://schacon.github.com/git/user-manual.html#public-repositories). You need to use a bare repository with GitPHP.
