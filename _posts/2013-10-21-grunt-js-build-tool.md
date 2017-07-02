---
layout: post
title:  "GRUNT – JavaScript Build Tool For Everyone"
date:   2013-10-21 13:34:32 +0300
categories: placeholder
permalink: "grunt-javascript-build-tool-for-everyone/"
---

It doesn’t matter if you are a high level developer or a newbie – [Grunt][link1] can help you. I will share a few practical ways I use Grunt with. You can do a lot more with Grunt than just those solutions that I will discuss. I will only show only a few of my favorites. Also I am still in the learning process of all of the benefits of Grunt, so if you have a usage that you think is important and is not listed here, please share! All of my current usages for Grunt is for static resources.

# Minify your code

With Grunt you can easily minify your code into a destination file. The most common way to minify a file with Grunt is to use [Uglify.js][link2]. there is a lot of information on the Grunt website on [how to get started][link3].

# Combine a few JavaScript files

With Grunt you can combine a few files into one file – that is great for configuration files. You probably have different configuration values on your development server than your production server – just make all your configurations on a separate file and combine it with Grunt. The build will be per server.

There are a lot of ways to handle configuration in JavaScript. The most obvious is to just put it in the script without thinking about it too much. That solution is good only if you test everything on production, but for sane developers like us that want to test our scripts on multiple environments we need a good way to easily move our scripts from one environment to the other. With Grunt it is easy to do so – use a settings file that is combined during the build process.

# JSLint

you can put [JSLint][link4] as part of the build process, personally I don’t use that feature since I use JSLint directly into my IDE, but that can be useful for other people.

# Testing

We can integrate our tests with the Grunt build. This is extremely useful since I can integrate the testing process directly to the build process and when the test is failing – I will get an immediate feedback.

# Reformatting code

Remove all of your debugging code on the build, that way no accidental console.log statements on the real script.

# How to install?

A great [in depth manual][link5] is in the Grunt website. It is depended on [Node.js][link6].

[link1]: http://gruntjs.com/
[link2]: https://github.com/mishoo/UglifyJS
[link3]: http://gruntjs.com/getting-started
[link4]: http://www.jslint.com/
[link5]: http://gruntjs.com/getting-started
[link6]: http://nodejs.org/