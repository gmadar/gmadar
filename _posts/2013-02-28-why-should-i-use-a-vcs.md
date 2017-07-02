---
layout: post
title:  "Why Should I Use A VCS"
date:   2013-02-28 13:29:32 +0300
categories: placeholder
permalink: "why-should-i-use-a-vcs/"
---
## Ohh crap my data is gone

So I re-created it with some links that might help you find what you are looking for, instead of giving you a 404 page.

I did it! I worked on my super cool new iPhone app. The app will upgrade my bank account status for sure. I’m on my way to brag about it to my friends and on my way the laptop fell down and.. Ohh CRAP! My hard drive is dead! What should I do? Take it to the trash? Or pay  a *lot* of money and try to restore it? 

## Huge bug – Let’s go back!

This time on my way to show off my cool app to my friend I didn’t break anything. As I present it, my dear friend found a critical bug on my new feature I've just added. I want to put it on the app store today, but it will take me three days to take the feature down, it has a lot of dependencies. Also I know it will take me four days to fix it so it will be a waste of time to work three days just to take it off. Bottom line? I can’t put the app on the app store today… Bummer!

## Backup the code before changing the code

OK – This time I decided that before each day of work I will backup my code. Not on the current machine because that one tend to break.

After a long day of coding – I showed my friend what I did and he (Again!) found a critical bug, well I didn’t need to waste 3 days to go back but I would like other features I worked on to stay. I did some ants work and merge the morning  version with just the features I wanted. That “only” took me an hour and a half. But what should I do with all the rest of the code (the one with the bug) I worked on that day?

## Should I backup the code on every change?

And then a question emerged – Should I backup the code after each feature I worked on? That work is frustrating and also there are always situations when I need to leave current work because some other bug that was found is more important. And one last problem on the subject – If I did 5 backups in a day and there is a bug in backup number 2 that mean that the bug is also exist in versions 3,4,5 of the backups. So what is the gain in that?

## Merging horror

Me and my Co-App partner working on the same code together, that caused some merging horrors. When working on the same files, you can end up working together to merge the files for more than an hour each day.

## And then came VCS

The great news is that for all of the above there is a solution. It is called VCS (Version-Control-System). With VCS I can control my code – I can backup my data whenever I want, It will take 5 second for each backup, I can see the history of the last work with a comment and a date.

In a VCS we can work on a few features at the same time all separated from each other. This is made simple with branches and it is super easy with Git. Not so trivial with SVN.

There are a lot of types out there – I have experience in SVN and GIT. For my opinion GIT is better but that is for a different post. In the meantime – I hope you have reached the conclusion that you should use an VCS. Git, or any other VCS system.