---
layout: post
title:  "How to use multiple SSH key settings for different github account"
date:   2018-09-28 21:11:00 +0530
categories: jekyll update
---
First, create multiple accounts in github account with username `<username1>, <username2>`.  

Create multiple ssh keys using
{% highlight command %}
$ ssh-keygen -t rsa -C "username1@youremail.com"
$ ssh-keygen -t rsa -C "username2@youremail.com"
{% endhighlight %}

create multiple ssh key example: thejsblog-author, thejsblog
{% highlight command %}
~/.ssh/id_rsa_thejsblog_author
~/.ssh/id_rsa_thejsblog
{% endhighlight %}

then add keys as such
{% highlight command %}
$ ssh-add ~/.ssh/id_rsa_thejsblog_author
$ ssh-add ~/.ssh/id_rsa_thejsblog
{% endhighlight %}

you need to delete all cached keys used before
{% highlight command %}
$ ssh-add -D
{% endhighlight %}

you can check your saved keys
{% highlight command %}
$ ssh-add -l
{% endhighlight %}

#### Add/Modify config file

{% highlight command %}
$ cd .ssh # from your home folder 
$ touch config
$ subl config
{% endhighlight %}

{% highlight ruby %}
#thejsblog-author account
Host github.com-thejsblogauthor
	HostName github.com
	User git
	IdentityFile ~/.ssh/id_rsa_thejsblog_author
#thejsblog account
Host github.com-thejsblog
	HostName github.com
	User git
	IdentityFile ~/.ssh/id_rsa_thejsblog
{% endhighlight %}

Modify the username and email of the current repo using 

{% highlight command %}
$ cd repo1
$ git config user.name "the js blog"
$ git config user.email "username1@gmail.com" 

$ cd ../repo2
$ git config user.name "the js blog author"
$ git config user.email "username2@gmail.com" 
{% endhighlight %}

Add your remote origin as such it finds the identity in config file 

{% highlight command %}
$ git remote add origin git@github.com-thejsblogauthor:thejsblog/thejsblog.github.io
{% endhighlight %}

then you can use the normal way to push, pull code.