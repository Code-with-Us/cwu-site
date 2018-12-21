---
categories: [jekyll]
date:   2018-12-21 14:25:00 -0500
excerpt_separator: <!--more-->
layout: post
# permalink:
published: true
tags: [learning, howto, navigation, menu, Minima, themes]
title:  "How the Minima Theme Handles Navigation"
---

Jeyll's default theme is called Minima. Minima offers an easy way to add a navigation menu to your site. In your project's _config.yml file, add the lines:

header_pages:
  - about.md

Stop your server, if it's running, and restart it with 'bundle exec jekyll serve.' When you look at your page in your browser, you'll see a menu item at the top right. 

To add additional menu items, just add the names of the pages you'd like ot include in your menu, e.g.

header_pages:
  - about.md
  - blog.md

You can put menu items in whatever order you'd like.

This is a great feature, but it requires that you put your 

