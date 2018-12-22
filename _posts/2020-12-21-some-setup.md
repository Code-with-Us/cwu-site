---
categories: [jekyll]
date:   2018-12-21 09:45:00 -0500
excerpt_separator: <!--more-->
layout: post
# permalink:
published: true
tags: [setup, config]
title:  "Jekyll Project: Some Setup"
---

The first thing I did after installing the project was add all of the folders I'll need later - _pages, _includes, assets, _sass, and _data. These folders aren't included in the base install, because you don't need them unless you plan to customize your blog and add new pages and functionality. If you're fuzzy on what any of those directories do, the [Jekyll documentation](https://jekyllrb.com/docs/) is pretty good. Look at the "Content" section in the sidebar on the right.

(Most of those folders _are_ included in the Minima theme's folder, which lives in the /usr/share/rvm/gems/ruby-2.5.1/gems/minima-2.5.0 directory. That confused me at first. Why put all of the folders and files that are actually generating the site in some hard to reach place? The reason for putting everything in the Minima theme folder, is to make sure that you get the benefit of any updates to the Minima theme. You could just copy all of those folders and files to your project directory, but then any updates to the Minima gem wouldn't have any effect on your site. BTW, the command to show where the Minima theme folder is is: 'bundle show minima') 

(Oh, and don't alter any of the files in the Minima theme folder. If you want to override one of those files, copy it to your project directory. The reason for that is that if you make a new project, that new project will use the same Minima theme folder as your old project.)

I also spent some time looking at the config.yml file and going over some of the default settings that don't show up in the base install. The only changes I made were to the comments. 

The base install has a pretty slim config file. It doesn't even include some of the config options that come with Minima, like the header_pages setting. header_pages allows you to set which pages you want to appear in Minima's navigation menu and the order you want them to be in. The About page is included by default (this is also the only page, other than the home page, that appears in the root directory), but you can include the names of any additional pages you want to appear in the menu at the top right of your site. I don't plan to use this feature, because in order to use it, you need to place your pages in the root directory and not in the _pages directory. There's probably some way to adjust that, but I haven't been able to find it yet.


I looked at the "front matter" settings in the welcome post too. You don't have to include anything in a post or page's front matter, other than the 3 dashes, but there are some useful settings available, like categories and tags, and permalink and publication settings. For example, using the publication setting, you can set the welcome post to 'published: false', which means you can hang on to it without actually showing it. I added some additional front matter to my posts, but commented out a couple of things I'm not using yet.