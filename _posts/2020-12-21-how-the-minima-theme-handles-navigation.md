---
categories: [jekyll]
date:   2018-12-21 14:25:00 -0500
excerpt_separator: <!--more-->
layout: post
# permalink:
published: true
tags: [learning, howto, navigation, menu, Minima, themes]
title:  "Jekyll Project: How the Minima Theme Handles Navigation"
---

This is a post about site navigation in Jekyll using the default Minima theme. If you have a Jekyll blog, have written a few posts, created an additional page or two, and dabbled in creating includes and layouts, then this post is for you.

Minima makes adding a navigation menu pretty easy. Here's how to do it. In your project's _config.yml file, add the lines:

{% highlight yml %}
header_pages:
  - about.md
{% endhighlight %}

Stop your server, if it's running, and restart it. If you still have an about.md file in your root directory and you haven't changed your site's styles too drastically, then when you look at the homepage in your browser, you'll see an "About" menu item at the top right. 

To add additional menu items, just add the names of the pages you'd like to include in your menu, in the order in which you'd like them to appear, e.g.,

{% highlight yml %}
header_pages:
  - about.md
  - blog.md
  - portfolio.md
{% endhighlight %}

This is a great feature, but as I alluded to above, to use it, you have to put your pages in your project's root directory. That's not standard practice. Generally speaking, pages should be placed in the _pages directory. 

So, what would we need to do to keep on using Minima's built-in navigation menu, while at same time keeping all of our pages in the _pages directory?

Let's take a look at the logic that's powering Minima's menu. Use 'bundle show minima' to locate and then navigate to the Minima theme's directory. On my machine that path looks like this:

/usr/share/rvm/gems/ruby-2.5.1/gems/minima-2.5.0

In the _includes folder, find and open the header.html file. Take a look at lines 4 and 5:

{% highlight liquid %}
{%- assign default_paths = site.pages | map: "path" -%}
{%- assign page_paths = site.header_pages | default: default_paths -%}
{% endhighlight %}

Let's talk about what these lines are doing. Jekyll uses a templating language called Liquid. The syntax we see in lines 4 and 5 is Liquid syntax. Line 4 declares a new variable called *default_paths* and assigns it to an expression that evaluates to an array of paths. *site.pages* is a built-in Jekyll object that contains an array of page objects. Each page object contains metadata about a page on your site. The pipe operator tells Liquid to take the value of the expression to the left of the pipe and run the filter to the right of the pipe on that value.  In this case, we're running the *map* filter on *site.pages*. The *map* filter creates an array of values by extracting the values of a named property from another object. In this case, *map* is using the "path" key, which we know is a property of each *site.pages* object. How do we know that? Well, you'd have to extract the values paired with that key from all of the objects in using the key 'path'.
          {%- assign default_paths = site.pages | map: "path" -%}
          <!-- Declare page_paths and assign it to the array of page file names in the header_pages object. If there aren't any such page file names, assign page_paths to the default_paths array. -->

