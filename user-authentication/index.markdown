---
layout: page
title: User Authentication
---
# User Authentication

GitPHP supports basic user authentication, in order to grant additional features to specific privileged users.

**Passwords are sent as plaintext, so user authentication is only as secure as your server setup. If you are in any way concerned about malicious users accessing resources they do not have access to, it is strongly recommended that you take additional measures beyond GitPHP to protect your install, such as enabling SSL.**

## User Setup
GitPHP users are defined in the config file config/users.conf.php. If this file does not exist, or does not have any users in it, the entire user authentication functionality will be disabled and the login link will be hidden. Users are defined as individual key-value arrays within a main user array, $gitphp_users. Each individual user has a 'username' and 'password' key, set to the user's login username and password, respectively.

{% highlight php %}
$gitphp_users = array(
  array(
    'username' => 'user1',
    'password' => 'password1'
  ),
  array(
    'username' => 'user2',
    'password' => 'password2'
  )
);
{% endhighlight %}

## User Access
Currently, the following functionality can be allowed on a per-user basis:

* Restrict access to certain projects to specific users, using the ['allowedusers' project setting]({{ site.baseurl }}/project-list/#project_settings)

## Non-interactive Login
If you are integrating with GitPHP functionality through a non-interactive interface, such as direct usage of non-HTML actions such as snapshot or RSS/Atom URLs, by default you will be considered an anonymous user, and will not have access if you have locked down access for anonymous users. In order to access restricted functionality, you will need to manually authenticate using the login action to generate a session key to use in subsequent authenticated requests. GitPHP uses standard PHP session functionality to generate session keys.

In order to initiate a login, you will need to submit a POST request to the login action. The login action is at (using http://localhost/gitphp as the URL of the GitPHP install) http://localhost/gitphp/?a=login, or http://localhost/gitphp/login if you’re using [Clean URLs]({{ site.baseurl }}/clean-urls). You will need to send the POST variables 'username’ and 'password’ as the username and password, respectively. The server will respond with a cookie in the HTTP header called PHPSESSID that contains your session key. You can send the PHPSESSID cookie with the same session key in subsequent requests to perform other actions as the same authenticated user.
