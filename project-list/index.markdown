---
layout: page
title: Project List
---
# Project List

## Project List Methods
There are several ways to populate the list of projects in GitPHP.

### Directory List
If you do not create the config file config/projects.conf.php or do not put any settings in it, by default GitPHP will list out all projects it can find in the project root. Projects will be categorized in GitPHP by directory by default, unless the category is overridden (see [Project Settings](#project_settings) below).

If you set the [exportedonly]({{ site.baseurl }}/configuration-options/#exportedonly) config flag, the list will only show projects that have been exported to the git daemon with the git-daemon-export-ok special file.

### Array
In config/projects.conf.php, you can set the $git_projects variable to an array of projects, and only these projects will be displayed. These are project paths relative to the project root.

{% highlight php %}
$git_projects = array(
  'gentoo.git',
  'php/gitphp.git',
  'core/fbx.git'
);
{% endhighlight %}

### File List
In config/projects.conf.php, you can set the $git_projects variable to the path to a list of projects.

{% highlight php %}
$git_projects = '/git/projectlist.txt';
{% endhighlight %}

This file contains a list of project paths relative to the projectroot, with each optionally followed by a space and an owner. The format is the standard Gitweb project list format, which can also be exported by apps like Gitosis and Gitolite.

```
gentoo.git Chris Han
php/gitphp.git Chris Han
core/fbx.git
```

### SCM-Manager Config
In config.projects.conf.php, you can set the $git_projects variable to the path to an [SCM-Manager](http://www.scm-manager.org/) repository config file. This is usually named repositories.xml, and resides in your SCM-Manager config directory in your home directory. GitPHP will only display git projects marked as public in SCM-Manager.

{% highlight php %}
$git_projects = '~/.scm/config/repositories.xml';
{% endhighlight %}

## Project Settings
Several GitPHP settings can be overridden on a per-project basis. There are couple different ways to set these per-project settings.

### Per-Project Settings
The following settings are unique to per-project settings:
* category - the category for the project
* owner - the owner of the project
* description - the description of the project
* website - the website url of the project
* allowedusers - an array of users that are allowed to access this project. Anonymous users, as well as users not in this list, will not be able to see or access this project. By default, if this option is not set, all anonymous and logged in users will have access to this project. For more information on prerequisite user setup, see [User Authentication]({{ site.baseurl }}/user-authentication).

Additionally, the following global settings can be overridden on a per-project level:
* [cloneurl]({{ site.baseurl }}/configuration-options/#cloneurl) - the full clone url of the project. Can be set to an empty string to say the project has no clone url
* [pushurl]({{ site.baseurl }}/configuration-options/#pushurl) - the full push url of the project. Can be set to an empty string to say the project has no push url
* [bugpattern]({{ site.baseurl }}/configuration-options/#bugpattern) - the bug number pattern of the project
* [bugurl]({{ site.baseurl }}/configuration-options/#bugurl) - the bug url of the project
* [compat]({{ site.baseurl }}/configuration-options/#compat) - whether this project runs in compatibility mode

### Project Config File
In config/projects.conf.php, the variable $git_projects_settings can be set with per-project settings. Each key in this variable is the project path relative to the project root, ad the value is an array of settings mapped to values.

{% highlight php %}
$git_projects_settings['php/gitphp.git'] = array(
  'category' => 'PHP',
  'description' => 'GitPHP, a web-based git repository browser in PHP',
  'owner' => 'Chris Han',
  'cloneurl' => 'http://git.gitphp.org/gitphp.git',
  'pushurl' => '',
  'bugpattern' => '/#([0-9]+)/',
  'bugurl' => 'http://www.gitphp.org/issues/${1}',
  'compat' => false,
  'website' => 'http://www.gitphp.org',
  'allowedusers' => array(
    'user1',
    'user2'
  )
);

$git_projects_settings['gentoo.git'] = array(
  'description' => 'Gentoo portage overlay',
  'compat' => true
);
{% endhighlight %}

### Git Config
Config values can also be set in the project's git config itself. This is the 'config' file inside your git repository, or it can be accessed using the 'git config' command.

In the config, the section is `[gitphp]`, and the key is the setting. Your config file could have a section like this:

```
[gitphp]
    category = PHP
    description = GitPHP, a web-based git repository browser in PHP
    owner = Chris Han
    cloneurl = http://git.gitphp.org/gitphp.git
    pushurl = 
    bugpattern = "/#([0-9]+)/"
    bugurl = http://www.gitphp.org/issues/${1}
    compat = false
    website = http://www.gitphp.org
    allowedusers = user1
    allowedusers = user2
```

Or, by setting individual config keys using git-config on the command line:

```
git --git-dir=/git/project.git config gitphp.category PHP
```
