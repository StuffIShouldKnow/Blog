+++
date = "2016-08-10T15:10:21+02:00"
draft = false
title = "Octopus can transform"
tags = ["Octopus Deploy", "Transform", "XML"]
comments = true
+++

I have not worked alot with **[Octopus Deploy](https://octopus.com/)** to be honest, but I feel like I need to learn more about it. Today I discovered that Octopus can be used to transform config files, which saved me alot of trouble in a situation where the test environment doesn't fully replicate the production environment (I know it's not ideal, but it's out of my control). 

In my situation, I have a config file in which I need to insert some xml based on the environment I'm currently deploying to. For this, I had to create 3 files:

- example.config
- example.Test.config
- example.Production.config

After that, just enable XML transformations in your deployment process and you're good to go. Just make sure all the config files are in the nuget package, I kind of missed that at first. 

