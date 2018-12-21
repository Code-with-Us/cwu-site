---
categories: [jekyll, learning, howto]
date:   2018-12-21 09:45:00 -0500
excerpt_separator: <!--more-->
layout: post
permalink: date
published: true
tags: [goals, todo]
title:  "Goals and Purpose"
---
I'm started this project to learn more about Jekyll and some of its themes and plugins. I'm thinking about trying to make my own theme, but that will probably come a bit later.

I'd like to learn how to turn a Jekyll blog into something more powerful, something that includes things like:

- search
- archives
- categories and tags
- pagination
- seo

There are plugins that will add each of those features, but they're not that easy to set up. That's what I'm going to do here: start with the default Minima theme and add one feature at a time, until I've got something that's as powerful as WordPress.

The first things I did was add folders for _pages, _includes, _data, and assets. These folders aren't included in the base install, although you can find them in the Minima folder. 

I also spent some time looking at the config.yml file and going over some of the default settings that don't show up in the base install. I looked at the "front matter" settings in the welcome post too. You don't have to include anything in a post or page's front matter, other than the 3 dashes, but there are some useful settings available, like categories and tags, and permalink and publication settings.