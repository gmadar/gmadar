---
layout: post
title:  "Best Practice to Build a Backbone.js App"
date:   2014-06-03 13:36:32 +0300
categories: placeholder
permalink: "best-practice-to-build-a-backbon-js-app/"
---

There is no one best way to build a Backbone.js app, Backbone.js is so flexible that you can write a good application is many ways.

Backbone.js has a lot of critics. The most obvious of all is the claim that there is no one straight forward way to build a Backbone.js app, more than one recipe exist. Every individual is doing it a little bit different. Not necessarily a bad thing.

# What You Already Need To Know

This is a basic tutorial for creating an application architecture but you should already know what is a backbone model, collection, view and how to create them.

# Freedom of Coding

You can built an app in any way You want. That can be a bad thing if you are not such a good developer. So I will say to you that if you are planing to be a mediocre developer, don’t develop in Backbone.js, it’s not that it is hard, it’s actually very easy. So easy that it will let you do stupid things, similar to PHP.

# Gradual Adaptation

Backbone.js is a very versatile tool. You can basically do whatever it is you want. One of these perks is the ability to convert your app gradually to Backbone.js. Yes! it is not a framework, you can play with a little feature and you can migrate your app bit by bit.

# Power Of Plugins

I’m *not* talking about Backbone Plugins… those exist and they are great. I’m referring to any JavaScript plugin that exist. want to use the funky jQuery dropdown plugin that you saw? You can! Or what about this beautiful bootstrap tooltip plugin? You can.

In fact it is very easy to use any plugin and embed it in your Backbone.js application. This feature was the most important one for me.

# Application Structure

After the ‘why’ let’s move on to the ‘how’, Every Backbone.js app I’m building has the same structure layout. It does not have to be in that structure, I just found out that most of the time that structure is a best practice for me.

I’m using one global variable that holds the entire application. Usually I call it ‘app’.

here is the structure of the app object:

{% highlight javascript %}
var app = {
        bb : {
            Models : {},
            Collections : {},
            Views : {}
        },// backbone data
        collections : {},
        models : {},
        views : {},
        data : {
            rawData : {}
        }
    };
{% endhighlight %}

Under the app object there is another object called ‘bb’ that is my short to Backbone, all my Backbone objects will exist under the ‘bb’ object.

Under the ‘bb’ object there are three types of objects that start with an uppercase

* Models
* Collections
* Views

All of the models will be under ‘app.bb.Models’, collection under ‘app.bb.Collections’  and views under ‘app.bb.Views’

The actual instances of models will be under ‘app.models’, same for collections and views.

# Creating a New Model Object

When creating a new model, just extend the ‘app.bb.Models’ object:

{% highlight javascript %}
_.extend(app.bb.Models, {
        MyModel : Backbone.Model.extend({

        })
});
{% endhighlight %}

It is best practice that the object name will also start with an uppercase, this way it will be easy to distinguish between objects and object instances.

# Creating a New Model Object Instance

Creating an object instance is simple:

{% highlight javascript %}
app.models.someItem = new app.bb.Models.MyModel();
{% endhighlight %}

The same process apply to collections and views.

# Raw Data

Preserving data after manipulation could be easy when you have a dedicated object for it. Want to create data that is not part of your models / collections / views? In those cases I save the data under ‘app.data’ and ‘app.data.rawData’. This is not a good idea if you have a huge amount of data – the browser have a size limit and with a humongous amount of data it could crash.