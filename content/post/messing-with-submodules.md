+++
date = "2016-08-11T12:18:13+02:00"
draft = false
title = "Messing with submodules"
tags = ["Git", "Submodules", "Wercker", "Deploy"]
comments = true
+++

Today I've been trying to set up automatic deployment for this blog, using **[Wercker](http://wercker.com/)**. There is a nice guide to follow [here](https://gohugo.io/tutorials/automated-deployments/), although it didn't go without issues. At first, everything was all nice and green on the dashboard and I was happy. But, when navigating to the site, there was nothing. 

Checking the html files on Github confirmed this, the files where empty. The index.xml file contained all the right stuff though. This turned out to be a problem with the theme I'm using. Or, not the theme itself, the theme is fine. But I had to import it as a git submodule for Wercker to actually be able to use the theme while building my site. 

I created a new submodule using the following command:

    git submodule add https://github.com/zhe/hugo-theme-slim

This created a .gitmodules file for me, clone the module in to a hugo-theme-slim folder and added the submodule to my .git/config file. But, I want the theme to be in a folder called themes/slim, not in the folder git put it. There should be a git command for this. but I couldn't make it work. So, in my .gitmodules I changed the path of my submodule, and changed the name to be the same as the path.

This wasn't enough of course, as now my build would fail because of the following error:

    No submodule mapping found in .gitmodules for path 'themes/slim'

Seems like the config file in my .git folder needed some attention aswell. The submodule is defined there too, and it's really great if the submodule has the same name in both this file and the .gitmodules file. So, changed it to themes/slim here too, and now everything works. I have content and everything. 

**.git/config**

    [submodule "themes/slim"]
        url = https://github.com/zhe/hugo-theme-slim
   
   **.gitmodules**

    [submodule "themes/slim"]
	    path = themes/slim
	    url = https://github.com/zhe/hugo-theme-slim

I going to keep learning about submodules though, I don't think this manual workaround should be necessary, I'm sure there's an easier way to be able to set name and path for your submodules.