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

This is a post about site navigation in Jekyll version 3.8.5 using Jekyll's default theme Minima version 2.5.0. If you have a Jekyll blog, have written a few posts, created an additional page or two, and dabbled in creating includes and layouts, then this post is for you.

## The Basics

Minima makes adding a navigation menu to your site pretty easy. Here's how to do it. In your project's _config.yml file, add the lines:

```yml
header_pages:
  - about.md
```

Stop your server, if it's running, and restart it. If you still have an about.md file in your root directory and you haven't changed your site's styles too drastically, then when you look at your homepage in your browser, you'll see an "About" menu item at the top right. 

![minima default menu](/assets/images/welcome-shot.png){:class="img-responsive"}

To add additional menu items, just add the names of the pages you'd like to include in your menu, in the order in which you'd like them to appear, e.g.,

```yml
header_pages:
  - about.md
  - blog.md
  - portfolio.md
```

By default additional pages need to be added to your project's root directory. That's not a best practice. Generally speaking, pages should be placed in the _pages directory. In order to do that you'll need to add one additional line to your _config.yml file:

```yml
include:
  - _pages
```

This setting tells Jekyll to include the *_pages* directory during conversion. Ordinarily, files or directories with a leading underscore or dot would be ignored during conversion.

Now you just need to alter the paths to your pages in *header_pages*. For example:

```yml
header_pages:
  - _pages/about.md
  - _pages/blog.md
  - _pages/portfolio.md
```

## How does it work?

Let's take a look at the logic that's powering Minima's menu. Use 'bundle show minima' to locate and then navigate to the Minima theme's directory. I'm using rvm, so on my machine that path looks like this:

```yml
/usr/share/rvm/gems/ruby-2.5.1/gems/minima-2.5.0
```
In the *_includes* folder, find and open the *header.html* file. Take a look at lines 4 and 5:

{% raw %}
```markdown
{%- assign default_paths = site.pages | map: "path" -%}
{%- assign page_paths = site.header_pages | default: default_paths -%}
```
{% endraw %}

Jekyll uses a templating language called Liquid. The syntax we see in lines 4 and 5 is Liquid syntax. 

In short, lines 4 and 5 declare a new variable called *page_paths* that is assigned to an array of file paths leading to the pages we'd like to appear in our menu, e.g. ["_pages/about.md", "_pages/blog.md"]. Now, let's walk through it.

### Line 4
- Line 4 declares a new variable called *default_paths* and assigns it to an expression that evaluates to an array of page file paths. 
- *site.pages* is a built-in Jekyll object that contains an array of page objects. Each page object contains metadata about a page on your site. 
- The pipe operator tells Liquid to take the value of the expression to the left of the pipe and run the filter to the right of the pipe on that value.  In this case, we're running the *map* filter on *site.pages*. 
- The *map* filter creates an array of values by extracting the values of a named property from another object. In this case, *map* is using the "path" key, which we know is a property of each *site.pages* object, to extract the values associated with that key. (How do we know that *site.pages* contains a path property?)

### Line 5
- Line 5 declares a new variable called *page_paths* and assigns to it an expression that evaluates to another array of page file paths. 
- *site.header_pages* is the custom variable that we created in _config.yml and within which we defined an array or pages paths and file names, e.g. "_pages/about.md".
- In this case, we're running the *default* filter  on *site.header_pages*. The *default* filter allows you to specify a fallback in case a value doesn’t exist. *default* will show its value if the left side is nil, false, or empty. In this case, *page_paths* will default to *default_paths* in the event that *site.header_pages* is empty.

So, we have a *page_paths* variable with some page paths in it, but what are we going to do with it? Well, it used to be that the next line to interest us was:

{% raw %}
```markdown
{%- if page_paths -%}
```
{% endraw %}

This changed a bit at the end of October, 2018, when a couple of lines were altered fix a small bug that occurred on mobile devices when the nav element was empty. A new line was added just after lines 4 and 5:

Well, it used to be that the next line to interest us was:

{% raw %}
```markdown
{%- assign titles_size = site.pages | map: 'title' | join: '' | size -%}
```
{% endraw %}

Let's walk through it.

- Line 6 declares a new variable called titles_size and assigns to it an expression that evaluates to the number of characters in all of the page titles joined together. 
- As we discussed earlier, *site.pages* is a built-in Jekyll object that contains an array of page objects. Each page object contains metadata about a page on your site.
- In this case, we're running the *map* filter on *site.pages*
- The *map* filter creates an array of values by extracting the values of a named property from another object. In this case, *map* is using the "title" key, which we know is a property of each *site.pages* object, to extract the values associated with that key. 
- Next, the array created by *map* is passed to *join.* *join* combines the items in an array into a single string using its argument as a separator. In this case, the argument is an empty string, which will have th effect of joining our page titles end-to-end.
- Next, the string by *join* is passed to *size.* *size* returns the number of characters in a string (or the number of items in an array).
